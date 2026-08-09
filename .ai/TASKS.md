# TASKS.md — Backlog

> El backlog completo. `CURRENT_TASK.md` toma **una** tarea de aquí a la vez.
>
> Prioridad: `P0` bloquea todo · `P1` sprint actual · `P2` siguiente · `P3` algún día.

---

## 🔴 En progreso

| ID | Tarea | Prioridad | Agente | Rama |
|----|-------|-----------|--------|------|
| TASK-004 | Adaptar el CI de `.github/workflows/ci.yml` al stack | P1 | Claude Code | `ci/task-004-adaptar-workflow` |

---

## 📋 Listo para empezar

> Solo entran aquí las tareas que cumplen `docs/process/` → *Definition of Ready*:
> objetivo claro, criterios de aceptación escritos, sin dependencias abiertas.

| ID | Tarea | Prioridad | Estimación | Depende de |
|----|-------|-----------|------------|------------|
| | | | | |

---

## 🧊 Backlog

| ID | Tarea | Prioridad | Nota |
|----|-------|-----------|------|
| | | | |

---

## 🚧 Bloqueadas

| ID | Tarea | Qué la bloquea | Desde |
|----|-------|----------------|-------|
| | | | |

---

## ✅ Hecho

> Mueve aquí al cerrar. Incluye el PR para poder rastrearlo.

| ID | Tarea | Cerrada | PR |
|----|-------|---------|-----|
| TASK-003 | Dibujar la arquitectura en `.ai/ARCHITECTURE.md` | 2026-08-07 | [#2](https://github.com/stexc7/TEC-SOLUCIONES/pull/2) |
| TASK-002 | Definir el stack en `.ai/STACK.md` | 2026-08-06 | — |
| TASK-001 | Rellenar `.ai/PROJECT.md` con el proyecto real | 2026-08-06 | — |

---

## 💡 Detectado al paso

> Cosas que una IA vio mientras hacía otra cosa. **No se arreglan en el momento.**
> Se anotan aquí y se priorizan después.

| Qué | Dónde | Detectado por | Fecha |
|-----|-------|---------------|-------|
| No hay provider de cobertura instalado (`@vitest/coverage-v8` o similar) ni umbral definido en `.ai/TESTING.md`. El CI corre `npm test` sin `--coverage`. | `frontend/package.json`, `.ai/TESTING.md` | Claude Code | 2026-08-09 |
| `.ai/TESTING.md` sigue con la plantilla sin rellenar (comandos, herramientas y cobertura en blanco), pese a que Vitest ya está instalado y configurado. | `.ai/TESTING.md` | Claude Code | 2026-08-09 |
