---
name: exploratory-testing
description: "Planifica, ejecuta y audita pruebas exploratorias: sesiones con objetivo (charters) y tiempo acotado, heurísticas para encontrar defectos (tours, CRUD, interrupciones, datos extremos, permisos, estados), notas de sesión, reportes de bug reproducibles (pasos, esperado y real, entorno, evidencia) y triage por severidad y prioridad. Un agente con navegador puede ejecutar la sesión sobre la aplicación. Úsala antes de un release, tras una funcionalidad nueva, cuando los tests pasan pero los usuarios encuentran fallos o para revisar la calidad de los reportes de bugs. No para diseñar casos automatizables (test-design) ni para crítica de diseño visual (frontend:ux-review)."
---

# Pruebas exploratorias

Los tests automatizados comprueban lo que alguien imaginó; las pruebas exploratorias encuentran **lo que nadie imaginó**: combinaciones raras, flujos interrumpidos, datos extremos, la interfaz que confunde. No son "probar sin plan": son sesiones con un objetivo, un tiempo acotado y un registro de lo que se probó y se encontró.

## Cuándo usarla

- Antes de un release, sobre lo que cambió.
- Tras construir una funcionalidad, antes de darla por terminada.
- Los tests pasan, pero los usuarios siguen encontrando fallos.
- Áreas nuevas, poco conocidas o difíciles de automatizar.
- Revisar la calidad de los reportes de bugs del equipo.

**No es para:** diseñar casos sistemáticos para automatizar → `test-design` · evaluar jerarquía visual, densidad o coherencia del diseño → `frontend:ux-review` · seguir un fallo ya conocido entre capas → `fullstack:flow-diagnosis`.

## Paso 0: contexto (ambos modos)

1. **Qué se explora y por qué:** cambios del release, funcionalidad nueva o área con quejas; riesgos conocidos (de `test-strategy` si existe).
2. **Entorno y datos:** dónde se prueba (local, staging; **nunca producción con datos reales** sin autorización explícita), usuarios y roles de prueba, datos de partida.
3. **Herramientas:** con navegador (el del agente o el del usuario), la sesión se ejecuta sobre la app; sin él, la skill prepara los charters y el usuario los ejecuta.
4. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir (planificar y ejecutar)

1. **Charters:** 1–5 objetivos de sesión con el formato "Explorar <área> con <recursos/heurística> para descubrir <tipo de información>". Ver [patterns.md § Charters](references/patterns.md#charters).
2. **Heurísticas** por charter, elegidas por el riesgo. Ver [patterns.md § Heurísticas](references/patterns.md#heurísticas).
3. **Ejecuta** cada sesión con tiempo acotado (30–90 min de trabajo humano; para un agente, un número de interacciones acordado), tomando notas: qué se probó, qué se encontró, qué preguntas surgieron. Antes de acciones con efectos reales (enviar emails, pagos, borrar datos) en un entorno compartido, confirma con el usuario.
4. **Reporta los bugs** con [patterns.md § Reporte de bug](references/patterns.md#reporte-de-bug): reproducible, con evidencia.
5. **Cierra la sesión** con el informe de [patterns.md § Informe de sesión](references/patterns.md#informe-de-sesión): cobertura, bugs, preguntas y riesgos que merecen un test automatizado.
6. Entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir).

## Modo Auditar

1. Revisa cómo se explora hoy: ¿hay sesiones, charters, notas? ¿Se explora antes de los releases?
2. Revisa una muestra de reportes de bugs: reproducibilidad, evidencia, severidad y prioridad.
3. Revisa si los hallazgos exploratorios se convierten en tests automatizados cuando el riesgo lo merece.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-EXPL`. Los bugs encontrados en una sesión no son hallazgos de esta skill: van como reportes de bug, con su severidad.

## Principios

1. **Objetivo y tiempo acotado:** explorar sin charter es pasear.
2. **Pensar como el sistema puede fallar,** no como el usuario ideal.
3. **Todo bug reportado se puede reproducir** por otra persona sin preguntar.
4. **Las notas son el entregable,** tanto como los bugs: dicen qué se cubrió.
5. **Lo que se repite se automatiza;** la exploración busca lo nuevo.
6. **Entornos seguros:** nada de datos reales ni efectos irreversibles sin autorización.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Un bug cruza capas y no está claro dónde se rompe el dato | `fullstack:flow-diagnosis` | Reporte del bug y evidencia (petición, respuesta, pasos) |
| Un bug encontrado merece un test de regresión | `test-design` | Bug y regla que viola (casos para automatizar) |
| Problemas de contraste, foco o teclado durante la sesión | `frontend:accessibility` | Pantallas y pasos |
| Interfaz confusa, jerarquía o estados de carga y error mal resueltos | `frontend:ux-review` | Pantallas y observaciones |
| Desbordes o layouts rotos en ciertos tamaños | `frontend:responsive-layout` | Pantallas y viewports |
| Acceso a datos o acciones de otro usuario o rol | `backend:authorization` | Pasos y endpoint observado |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: charters, heurísticas, notas, reporte de bug, informe de sesión y triage. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `test-strategy`: decide qué áreas se exploran y cuáles se automatizan.
- `test-design`: convierte los hallazgos repetibles en casos.
- `frontend:ux-review`: crítica de diseño, complementaria a la exploración funcional.
