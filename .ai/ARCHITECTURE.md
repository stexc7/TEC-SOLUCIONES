# ARCHITECTURE.md — Cómo está construido

> Este archivo responde a *"¿dónde va este código?"* y *"¿por qué está así?"*.
> Manténlo al día: una arquitectura documentada que ya no coincide con la realidad
> es peor que no tener ninguna.

**Última revisión:** `<AAAA-MM-DD>`

---

## Vista general

```
<Diagrama de bloques. ASCII está bien. Mermaid también.>

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
  src/
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

Romper una de estas reglas requiere un ADR que lo justifique.

## Flujos principales

### Flujo: `<nombre>`

1. 
2. 
3. 

## Puntos de integración externos

| Servicio | Para qué | Qué pasa si se cae |
|----------|----------|--------------------|
| Formspree | Recibir el formulario de contacto | Siguen disponibles WhatsApp, teléfono y correo. |
| Cloudflare Pages | Publicar el sitio estático | El sitio no queda disponible hasta restaurar el hosting. |

## Rendimiento y escala

- Carga esperada: 
- Cuellos de botella conocidos: 
- Estrategia de caché: 

## Deuda técnica conocida

> Sé honesto aquí. La deuda no documentada se convierte en sorpresa.

| Qué | Por qué existe | Impacto | Cuándo se paga |
|-----|----------------|---------|----------------|
| | | | |
