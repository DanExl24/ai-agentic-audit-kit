---
name: audit
description: Orquesta una auditoría completa o parcial del frontend combinando las skills del plugin frontend. Hace el triage del objetivo, elige una ruta (integral, UX, rendimiento, formularios, visual y accesible, responsive, cimientos técnicos, seguridad, pre-release), aplica cada skill en modo Auditar, deduplica hallazgos, calcula una puntuación por área y global (0–100) y entrega un dictamen único con plan de remediación priorizado; opcionalmente ejecuta la remediación por lotes. Úsala para revisar un módulo o una app de principio a fin, decidir si algo está listo para publicar o cuando no está claro qué skill aplicar. No la uses si ya sabes qué área revisar: invoca directamente esa skill.
---

# Auditoría orquestada del frontend

Esta skill no audita líneas de código por sí misma: **decide qué skills aplicar, en qué orden y sobre qué alcance, y convierte sus resultados en un único dictamen** con prioridades claras. Es la puerta de entrada cuando la pregunta es amplia ("¿cómo está este módulo?", "¿está listo para publicar?") o cuando no está claro qué área falla.

## Cuándo usarla

- Revisar un módulo, feature o aplicación completa (diseño + ingeniería).
- Decidir si un release está listo (sí/no por bloque, con riesgos abiertos).
- El síntoma es difuso y no se sabe qué skill aplicar.
- Obtener una línea base con puntuación para comparar en el tiempo.

**No es para:** revisiones de un área concreta y conocida → invoca la skill directamente (`/frontend:forms`, `/frontend:accessibility`…) · backend, base de datos o integración entre capas → otros dominios del kit (ver [routes.md § Escalado](references/routes.md#escalado-a-otros-dominios)).

## Paso 0: triage

1. **Alcance:** rutas o módulos (`src/features/checkout`, toda `src/`), URL de la app si está en ejecución, entorno.
2. **Objetivo:** auditoría completa, una preocupación concreta, o control previo a un release.
3. **Contexto:** stack (lee `package.json`), tipo de app (pública indexable, panel privado, mixta), usuarios (uso intensivo, ocasional, móvil), requisitos (legales de accesibilidad, rendimiento, multi-idioma).
4. **Ruta:** elige una de [routes.md](references/routes.md) y **explica en una línea por qué**. Si el objetivo no encaja con ninguna, compón una secuencia de skills y justifícala.

Si el alcance es muy grande (toda una app con decenas de features), propón empezar por los flujos críticos y amplía después.

## Modo Auditar (por defecto)

1. **Aplica cada skill de la ruta en modo Auditar** sobre el mismo alcance. Para cargar una skill: usa la herramienta de skills con `frontend:<skill>` si está disponible; si no, lee `../<skill>/SKILL.md` y las referencias que indique. Aplica su checklist completo; no te quedes en lo superficial.
2. **Paralelización opcional:** si el alcance es grande y el entorno permite subagentes, y el usuario está de acuerdo, delega cada área en un subagente con el mismo alcance y pídele el informe en el formato de [output-formats.md](../../standards/output-formats.md). Revisa que cada informe cite archivo y líneas antes de consolidarlo.
3. **Control de calidad** de cada resultado: sin archivo y líneas, sin severidad o sin corrección aplicable, ese hallazgo se rehace o se descarta.
4. **Consolida** según [report-template.md](references/report-template.md):
   - Deduplica: el mismo problema visto desde dos skills (contraste en `design-system` y en `accessibility`; token en `localStorage` en `data-fetching` y en `security`) es **un** hallazgo, con la corrección en su causa raíz y las skills implicadas.
   - Ordena por severidad ([severity.md](../../standards/severity.md)) y, a igual severidad, por esfuerzo (lo barato primero).
   - Puntúa por área y global con la [rúbrica](references/report-template.md#rúbrica-de-puntuación).
   - Escala lo que no es del frontend (autorización, contratos de API, rendimiento del backend).
5. **Entrega** el dictamen en el chat y, si es largo o el usuario lo pide, en `audit-frontend-<fecha>.md`.

## Modo Remediar

Cuando el usuario pide aplicar las correcciones tras la auditoría:

1. Agrupa los hallazgos en **lotes** por prioridad y área (primero CRITICAL/HIGH; dentro, por skill, para que cada lote sea coherente).
2. Para cada lote, aplica la skill correspondiente en modo **Construir** con los hallazgos como especificación.
3. Tras cada lote: type-check, lint, tests y, si aplica, verificación visual. Informa de lo hecho y de lo que no se pudo verificar antes de pasar al siguiente.
4. No mezcles cambios de diseño (`ux-review`) con correcciones técnicas sin que el usuario los haya aprobado.
5. Al terminar, actualiza la puntuación con los hallazgos resueltos.

## Principios

1. **Ruta justificada:** cada skill que se aplica tiene un motivo ligado al objetivo.
2. **Profundidad sobre amplitud:** mejor 6 áreas bien auditadas que 14 a medias. Si no da tiempo, dilo.
3. **Un problema, un hallazgo:** deduplicado y corregido en su causa raíz.
4. **Evidencia o nada:** cada hallazgo con archivo y líneas, o reproducible en la interfaz.
5. **La puntuación orienta, no sustituye:** acompaña cada nota con los hallazgos que la explican y compárala solo con auditorías hechas con la misma rúbrica.
6. **Lo que no es del frontend se escala**, con la evidencia reunida.
7. **Declara los límites:** qué no se pudo verificar (sin navegador, sin datos de campo, sin acceso al backend).

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [routes.md](references/routes.md) | Siempre: rutas, criterios de selección y escalado. |
| [report-template.md](references/report-template.md) | Al consolidar: plantilla del dictamen y rúbrica de puntuación. |

## Skills que orquesta

`ux-review` · `architecture` · `typescript` · `routing` · `data-fetching` · `state-management` · `forms` · `design-system` · `accessibility` · `responsive-layout` · `performance` · `rendering-and-seo` · `security` · `testing` · `observability` · `i18n` · `tooling`
