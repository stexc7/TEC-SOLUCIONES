# CURRENT_TASK.md — La tarea de ahora mismo

> **Solo una tarea a la vez.** Este archivo es el foco. Si tiene tres tareas, no
> tiene ninguna.
>
> Zoo Code lee este archivo como su instrucción principal.

---

## Tarea activa

**ID:** `TASK-004`
**Título:** Adaptar el CI de `.github/workflows/ci.yml` al stack
**Estado:** `pendiente`
**Agente asignado:** `—`
**Rama:** `—`
**Iniciada:** `—`

### Objetivo

Configurar `.github/workflows/ci.yml`, hoy un placeholder de plantilla, para que valide de verdad el stack real del proyecto (Astro + TypeScript + Vitest) en cada PR y en `main`.

### Criterios de aceptación

- [ ] `.github/workflows/ci.yml` descomenta/adapta el bloque Node.js de la plantilla (o lo reescribe) para instalar dependencias, ejecutar lint, comprobación de tipos, tests y build desde `frontend/`.
- [ ] Se elimina el job `placeholder` que solo emite el aviso de "CI no configurado".
- [ ] El pipeline completo corre en menos de 10 minutos.
- [ ] El flujo de despliegue descrito en `.ai/ARCHITECTURE.md` (PR → CI → Cloudflare Pages) queda respaldado por un CI real.

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
| 1. Confirmar que `frontend/` tiene `package.json` con scripts de lint/typecheck/test/build | Pendiente | — |
| 2. Adaptar `ci.yml` | Pendiente | — |
| 3. Verificar en un PR de prueba | Pendiente | — |

## Bloqueos

| Qué bloquea | Quién lo desbloquea | Desde |
|-------------|---------------------|-------|
| | | |

---

## Al terminar

- [ ] Tests en verde
- [ ] `docs/standards/DEFINITION_OF_DONE.md` revisado
- [ ] `.ai/TASKS.md` actualizado (tarea movida a *Hecho*)
- [ ] `.ai/AI_MEMORY.md` actualizado (qué aprendiste)
- [ ] `.ai/CHANGELOG.md` actualizado si el cambio es visible para usuarios
- [ ] PR abierto con la plantilla de `.github/PULL_REQUEST_TEMPLATE.md`
- [ ] **Este archivo reseteado** con la siguiente tarea de `TASKS.md`
