# Runbook: Desplegar a producción

**Cuándo usarlo:** publicación planificada o corrección aprobada.
**Plataforma:** Cloudflare Pages.

## Antes de empezar

- [ ] CI en verde en `main`.
- [ ] La compilación `npm run build` pasó desde [`frontend/`](../../frontend/).
- [ ] Las variables públicas de contacto están configuradas en Cloudflare Pages.
- [ ] Los enlaces de WhatsApp, teléfono y correo fueron revisados.
- [ ] El formulario de Formspree fue probado con un mensaje de prueba.

## Despliegue

1. Fusiona el pull request aprobado en `main`.
2. Cloudflare Pages instala dependencias con `npm ci`, ejecuta `npm run build` y publica `frontend/dist`.
3. Espera a que el despliegue se marque como correcto.
4. Comprueba en móvil y escritorio el catálogo, los enlaces de contacto y el formulario.

## Reversión

Usa el panel de Cloudflare Pages para volver al último despliegue correcto. Luego
comprueba los enlaces directos y el formulario antes de comunicar la recuperación.
