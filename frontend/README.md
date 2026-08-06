# frontend/

Aplicación web estática de TEC-SOLUCIONES, creada con Astro, TypeScript y CSS
nativo. Se publica como archivos estáticos en Cloudflare Pages.

> Esta carpeta se inicializará al implementar el sitio. Consulta
> [`.ai/STACK.md`](../.ai/STACK.md) para las versiones, comandos y configuración
> de contacto aprobados.

---

## Estructura esperada

```text
src/
  components/  Componentes reutilizables de presentación.
  content/     Datos estáticos del catálogo de servicios y equipos.
  layouts/     Estructuras visuales compartidas de Astro.
  pages/       Rutas que Astro compila a HTML estático.
  styles/      Estilos globales y tokens de diseño.
```

## Reglas

- El catálogo se mantiene como contenido local y se compila junto con el sitio.
- Se añade JavaScript de cliente solo cuando una interacción no se puede
  resolver con HTML y CSS.
- WhatsApp, teléfono y correo son enlaces directos; el formulario se envía a
  Formspree.
- Solo se exponen variables de entorno con prefijo `PUBLIC_`; nunca secretos.
