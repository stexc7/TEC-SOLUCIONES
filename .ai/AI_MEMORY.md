# AI_MEMORY.md — Memoria compartida entre sesiones

> **Este archivo es la memoria a largo plazo del proyecto.** Claude Code, Codex y
> Zoo Code escriben aquí y leen de aquí. Es lo que evita que cada sesión empiece
> desde cero.

## Cómo usarlo

**Al empezar una sesión:** lee todo el archivo.
**Al terminar una tarea:** añade lo que la próxima sesión necesitará saber.

### Qué **sí** va aquí

- Cosas que descubriste y no son evidentes leyendo el código.
- Trampas: "el test X falla en Windows por los saltos de línea".
- Preferencias del humano que ya te corrigió una vez.
- Estado de cosas a medias: "el módulo de pagos está a la mitad, falta el webhook".
- Contexto externo: "el cliente pidió priorizar móvil sobre escritorio".

### Qué **no** va aquí

- Lo que ya está en el código (se lee del código).
- Lo que ya está en el historial de Git.
- Decisiones de arquitectura → van a `DECISIONS.md` o a un ADR.
- Bugs → van a `BUGS.md`.
- Tareas → van a `TASKS.md`.

### Formato

```
### AAAA-MM-DD — <Título corto>
**Agente:** Claude Code | Codex | Zoo Code
**Contexto:** qué estabas haciendo.
**Aprendido:** el hecho que importa.
**Aplicar cuando:** en qué situación futura sirve esto.
```

Mantén el archivo **por debajo de ~200 líneas**. Cuando crezca demasiado,
consolida: fusiona entradas repetidas, borra lo que ya no aplica.

---

## Entradas

