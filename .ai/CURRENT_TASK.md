# CURRENT_TASK.md — La tarea de ahora mismo

> **Solo una tarea a la vez.** Este archivo es el foco. Si tiene tres tareas, no
> tiene ninguna.
>
> Zoo Code lee este archivo como su instrucción principal.

---

## Tarea activa

**ID:** `TASK-002`
**Título:** Definir el stack en `.ai/STACK.md`
**Estado:** `terminada`
**Agente asignado:** `Zoo Code`
**Rama:** `docs/task-002-definir-stack`
**Iniciada:** `2026-08-06`

### Objetivo

Tener un stack tecnológico concreto elegido y documentado para TEC-SOLUCIONES, de forma que TASK-003 (arquitectura) y TASK-004 (CI) puedan apoyarse en él.

### Criterios de aceptación

- [x] `.ai/STACK.md` indica framework/generador de sitio, hosting y cómo se gestiona el formulario de contacto.
- [x] La elección es coherente con `PROJECT.md`: sitio informativo + catálogo, sin carrito ni backend complejo, lanzamiento rápido y económico.
- [x] Queda registrada la justificación (por qué ese stack y no otro) para poder anotarla en `DECISIONS.md` si tiene consecuencias relevantes.

### Archivos que se van a tocar

```
.ai/STACK.md
```

### Enfoque

1. Proponer un stack acorde a un sitio informativo/catálogo con formulario de contacto (p.ej. generador estático + hosting gratuito/económico).
2. Confirmar la elección con el humano.
3. Documentarlo en `.ai/STACK.md`.

### Fuera de alcance en esta tarea

- Implementar el sitio (eso es trabajo posterior a TASK-003/004).
- Definir la arquitectura detallada (TASK-003).

- 

---

## Progreso

> Actualiza esto mientras trabajas. Es lo que permite retomar tras una interrupción.

| Paso | Estado | Nota |
|------|--------|------|
| 1. Proponer y confirmar el stack con el humano | Hecho | Astro + TypeScript + CSS nativo, Cloudflare Pages y Formspree aprobados. |
| 2. Documentar el stack y la decisión | Hecho | Documentados en `.ai/STACK.md` y `.ai/DECISIONS.md`. |

## Bloqueos

| Qué bloquea | Quién lo desbloquea | Desde |
|-------------|---------------------|-------|
| | | |

---

## Al terminar

- [x] Tests en verde (no aplican: tarea exclusivamente documental)
- [x] `docs/standards/DEFINITION_OF_DONE.md` revisado para el alcance documental
- [ ] `.ai/TASKS.md` actualizado (tarea movida a *Hecho*)
- [ ] `.ai/AI_MEMORY.md` actualizado (qué aprendiste)
- [x] `.ai/CHANGELOG.md` no actualizado (no hay cambio visible para usuarios)
- [ ] PR abierto con la plantilla de `.github/PULL_REQUEST_TEMPLATE.md`
- [ ] **Este archivo reseteado** con la siguiente tarea de `TASKS.md`
