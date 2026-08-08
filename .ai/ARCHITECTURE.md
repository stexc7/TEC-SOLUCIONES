# ARCHITECTURE.md — Cómo está construido

> Este archivo responde a *"¿dónde va este código?"* y *"¿por qué está así?"*.
> Manténlo al día: una arquitectura documentada que ya no coincide con la realidad
> es peor que no tener ninguna.

**Última revisión:** `2026-08-06`

---

## Vista general

```
  Visitante ──▶ Cloudflare Pages ──▶ Sitio Astro estático
                                          │
                                          └──▶ Formspree (formulario de contacto)
```

## Decisiones estructurales

| Decisión | Elección | Por qué | ADR |
|----------|----------|---------|-----|
| Estilo de arquitectura | Sitio estático | Catálogo informativo sin servicios propios de servidor | [`DECISIONS.md`](DECISIONS.md) |
| Contacto | Enlaces directos + Formspree | Evita operar infraestructura de servidor | [`DECISIONS.md`](DECISIONS.md) |

> Cada fila con consecuencias reales merece un ADR en `docs/adr/`.

## Estructura de carpetas

```
frontend/
  public/          # Archivos servidos tal cual, sin procesar por Astro.
  src/
    assets/        # Imágenes y recursos que Astro procesa y optimiza en el build.
    components/    # Componentes de presentación reutilizables.
    content/       # Datos estáticos del catálogo.
    layouts/       # Estructuras visuales compartidas.
    pages/         # Rutas generadas como HTML estático.
    styles/        # Estilos globales y tokens de diseño.
```

## Reglas de dependencia

> La regla más importante del archivo. Las flechas apuntan **hacia dentro**.

- Las páginas y componentes pueden importar contenido estático y estilos.
- El contenido no depende de servicios remotos para poder generar el sitio.
- El formulario se comunica directamente con Formspree desde el navegador.
- Las imágenes del catálogo (servicios, equipos) van en `src/assets/` y se importan desde el componente o página que las usa, para que Astro las optimice y las incluya en el build con hash de caché. Solo van en `public/` los archivos que deben conservar una ruta fija o no necesitan procesado: favicon, `robots.txt`, imágenes de redes sociales (Open Graph) referenciadas por URL absoluta.

Romper una de estas reglas requiere un ADR que lo justifique.

## Flujos principales

### Flujo: Visitante navega el sitio

1. Astro genera el HTML de cada página en tiempo de compilación (`npm run build`), a partir del contenido estático en `frontend/src/content/`.
2. Cloudflare Pages sirve esos archivos estáticos desde su CDN; no hay servidor de aplicación ni renderizado en cada petición.
3. El visitante ve el catálogo de servicios y equipos y los enlaces de contacto (WhatsApp, teléfono, correo) sin llamadas a una API.

### Flujo: Visitante envía el formulario de contacto

1. El visitante rellena el formulario en el navegador; la validación de cliente solo mejora la experiencia (no es la validación de seguridad, porque no hay servidor propio que la aplique).
2. El navegador envía la solicitud directamente al endpoint HTTPS de Formspree, identificado por `PUBLIC_FORMSPREE_FORM_ID`.
3. Formspree procesa el mensaje y lo entrega al buzón configurado del negocio; el sitio no guarda ni reenvía esos datos.

### Flujo: Despliegue a producción

1. Se fusiona un pull request aprobado en `main`.
2. GitHub Actions ejecuta el CI configurado sobre esa rama (validación previa a la publicación).
3. Cloudflare Pages instala dependencias (`npm ci`), ejecuta `npm run build` desde `frontend/` y publica el contenido de `frontend/dist`.

## Puntos de integración externos

| Servicio | Para qué | Qué pasa si se cae |
|----------|----------|--------------------|
| Formspree | Recibir el formulario de contacto | Siguen disponibles WhatsApp, teléfono y correo. |
| Cloudflare Pages | Publicar el sitio estático | El sitio no queda disponible hasta restaurar el hosting. |

## Rendimiento y escala

- Carga esperada: sitio informativo de bajo tráfico (catálogo + contacto), sin picos previstos por campañas o ventas online.
- Cuellos de botella conocidos: ninguno identificado; al ser HTML estático servido por CDN, el sitio en sí no impone límites de escala propios. El formulario de contacto depende de los límites de plan de Formspree.
- Estrategia de caché: gestionada por la CDN de Cloudflare Pages sobre los archivos estáticos generados en cada build; no hay caché de aplicación propia.

## Deuda técnica conocida

> Sé honesto aquí. La deuda no documentada se convierte en sorpresa.

| Qué | Por qué existe | Impacto | Cuándo se paga |
|-----|----------------|---------|----------------|
| Ninguna conocida a la fecha de esta revisión. | — | — | — |
