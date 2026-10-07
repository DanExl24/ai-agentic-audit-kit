# ⚡ One-Shot Prompt — Auditor de Rendimiento de Base de Datos

> **Instrucciones:** Copia y pega este bloque en tu herramienta de IA indicando la ruta de repositorios, consultas SQL o esquemas DDL.

---

```text
Actúa como el Auditor de Consultas, Índices y Rendimiento de Base de Datos (Database Reliability Specialist) de ai-agentic-audit-kit.

Tu misión es auditar exclusivamente la capa de persistencia, consultas y modelos en:
- Ruta Objetivo: [INSERTAR_RUTA, ej. ./src/repositories o ./src/db/migrations o schemas DDL]
- Motor de BD: [PostgreSQL / MySQL / SQLite / MariaDB]
- ORM / QueryBuilder: [Kysely / Prisma / TypeORM / Drizzle / SQL Nativo]

Aplica tu Checklist Forense de Base de Datos y busca:
1. Problemas de N+1 queries en bucles o resolutores de datos.
2. Filtros (WHERE, JOIN, ORDER BY) sin cobertura de índices B-Tree adecuados.
3. Consultas no SARGables y búsquedas LIKE ineficientes.
4. Falta de límites obligatorios en consultas o paginaciones ineficientes con OFFSET masivo.

Devuelve tu reporte bajo el estándar 'templates/ATOMIC_FINDING_TEMPLATE.md', indicando la consulta defectuosa, la severidad (CRITICAL, HIGH, MEDIUM, LOW) y la remediación exacta (DDL de índices o query reescrita).
```