### 2026-08-09 — TASK-004: `ci.yml` adaptado, pendiente de confirmar en verde
**Agente:** Claude Code
**Contexto:** Al retomar, `feat/inicializar-astro` ya estaba mergeado (PR #3) y `frontend/package.json` ya traía `lint`/`format`/`typecheck`/`test`/`build` (ESLint, Prettier, Vitest, `astro check` — añadidos fuera de esta sesión en el commit `468d135`). Con eso, TASK-004 ya no estaba bloqueada.
**Aprendido:** Se reemplazó el job `placeholder` de `.github/workflows/ci.yml` por un job `node` real (`working-directory: frontend`, `cache-dependency-path` al lockfile de `frontend/`, y los pasos install/lint/format/typecheck/test/build). Se omitió `--coverage` a propósito: no hay `@vitest/coverage-v8` instalado ni umbral en `.ai/TESTING.md` (que sigue con la plantilla sin rellenar). **No pude verificar que el pipeline corra en verde**: este entorno no tiene Node.js en el PATH (ni Bash ni PowerShell lo encuentran) para correr los comandos en local, y no hay `gh` ni token para abrir el PR y disparar el trigger `pull_request` de GitHub Actions. La rama `ci/task-004-adaptar-workflow` está pusheada a `origin` pero sin PR.
**Aplicar cuando:** Antes de dar TASK-004 por cerrada, confirmar en GitHub que el run de "CI / Node.js" pasa y que tarda menos de 10 min. Si se repite la falta de `gh`/token en una sesión futura, avisar al humano de inmediato en vez de asumir que el CI pasará.

### 2026-08-08 — Cierre de sesión: PR de TASK-003 mergeado, detectado trabajo de Astro sin tarea formal
**Agente:** Claude Code
**Contexto:** Sesión de cierre (`/cerrar`). El PR de TASK-003 (#2) ya estaba mergeado a `main` al retomar. Al revisar el estado real del repo, apareció una rama `feat/inicializar-astro` (2 commits: init de Astro + página de inicio) pushada a `origin`, con `frontend/package.json`, `astro.config.mjs`, `src/pages/index.astro` y carpetas base — trabajo hecho fuera de esta sesión de Claude Code, sin entrada en `TASKS.md` ni `CURRENT_TASK.md`.
**Aprendido:** `frontend/package.json` solo trae los scripts `dev`/`build`/`preview`; **no** están instalados ESLint, TypeScript check ni Vitest, aunque `.ai/STACK.md` los exige como parte del stack. Eso bloquea TASK-004 (CI) hasta que se completen. También: `scripts/check-context.ps1` no excluye `frontend/node_modules/`, así que reporta ~80 falsos positivos de "enlace roto" que vienen de READMEs de dependencias — hay que filtrarlos a mano o arreglar el script antes de fiarse de su recuento.
**Aplicar cuando:** Antes de empezar TASK-004, confirmar en qué rama sigue el trabajo de Astro (`feat/inicializar-astro`) y si hay que fusionarla o abrir una tarea formal para ella. No asumir que `check-context.ps1` está limpio solo por el número de avisos: filtrar `node_modules` primero.

### 2026-08-07 — TASK-003 cerrada: arquitectura documentada, `backend/` eliminada
**Agente:** Claude Code
**Contexto:** `.ai/ARCHITECTURE.md` ya tenía el diagrama, la estructura de carpetas, las reglas de dependencia y las integraciones externas desde el commit `273a384`, pero `CURRENT_TASK.md` (sin commitear, huérfano de una sesión anterior) marcaba TASK-003 como pendiente. Se revisó a fondo y se detectó que solo faltaban "Flujos principales" y "Rendimiento y escala" con placeholders vacíos.
**Aprendido:** Se completaron los 3 flujos reales del sitio (navegación estática servida por Cloudflare Pages, envío del formulario a Formspree, y despliegue vía PR + CI + Cloudflare Pages) y la sección de rendimiento/escala. Además, la carpeta `backend/` existía vacía y sin trackear en git — era el resto de `backend/README.md`, borrado en `273a384` al adaptar la plantilla al stack estático, pero el directorio quedó huérfano en disco. Se eliminó por no tener uso (confirmado en `STACK.md`: "Backend o API propia: no se requiere").
**Aplicar cuando:** Si vuelve a aparecer una carpeta vacía y no trackeada en el repo, comprobar primero si es un resto de una limpieza anterior en el historial de git antes de asumir que es trabajo en progreso.

### 2026-08-06 — Plantilla alineada con el sitio estático
**Agente:** Zoo Code
**Contexto:** Tras definir el stack, se eliminaron los artefactos de la plantilla que suponían servicios de servidor.
**Aprendido:** No existe directorio `backend/`, rol de backend/datos, guía de API ni configuración de entorno privada. [`.env.example`](../.env.example) contiene únicamente las cuatro variables públicas de contacto: Formspree, WhatsApp, teléfono y correo. Los runbooks y la documentación de frontend describen el despliegue estático en Cloudflare Pages.
**Aplicar cuando:** Implementar el sitio solo en `frontend/`; no introducir una API, una base de datos ni cuentas de usuario sin una decisión y tarea nuevas.

### 2026-08-06 — TASK-002 cerrada: stack estático confirmado
**Agente:** Zoo Code
**Contexto:** Se eligió la tecnología base para el sitio informativo de
TEC-SOLUCIONES.
**Aprendido:** El sitio usará Astro 5, TypeScript y CSS nativo, compilado como
estático y alojado en Cloudflare Pages. No habrá backend, API, base de datos,
autenticación ni e-commerce. WhatsApp, teléfono y correo son canales de contacto
directos; el formulario se procesa mediante Formspree y requiere configurar su
identificador público durante la implementación.
**Aplicar cuando:** TASK-003 debe describir una arquitectura estática. TASK-004
debe validar Node.js 22 y la compilación `npm run build` desde `frontend/`.

### 2026-08-06 — TASK-001 cerrada: PROJECT.md relleno
**Agente:** Claude Code
**Contexto:** Primera sesión real del proyecto. El repo era el scaffold `ai-project-starter` sin datos concretos.
**Aprendido:** TEC-SOLUCIONES es un sitio web informativo/catálogo (no e-commerce) para un emprendimiento de servicios de tecnología: reparación, mantenimiento, optimización, venta de equipos y creación de páginas web. Usuarios objetivo: particulares. Sin carrito/pago online ni panel admin — el contacto se hace por WhatsApp/teléfono/email/formulario. Presupuesto, plazo y temas legales quedaron "por definir", el humano no los ha concretado aún.
**Aplicar cuando:** Al proponer stack (TASK-002) o arquitectura (TASK-003): priorizar algo simple, estático/ligero y económico, orientado a móvil, sin backend de e-commerce.

### AAAA-MM-DD — Plantilla inicial del proyecto
**Agente:** —
**Contexto:** Creación del repositorio a partir de `ai-project-starter`.
**Aprendido:** El proyecto sigue el contrato de `AGENTS.md`. Toda IA lee ese archivo primero.
**Aplicar cuando:** Siempre, al arrancar una sesión.

<!-- Añade entradas nuevas ARRIBA de esta línea, más recientes primero. -->

---

## Hechos permanentes

> Cosas que no cambian y toda IA debe saber. Sección estable, se edita poco.

- **Idioma:** código en inglés, documentación y comentarios en español.
- **Rama principal:** `main`. Protegida. Solo por PR.
- **Nunca** commitear `.env` ni credenciales.

## Preferencias del humano

> Cada vez que te corrijan sobre *cómo* trabajar, anótalo aquí.

| Preferencia | Por qué | Desde |
|-------------|---------|-------|
| | | |
