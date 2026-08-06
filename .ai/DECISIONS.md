# DECISIONS.md — Registro rápido de decisiones

> Para decisiones **pequeñas o medianas**. Las grandes (con consecuencias
> estructurales, difíciles de revertir) van a un ADR completo en `docs/adr/`.
>
> Regla práctica: si dentro de seis meses alguien va a preguntar *"¿por qué se hizo
> así?"*, escríbelo. Aquí o en un ADR.

---

## Formato

```
### AAAA-MM-DD — <Decisión en una frase>
**Contexto:** qué situación forzó la decisión.
**Decisión:** qué se eligió.
**Alternativas descartadas:** qué más se consideró y por qué no.
**Consecuencias:** qué se gana, qué se pierde, qué queda pendiente.
**Decidido por:** humano / Claude Code / Codex / Zoo Code.
```

---

## Decisiones

### 2026-08-06 — Sitio estático con Astro en Cloudflare Pages y contacto mediante Formspree
**Contexto:** TEC-SOLUCIONES necesita una web informativa y un catálogo para
particulares, sin carrito, pago en línea, cuentas ni panel administrativo. Se
priorizan el lanzamiento rápido, el bajo coste y una experiencia móvil rápida.
**Decisión:** Se usará Astro 5 con TypeScript y CSS nativo para generar un sitio
estático. Se desplegará en Cloudflare Pages. Los enlaces de WhatsApp, teléfono y
correo serán el canal de contacto principal; el formulario se enviará a
Formspree, sin backend propio.
**Alternativas descartadas:** (a) Next.js con Vercel: añade capacidades de
servidor no necesarias para el alcance actual. (b) Un backend o endpoint
serverless propio: aumenta mantenimiento, seguridad y configuración para una
necesidad que Formspree cubre. (c) Un framework CSS: aporta una dependencia que
CSS nativo no necesita en este sitio reducido.
**Consecuencias:** Se obtiene una web ligera, económica y sencilla de desplegar.
El catálogo se actualiza mediante cambios de contenido y una nueva compilación.
La disponibilidad y protección anti-spam del formulario dependen de Formspree;
su identificador público deberá configurarse al implementar el formulario.
**Decidido por:** humano, con propuesta de Zoo Code.

### 2026-01-01 — Un único contrato para todas las IAs en `AGENTS.md`
**Contexto:** Tres herramientas de IA (Claude Code, Codex, Zoo Code) trabajando sobre
el mismo repositorio, cada una con su propio archivo de configuración. Duplicar las
reglas en tres sitios garantiza que se desincronicen.
**Decisión:** `AGENTS.md` es la única fuente de verdad. `CLAUDE.md` y cualquier otro
archivo de configuración específico de herramienta solo apuntan hacia él y añaden lo
estrictamente propio de esa herramienta.
**Alternativas descartadas:** (a) Duplicar el contenido — se desincroniza. (b) Enlaces
simbólicos — no funcionan bien en Windows ni en todos los clones de Git.
**Consecuencias:** Una sola edición actualiza a las tres IAs. A cambio, cada
herramienta necesita un archivo puente de dos líneas.
**Decidido por:** humano

<!-- Añade decisiones nuevas ARRIBA de esta línea, más recientes primero. -->

---

## Decisiones revertidas

> No borres una decisión que dejó de valer. Muévela aquí con el motivo.
> Saber qué se intentó y falló vale tanto como saber qué funcionó.

| Fecha | Decisión | Por qué se revirtió | Reemplazada por |
|-------|----------|---------------------|-----------------|
| | | | |
