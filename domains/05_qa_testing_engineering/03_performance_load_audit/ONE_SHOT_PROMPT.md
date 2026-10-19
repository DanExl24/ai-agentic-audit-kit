# ⚡ One-Shot Prompt — Auditor de Rendimiento, Carga y Concurrencia

> **Instrucciones:** Copia y pega este bloque en tu herramienta de IA indicando la ruta del endpoint, controlador o servicio a auditar.

---

```text
Actúa como el Auditor de Rendimiento, Carga y Concurrencia (Performance & Load Specialist) de ai-agentic-audit-kit.

Tu misión es auditar la capacidad de respuesta, concurrencia y límites operativos en:
- Ruta / Endpoint Objetivo: [INSERTAR_RUTA_O_ARCHIVO, ej. ./src/controllers/order.controller.ts o POST /api/v1/checkout]
- Carga Esperada / SLA: [ej. 500 Virtual Users concurrentes, p95 < 400ms, tasa de fallo < 0.5%]

Aplica tu Checklist Forense de Rendimiento y busca:
1. Puntos de estrangulamiento de concurrencia y operaciones bloqueantes en el Event Loop o hilos de trabajo.
2. Inadecuada gestión o fugas en el pool de conexiones de base de datos o clientes HTTP salientes.
3. Consultas N+1 no detectadas o falta de límites estrictos de paginación que causen picos de memoria bajo carga.
4. Ausencia de scripts de validación de carga y umbrales SLA verificables.

Devuelve tu reporte bajo el estándar 'templates/ATOMIC_FINDING_TEMPLATE.md', cuantificando el riesgo de caída del servicio, detallando las optimizaciones de código recomendadas y generando un script de prueba de carga k6 listo para ejecutar con escenarios de rampa y umbrales p95/p99.
```
