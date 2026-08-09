# CURRENT_TASK.md — La tarea de ahora mismo

> **Solo una tarea a la vez.** Este archivo es el foco. Si tiene tres tareas, no
> tiene ninguna.
>
> Zoo Code lee este archivo como su instrucción principal.

---

## Tarea activa

**ID:** `TASK-004`
**Título:** Adaptar el CI de `.github/workflows/ci.yml` al stack
**Estado:** `en revisión — código listo, CI sin confirmar en verde todavía`
**Agente asignado:** `Claude Code`
**Rama:** `ci/task-004-adaptar-workflow`
**Iniciada:** `2026-08-09`

### Objetivo

Configurar `.github/workflows/ci.yml`, hoy un placeholder de plantilla, para que valide de verdad el stack real del proyecto (Astro + TypeScript + Vitest) en cada PR y en `main`.

### Criterios de aceptación

- [x] `.github/workflows/ci.yml` adapta el bloque Node.js de la plantilla para instalar dependencias, ejecutar lint, formato, comprobación de tipos, tests y build desde `frontend/`.
- [x] Se elimina el job `placeholder` (y los bloques comentados de otros stacks que no aplican).
- [ ] El pipeline completo corre en menos de 10 minutos. **No verificado todavía**: no pude ejecutar `npm ci`/lint/test/build en local (Node.js no está en el PATH de este entorno) ni disparar el workflow real, porque no hay PR abierto (el trigger `pull_request` necesita uno) y no tengo `gh` ni un token para abrirlo.
- [ ] El flujo de despliegue descrito en `.ai/ARCHITECTURE.md` queda respaldado por un CI real. **Pendiente de confirmar** en cuanto el PR dispare el primer run.

### Archivos que se van a tocar

```
.github/workflows/ci.yml
```

### Enfoque

1. Revisar `.ai/STACK.md` para confirmar los comandos exactos (`npm ci`, lint, typecheck, test, build) una vez existan en `frontend/package.json`.
2. Adaptar el bloque Node.js ya presente en la plantilla de `ci.yml`.
3. Verificar que corre en un PR de prueba.

### Fuera de alcance en esta tarea

- Inicializar Astro o implementar páginas, componentes, estilos o contenido del sitio (si `frontend/` sigue sin `package.json`, esta tarea queda bloqueada hasta que exista).
- Configurar el despliegue en Cloudflare Pages (lo gestiona Cloudflare directamente, no GitHub Actions).

---

## Progreso

> Actualiza esto mientras trabajas. Es lo que permite retomar tras una interrupción.

| Paso | Estado | Nota |
|------|--------|------|
| 1. Confirmar que `frontend/` tiene `package.json` con scripts de lint/typecheck/test/build | Hecho | Ya estaban los 5 scripts (`lint`, `format`, `typecheck`, `test`, `build`) desde el commit `468d135`, fuera de esta sesión. |
| 2. Adaptar `ci.yml` | Hecho | Job `node` reemplaza al `placeholder`; corre `npm ci` → lint → formato → tipos → tests → build con `working-directory: frontend`. Se omite `--coverage` (sin provider instalado, sin umbral en `TESTING.md`; anotado en `TASKS.md`). |
| 3. Verificar en un PR de prueba | Pendiente | Rama `ci/task-004-adaptar-workflow` pusheada a `origin`. Falta abrir el PR (no hay `gh` ni token disponible en este entorno) para que el trigger `pull_request` dispare el primer run real. |

## Bloqueos

| Qué bloquea | Quién lo desbloquea | Desde |
|-------------|---------------------|-------|
| Nadie ha abierto el PR de `ci/task-004-adaptar-workflow` todavía, así que el workflow nunca se ha ejecutado de verdad | El humano (abrir el PR manualmente o instalar `gh`) | 2026-08-09 |

---

## Al terminar

- [ ] Tests en verde — **no confirmado**, ver nota en "Progreso"
- [x] `docs/standards/DEFINITION_OF_DONE.md` revisado
- [ ] `.ai/TASKS.md` actualizado (tarea movida a *Hecho*) — sigue en "En progreso" a propósito, hasta confirmar el CI
- [x] `.ai/AI_MEMORY.md` actualizado (qué aprendiste)
- [x] `.ai/CHANGELOG.md` no actualizado (sin cambio visible para usuarios del sitio)
- [ ] PR abierto con la plantilla de `.github/PULL_REQUEST_TEMPLATE.md`
- [ ] **Este archivo reseteado** — no, sigue siendo la tarea activa hasta confirmar el CI en verde
