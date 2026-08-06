# STACK.md — Tecnologías del proyecto

**Última revisión:** `2026-08-06`

---

## Resumen

| Capa | Tecnología | Versión | Por qué |
|------|-----------|---------|---------|
| Lenguaje (backend) | No aplica | — | El sitio no tiene backend propio. |
| Framework (backend) | No aplica | — | El catálogo se genera de forma estática. |
| Lenguaje (frontend) | TypeScript | 5.x | Tipado para componentes y utilidades sin añadir complejidad al sitio. |
| Framework (frontend) | Astro | 5.x | Genera HTML estático rápido, con JavaScript mínimo y buen soporte para contenido. |
| Estilos | CSS nativo | Estándar web | Evita dependencias de estilos para un sitio pequeño y facilita un diseño móvil a medida. |
| Base de datos | No aplica | — | Servicios, catálogo y datos de contacto se mantienen como contenido estático. |
| Caché | No aplica | — | Cloudflare Pages entrega los archivos estáticos desde su CDN. |
| Cola / mensajería | No aplica | — | No existen procesos asíncronos propios. |
| Autenticación | No aplica | — | No hay cuentas ni áreas privadas. |
| Formulario de contacto | Formspree | SaaS | Recibe los mensajes sin operar un servidor ni guardar credenciales en el cliente. |
| Tests | Vitest | 3.x | Pruebas unitarias de utilidades y componentes cuando se implemente el sitio. |
| Linter / formateador | ESLint + Prettier | 9.x / 3.x | Mantiene una base TypeScript consistente. |
| Empaquetado | Astro | 5.x | Ejecuta la compilación estática a `dist/`. |
| CI/CD | GitHub Actions + Cloudflare Pages | — | Valida el proyecto en cada PR y publica desde la rama principal. |
| Hosting | Cloudflare Pages | — | Hosting estático global, sencillo y económico. |
| Observabilidad | Cloudflare Web Analytics | — | Métricas básicas sin implementar un servicio propio. |

## Versiones exigidas

```text
Node.js  >= 22.0.0 LTS
npm      >= 10.0.0
```

Las versiones exactas de las dependencias de aplicación se fijarán en
[`package-lock.json`](../package-lock.json) cuando se inicialice el frontend.

## Puesta en marcha

El frontend se creará en [`frontend/`](../frontend/). Cuando exista, se inicia así:

```bash
# 1. Instalar dependencias desde la raíz del frontend
cd frontend
npm ci

# 2. Ejecutar el servidor de desarrollo
npm run dev

# 3. Crear la versión estática de producción
npm run build

# 4. Previsualizar la compilación (opcional)
npm run preview
```

El servidor de desarrollo estará disponible habitualmente en
`http://localhost:4321`. La compilación genera archivos estáticos en
[`frontend/dist/`](../frontend/dist/).

## Despliegue

Cloudflare Pages se conectará al repositorio y usará esta configuración:

| Ajuste | Valor |
|--------|-------|
| Directorio raíz | `frontend` |
| Comando de instalación | `npm ci` |
| Comando de compilación | `npm run build` |
| Directorio publicado | `dist` |
| Rama de producción | `main` |
| Previsualizaciones | Una por cada pull request, cuando Cloudflare Pages esté conectado |

El resultado es un sitio estático servido por la CDN de Cloudflare. No se
desplegarán funciones, API ni procesos persistentes.

## Contacto

El sitio siempre mostrará enlaces directos de WhatsApp, teléfono y correo para
que una persona pueda iniciar contacto en un máximo de dos clics. El formulario
alternativo se enviará directamente a Formspree mediante su endpoint HTTPS.

| Configuración | Obligatoria | Ejemplo | Para qué |
|---------------|-------------|---------|----------|
| `PUBLIC_FORMSPREE_FORM_ID` | Sí para activar el formulario | `abcdwxyz` | Identificador público del formulario de Formspree. Se asigna al crear el formulario. |
| `PUBLIC_WHATSAPP_NUMBER` | Sí | `593999999999` | Número de WhatsApp en formato internacional, sin `+` ni espacios. |
| `PUBLIC_CONTACT_PHONE` | Sí | `+593 99 999 9999` | Teléfono visible y destino de enlaces `tel:`. |
| `PUBLIC_CONTACT_EMAIL` | Sí | `contacto@ejemplo.com` | Correo visible y destino de enlaces `mailto:`. |

Los valores con prefijo `PUBLIC_` se exponen deliberadamente en el navegador.
No son secretos. Las claves privadas o de administración de Formspree nunca se
incluyen en el repositorio, las variables públicas ni el código cliente.

## Convenciones del stack

- El código del sitio vive en [`frontend/`](../frontend/) y se organiza según
  las convenciones de Astro: páginas en `src/pages/`, componentes reutilizables
  en `src/components/`, estilos globales y tokens en `src/styles/`.
- Se genera HTML estático por defecto. Solo se añade JavaScript de cliente si
  una interacción concreta no puede resolverse con HTML y CSS.
- El contenido del catálogo se representa localmente; no se hacen peticiones a
  una API ni a una base de datos.
- El formulario valida la experiencia del cliente, pero Formspree es quien
  procesa la solicitud. No se implementa un endpoint propio para el formulario.
- Las variables expuestas en Astro deben empezar por `PUBLIC_`. Nunca se usan
  para secretos.

## Lo que este proyecto **no** usa

| Tecnología | Por qué no |
|------------|------------|
| Backend o API propia | No se requieren datos dinámicos ni lógica de negocio de servidor para el alcance actual. |
| Base de datos | El catálogo es informativo y no existe gestión de pedidos, usuarios ni inventario en tiempo real. |
| Carrito, pagos o e-commerce | Están explícitamente fuera del alcance del proyecto. |
| Autenticación | No hay áreas privadas ni cuentas de cliente. |
| Framework CSS | CSS nativo cubre el diseño del sitio sin aumentar dependencias ni configuración. |
| Formulario con servidor propio | Formspree evita infraestructura, credenciales de correo y mantenimiento de backend. |
