# 🚀 Guía de Invocación Rápida de Agentes Auditores

Esta guía explica cómo ejecutar a los agentes de `ai-agentic-audit-kit` en cualquier entorno de trabajo de IA.

---

## 1. Modos de Uso según tu Herramienta de IA

### A. En Google Antigravity / Claude Code / Windsurf / Cursor
1. Abre tu proyecto objetivo en el editor.
2. Abre el archivo `ONE_SHOT_PROMPT.md` del auditor que deseas utilizar (o `SYSTEM_PROMPT.md`).
3. Copia el texto y reemplaza los parámetros:
   - `[TARGET_PATH]`: Ruta relativa o absoluta de la carpeta o archivo a auditar.
   - `[TARGET_FRAMEWORK]`: (Opcional) Ej. Vue 3, React, Express, FastAPI, Django, PostgreSQL.
4. Envía el prompt. El agente ejecutará la inspección forense y te devolverá el reporte estructurado.

---

### B. En ChatGPT / Claude Pro / Gemini Web (Sin acceso directo a terminal)
1. Copia el contenido de `SYSTEM_PROMPT.md` en las Instrucciones Personalizadas (Custom Instructions) o como primer mensaje.
2. Pega el archivo o fragmento de código que deseas auditar.
3. El agente responderá siguiendo la estructura forense y la escala de severidad.

---

## 2. Flujo Recomendado: Auditoría Quirúrgica vs Auditoría Integral

### Caso 1: Quieres auditar un problema puntual de UI o API
* Ejecuta directamente al especialista vertical correspondiente:
  - Frontend: `domains/01_frontend/state_and_reactivity/` o `ui_design_a11y/`
  - Backend: `domains/02_backend/api_rest_gateway/` o `domain_business_logic/`
  - Base de Datos: `domains/03_database/query_performance_indexer/`
  - Seguridad: `domains/04_security/owasp_threat_hunter/`

### Caso 2: El sistema falla entre frontend y backend, o el proyecto está desordenado
* Ejecuta al **Agente Integrador Fullstack**:
  - `domains/00_fullstack_integrator/ONE_SHOT_PROMPT.md`
  - Este agente analizará ambos lados, detectará discrepancias de contrato y te entregará una propuesta limpia de estructura de carpetas y arquitectura.
