# 🛡️ AI Agentic Audit Kit

> **Arsenal de Agentes Especialistas Verticales y Auditor Integrador Fullstack para cualquier Base de Código.**

Este repositorio implementa el patrón **Hub & Spoke Specialist Audit Pattern**: una arquitectura que combina **Especialistas Verticales de Láser Profundo** con un **Agente Integrador Fullstack**, permitiendo auditar, diagnosticar y refactorizar cualquier proyecto de software existente (sin importar su lenguaje o framework).

---

## 🏛️ Arquitectura Hub & Spoke (Especialistas + Árbitro)

```mermaid
flowchart TD
    subgraph "Spokes: Especialistas Verticales (Microscopio Forense)"
        UX["👁️ 01_frontend/ui_ux_experience<br/>Senior Design Critic (CERO CÓDIGO)"]
        F1["🏗️ 01_frontend/engineering/arch_and_network<br/>Arquitectura, Axios y Tipado TS"]
        F2["🧠 01_frontend/engineering/state_and_reactivity<br/>Stores, Reactividad y Memory Leaks"]
        F3["📝 01_frontend/engineering/forms_and_data_flow<br/>Validación Zod, UX y Double Submit"]
        F4["🎨 01_frontend/engineering/design_system_and_styling<br/>Tokens, Variantes, Temas y Layout"]
        F5["♿ 01_frontend/engineering/accessibility_and_wcag<br/>WCAG 2.1/2.2 AA, Teclado y ARIA"]
        F6["📱 01_frontend/engineering/responsive_layout_specialist<br/>13 Viewports, Tailwind/CSS (NO Rediseñar)"]
        B1["⚙️ 02_backend/api_rest_gateway<br/>Routes, Middlewares, Validation y HTTP Errors"]
        B2["🧩 02_backend/domain_business_logic<br/>Services, Transacciones ACID y DDD"]
        D1["🗄️ 03_database/query_performance_indexer<br/>N+1 Queries, B-Tree Indexes y DDL"]
        S1["🛡️ 04_security/owasp_threat_hunter<br/>IDOR, Inyecciones, JWT y Secrets"]
        QD["👑 05_qa/00_qa_director<br/>Director Rector de Calidad & Triage"]
        Q1["🧪 05_qa/01_testability_and_unit_audit<br/>Inversión de dependencias, TDD y Mocks"]
        Q2["🎭 05_qa/02_contract_and_e2e_audit<br/>Playwright getByRole, BVA y Zod Contracts"]
        Q3["⏱️ 05_qa/03_performance_load_audit<br/>k6 scripts, p95/p99 SLAs y Concurrencia"]
        Q4["🔍 05_qa/04_dast_security_zap_audit<br/>OWASP ZAP runtime, CSP y Rate-Limiting"]
        Q5["🧬 05_qa/05_root_cause_kaizen_audit<br/>Ishikawa 5 ramas, Pareto y Quick Wins"]
    end

    subgraph "Hub: Agente Integrador Fullstack (Telescopio Sistémico)"
        HUB["🧠 00_fullstack_integrator<br/>(Staff Cross-Layer Systems Architect)"]
    end

    subgraph "Entregables Finales"
        OUT1["📋 Reconciliación de Contratos API ↔ SPA"]
        OUT2["🏗️ Propuesta de Topología Limpia de Carpetas"]
        OUT3["🧪 Diagnóstico de Fallos y Trazabilidad E2E"]
        OUT4["📊 Scorecard de Madurez QA y Plan Kaizen"]
    end

    UX -.->|Atomic Finding| HUB
    F1 -.->|Atomic Finding| HUB
    F2 -.->|Atomic Finding| HUB
    F3 -.->|Atomic Finding| HUB
    F4 -.->|Atomic Finding| HUB
    F5 -.->|Atomic Finding| HUB
    F6 -.->|Atomic Finding| HUB
    B1 -.->|Atomic Finding| HUB
    B2 -.->|Atomic Finding| HUB
    D1 -.->|Atomic Finding| HUB
    S1 -.->|Atomic Finding| HUB
    QD -.->|QA Maturity Scorecard| HUB
    Q1 -.->|Atomic Finding| HUB
    Q2 -.->|Atomic Finding| HUB
    Q3 -.->|Atomic Finding| HUB
    Q4 -.->|Atomic Finding| HUB
    Q5 -.->|Atomic Finding| HUB

    HUB ==> OUT1
    HUB ==> OUT2
    HUB ==> OUT3
    HUB ==> OUT4

    style HUB fill:#003366,stroke:#38bdf8,color:#ffffff,stroke-width:2px
    style OUT1 fill:#064e3b,stroke:#34d399,color:#ffffff
    style OUT2 fill:#064e3b,stroke:#34d399,color:#ffffff
    style OUT3 fill:#064e3b,stroke:#34d399,color:#ffffff
    style OUT4 fill:#064e3b,stroke:#34d399,color:#ffffff
```

---

## 🗂️ Estructura del Repositorio

