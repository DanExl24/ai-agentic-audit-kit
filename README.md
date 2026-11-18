# 🛡️ AI Agentic Audit Kit → SDLC Skills

> **Repositorio de skills por dominio para todo el ciclo de vida del software: diseñar, construir, auditar y operar.**

El kit nació como un conjunto de prompts de auditoría (patrón *Hub & Spoke*: especialistas verticales + integrador fullstack). Ahora se está migrando a **skills de Claude Code** empaquetadas como **un plugin por dominio** dentro de un marketplace. Cada skill sirve tanto para construir como para auditar, y es agnóstica de framework, con notas específicas por stack.

---

## 🧭 Estado de la migración

| Dominio | Formato | Estado |
| :--- | :--- | :--- |
| **Frontend** | Plugin `plugins/frontend/` | 🟡 Olas 1 y 2 completadas: 9 skills (`ux-review`, `architecture`, `typescript`, `data-fetching`, `state-management`, `forms`, `design-system`, `accessibility`, `responsive-layout`). Solo el director sigue en `domains/01_frontend/`. Pendientes: olas 3 y 4 (skills nuevas y orquestador). |
| Fullstack integrator | Prompts en `domains/00_fullstack_integrator/` | ⏳ Pendiente |
| Backend | Prompts en `domains/02_backend/` | ⏳ Pendiente |
| Database | Prompts en `domains/03_database/` | ⏳ Pendiente |
| Security | Prompts en `domains/04_security/` | ⏳ Pendiente |
| QA & Testing | Prompts en `domains/05_qa_testing_engineering/` | ⏳ Pendiente |

Catálogo y hoja de ruta del frontend: [`plugins/frontend/README.md`](plugins/frontend/README.md).

---

## 🗂️ Estructura

```text
ai-agentic-audit-kit/
├── .claude-plugin/
│   └── marketplace.json          # marketplace "sdlc-skills": lista los plugins por dominio
│
├── plugins/                      # ✅ NUEVO FORMATO: un plugin por dominio
│   └── frontend/
│       ├── .claude-plugin/plugin.json
│       ├── standards/            # severidad, formato de informes y matriz de viewports
│       └── skills/
│           ├── ux-review/
│           ├── architecture/
│           ├── typescript/
│           ├── data-fetching/
│           ├── state-management/
│           ├── forms/
│           ├── design-system/
│           ├── accessibility/
│           └── responsive-layout/
│
├── domains/                      # ⏳ FORMATO ANTIGUO: prompts pendientes de migrar
│   ├── 00_fullstack_integrator/
│   ├── 01_frontend/              # solo el director (orquesta las skills del plugin)
│   ├── 02_backend/
│   ├── 03_database/
│   ├── 04_security/
│   └── 05_qa_testing_engineering/
│
├── protocols/                    # protocolo de interoperabilidad del formato antiguo
├── templates/                    # plantillas de informes del formato antiguo
└── guides/                       # guía de invocación y matriz de severidad
```

---

## ⚡ Uso

### Skills (formato nuevo)

Desde Claude Code:

```bash
/plugin marketplace add <ruta-local-o-repo-github-de-este-kit>
/plugin install frontend@sdlc-skills
```

Después:

```text
/frontend:architecture propón una estructura por features para src/
/frontend:forms audita los formularios de src/features/checkout
```

Las skills también se activan automáticamente cuando la petición encaja con su descripción.

### Prompts (formato antiguo, dominios pendientes)

1. Entra a la carpeta del agente (ej. `domains/02_backend/api_rest_gateway/`).
2. Abre `ONE_SHOT_PROMPT.md`, copia el prompt y reemplaza la ruta del archivo o módulo.
3. El agente devuelve un informe de hallazgos con severidad y corrección.

Guía detallada de cada agente y skill: [`guides/HOW_TO_INVOKE.md`](guides/HOW_TO_INVOKE.md).

---

## ⚖️ Licencia
MIT License.
