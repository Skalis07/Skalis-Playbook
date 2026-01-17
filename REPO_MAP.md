# 🗺️ REPO_MAP — Skalis Playbook

Este documento describe **qué contiene el repositorio** y **para qué sirve cada archivo/carpeta**.

> Nota: el README es intencionalmente breve y solo explica **cómo usar el repo**.
> Este archivo es la **fuente de verdad** para el detalle.

---

## 📌 Archivos raíz

### `README.md`

Entrada rápida al repositorio: qué es, cómo empezar y links a los documentos principales.

---

### `CREAR-PROYECTO.md`

**Bootstrapper de proyecto** (prompt/guía previa al manager).

Sirve para:

- definir objetivo, alcance y supuestos si falta info
- decidir **stack recomendado por capas** (frontend/backend/db/infra)
- proponer **alternativas con tradeoffs**
- definir **tooling mínimo profesional**
- dejar listo un **primer hito baseline** para ejecutar con el Manager

Relación:

- `CREAR-PROYECTO.md` = **decidir stack + tooling + setup**
- `MANAGER.md` = **ejecutar por fases/hitos con QA**

---

### `MANAGER.md`

Framework operativo (“todo terreno”) para ejecutar proyectos con estándar profesional.

Incluye:

- roadmap por **Fases → Hitos**
- formato fijo por hito (objetivo, entregables, DoD, riesgos/rollback)
- QA manual con **Golden Paths**
- sizing **S/M/L**
- apéndices opcionales (GitHub/PR, CI/CD, QA automatizado, Docker, Deploy, Observabilidad, etc.)

---

### `REPO_MAP.md`

Mapa del repositorio (este archivo). Explica **estructura**, **propósito** y **uso**.

---

## 📂 Carpetas

### `prompts/`

Prompts reutilizables para acelerar trabajo con IA.

#### `prompts/code/`

Prompts orientados a tareas sobre código.

##### `prompts/code/comentar-codigo-didactico.md`

Prompt para que un asistente comente código con enfoque:

- didáctico, profundo y realista
- sin cambiar lógica, formato o comentarios existentes
- priorizando el “por qué” y el contexto real

---

## ✅ Convenciones / intención del repo

- Archivos .md = piezas reutilizables de tu “sistema operativo” de ingeniería
- El repo está pensado para crecer con:
  - `templates/` (plantillas de proyectos)
  - `qa/` o `docs/qa/` (golden paths/checklists)
  - más prompts por dominio (debug, review, arquitectura, etc.)

---

> Fin del mapa del repositorio.