```text
ai-agentic-audit-kit/
│
├── domains/                            # 🎯 Agentes Auditores Organizados por Dominio
│   │
│   ├── 00_fullstack_integrator/        # 🧠 EL HUB / ÁRBITRO CROSS-LAYER
│   │   ├── SYSTEM_PROMPT.md            # Rol maestro de Staff Systems Integrator
│   │   ├── CONTRACT_RECONCILER.md      # Metodología de cruce de contratos API ↔ SPA
│   │   ├── TOPOLOGY_REFACTORER.md      # Metodología de refactorización de carpetas
│   │   └── ONE_SHOT_PROMPT.md          # Invocación directa sobre todo el repo
│   │
│   ├── 01_frontend/                    # 🎨 DOMINIO FRONTEND (Escuadrón Colaborativo)
│   │   ├── 00_frontend_director/       # 👑 Director Rector del Dominio (Enrutador y consolidación)
│   │   ├── protocols/                  # 🤝 Handoff Memo y Peer Rejection Protocol
│   │   │
│   │   ├── ui_ux_experience/           # 👁️ Subdominio: Experiencia & Crítica Visual (CERO CÓDIGO)
│   │   │   └── 01_senior_design_critic/# Usabilidad, 10 viewports, fatiga, Before vs After
│   │   │
│   │   └── engineering/                # ⚙️ Subdominio: Ingeniería y Código
│   │       ├── 01_arch_and_network/    # 🏗️ Arquitectura, modularización, Axios y TS
│   │       ├── 02_state_and_reactivity/# 🧠 Stores Pinia/Zustand, memory leaks y re-renders
│   │       ├── 03_forms_and_data_flow/ # 📝 Formularios, validación Zod, doble submit y UX
│   │       ├── 04_design_system_and_styling/ # 🎨 Design System, tokens, temas y variantes
│   │       ├── 05_accessibility_and_wcag/  # ♿ WCAG 2.1/2.2 AA, navegación teclado y ARIA
│   │       └── 06_responsive_layout_specialist/ # 📱 13 viewports, Tailwind/CSS, CERO rediseño
│   │
│   ├── 02_backend/                     # ⚙️ DOMINIO BACKEND
│   │   ├── api_rest_gateway/           # Middlewares, Zod schemas, rate limit, envelopes
│   │   └── domain_business_logic/      # Casos de uso, transacciones ACID, clean code
│   │
│   ├── 03_database/                    # 🗄️ DOMINIO PERSISTENCIA
│   │   └── query_performance_indexer/  # N+1 queries, planes de ejecución, índices B-Tree
│   │
│   ├── 04_security/                    # 🛡️ DOMINIO CIBERSEGURIDAD
│   │   └── owasp_threat_hunter/        # IDOR, OWASP Top 10, inyecciones, fuga de credenciales
│   │
│   └── 05_qa_testing_engineering/      # 🧪 DOMINIO QA & QUALITY ENGINEERING
│       ├── 00_qa_director/             # 👑 Director Rector del Dominio (Triage y Scorecard 0-100)
│       ├── 01_testability_and_unit_audit/ # Desacoplamiento, DI, TDD y tests deterministas
│       ├── 02_contract_and_e2e_audit/     # Suites Playwright/Cypress, getByRole, BVA
│       ├── 03_performance_load_audit/     # Pruebas de carga k6, p95/p99 SLAs y estrés
│       ├── 04_dast_security_zap_audit/    # DAST en runtime, cabeceras HTTP y rate-limits
│       └── 05_root_cause_kaizen_audit/    # Ishikawa 5 ramas, Pareto 80/20 y matriz Kaizen
│
├── protocols/                          # 🤝 Protocolos de Intercambio
│   └── AUDIT_INTEROP_PROTOCOL.md       # Estándar de entrega de hallazgos entre agentes
│
├── templates/                          # 📋 Plantillas de Dictámenes Forenses
│   ├── ATOMIC_FINDING_TEMPLATE.md      # Para hallazgos de especialistas individuales
│   ├── FULLSTACK_SYNTHESIS_REPORT.md   # Dictamen integral del Agente Fullstack
│   ├── QA_MATURITY_SCORECARD_TEMPLATE.md # Evaluación cuantitativa de madurez QA (0-100)
│   └── KAIZEN_ACTION_TEMPLATE.md       # Matriz de priorización de acciones correctivas
│
└── guides/                             # 🚀 Guías de Operación
    ├── HOW_TO_INVOKE.md                # Guía de uso en Cursor, Antigravity, Claude, etc.
    └── SEVERITY_STANDARDS.md           # Matriz de severidad (CRITICAL, HIGH, MEDIUM, LOW)
```

---

## ⚡ ¿Cómo se Usa?

### Modo 1: Diagnóstico Quirúrgico (Especialista Aislado)
Úsalo cuando tengas una duda puntual en una capa específica:
1. Entra a la carpeta del especialista (ej. `domains/01_frontend/state_and_reactivity/`).
2. Abre `ONE_SHOT_PROMPT.md`, copia el prompt y reemplaza la ruta del archivo o módulo.
3. El agente te devolverá un reporte atómico con la severidad y el fix de código exacto.

### Modo 2: Diagnóstico y Reestructuración Integral (Agente Fullstack)
Úsalo cuando un flujo falle de extremo a extremo, haya desorden de carpetas o sospeches desalineación entre frontend y backend:
1. Abre `domains/00_fullstack_integrator/ONE_SHOT_PROMPT.md`.
2. Proporciona la ruta del frontend y del backend (o los reportes atómicos de los especialistas).
3. El Agente Fullstack actuará como árbitro: detectará discrepancias de contrato, localizará la causa raíz y te entregará una propuesta visual de arquitectura y estructura de carpetas.

---

## ⚖️ Licencia
MIT License.
