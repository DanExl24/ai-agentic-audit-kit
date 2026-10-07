# 🛡️ AI Agentic Audit Kit

> **Arsenal de Agentes Especialistas y Auditores Autónomos On-Demand para cualquier Base de Código.**

Este repositorio contiene un conjunto de **Agentes de IA Tácticos e Individuales** diseñados para auditar, diagnosticar, refactorizar y documentar proyectos de software existentes, **sin importar el framework, lenguaje o arquitectura que utilicen**.

A diferencia de una fábrica SDLC completa, estos agentes son **stateless, quirúrgicos y de ejecución inmediata**: los invocas con un prompt o instrucción sobre cualquier repositorio, archivo o Pull Request para obtener diagnósticos forenses de nivel Staff Engineer.

---

## 🗂️ Estructura del Repositorio

```text
ai-agentic-audit-kit/
├── README.md                           # Visión general y guía rápida de uso
├── .gitignore                          # Exclusiones de Git
│
├── auditors/                           # 🕵️ Catálogo de Agentes Auditores Especializados
│   ├── 01_security_owasp_auditor/      # Auditor de Seguridad, IDOR, Injection y Credenciales
│   ├── 02_db_performance_profiler/     # Optimizador de Consultas, Planes de Ejecución e Índices
│   ├── 03_tech_debt_refactorer/        # Caza-anti-patrones, Complejidad y Tipado Seguro
│   ├── 04_accessibility_ux_inspector/  # Auditor WCAG 2.1 AA, ARIA y Semántica Web
│   ├── 05_legacy_reverse_engineer/     # Extractor de Especificaciones y Arquitectura C4
│   └── 06_pr_gatekeeper_reviewer/      # Revisor implacable de Pull Requests y Breaking Changes
│
├── templates/                          # 📋 Plantillas de Reportes Forenses Estandarizados
│   ├── AUDIT_EXECUTIVE_REPORT.md       # Plantilla maestra de dictamen técnico
│   └── SECURITY_DISCLOSURE_REPORT.md   # Plantilla para hallazgos críticos de seguridad
│
└── guides/                             # 🚀 Guías de Invocación
    ├── HOW_TO_INVOKE.md                # Cómo ejecutar en Antigravity, Cursor, Claude, Windsurf
    └── AUDIT_SEVERITY_SCALE.md         # Escala canónica de severidad (CRITICAL, HIGH, MEDIUM, LOW)
```

---

## 🛠️ Modos de Invocación

Cada agente en `auditors/` cuenta con:
1. **`SYSTEM_PROMPT.md`**: Instrucciones maestras de sistema (para usar como Custom Instructions, System Prompt o perfil de agente).
2. **`CHECKLIST.md`**: Lista forense exhaustiva de verificación paso a paso.
3. **`COMMAND_PROMPT.md`**: Prompt rápido de un solo disparo listo para copiar y pegar indicando la ruta del objetivo.

---

## ⚖️ Licencia
MIT License.
