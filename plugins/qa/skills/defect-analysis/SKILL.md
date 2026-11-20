---
name: defect-analysis
description: "Analiza defectos escapados y regresiones para que no vuelvan: recopilación desde issues, historial de git y reportes; clasificación (tipo, fase de introducción, fase de detección, por qué escapó); hotspots y regresiones en el historial; causa raíz con 5 porqués y diagrama de Ishikawa en Mermaid (5 ramas: Métodos, Personas, Herramientas, Entorno, Código); Pareto 80/20; matriz de acciones Kaizen (Quick Win, Táctico, Estratégico, con dificultad, plazo, impacto y KPI); criterios de cierre (test de no regresión, 14 días sin recurrencia, lección incorporada al checklist o al CI) y métricas de escape, regresión y reapertura. Úsala cuando un bug corregido vuelve, cuando se escapan defectos a producción o tras un defecto grave. No para diagnosticar un fallo en curso entre capas (fullstack:flow-diagnosis) ni para incidentes de operación (disponibilidad, guardias, SLO)."
---

# Análisis de defectos escapados y regresiones

Corregir un bug arregla **ese** bug; analizarlo evita **la familia entera**. Esta skill parte de defectos que ya llegaron a donde no debían (producción, usuarios, un release) o que volvieron tras corregirse, encuentra por qué el proceso los dejó pasar y convierte la respuesta en acciones con dueño, plazo y una métrica que diga si funcionaron.

## Cuándo usarla

- "Este bug ya lo habíamos arreglado": regresiones.
- Se escapan defectos a producción con frecuencia, o uno grave acaba de escaparse.
- Revisión periódica (por release o trimestre) de los defectos encontrados.
- Auditar cómo gestiona el equipo los defectos y si aprende de ellos.

**No es para:** localizar un fallo que está ocurriendo ahora y no se sabe en qué capa → `fullstack:flow-diagnosis` · incidentes de operación (caídas, latencia, guardias, SLO y post-mortems de disponibilidad) → futuro dominio SRE · corregir el código → la skill de la capa (este análisis dice qué corregir y dónde) · decidir la cobertura de un release → `test-strategy`.

## Paso 0: fuentes y alcance (ambos modos)

1. **Defectos a analizar:** uno concreto (issue, commit, reporte) o un lote (periodo, release, módulo). Define qué cuenta como **escapado** en este proyecto (llegó a producción, a usuarios, a un release etiquetado).
2. **Fuentes:** gestor de issues (si hay acceso), historial de git (commits de corrección, reverts), post-mortems, reportes de usuarios, `.sdlc/context.md`. Cada dato del análisis sale de una fuente citada; **sin fuente, no hay dato** (ver [patterns.md § Datos](references/patterns.md#datos-y-veracidad)).
3. **Sin culpables:** se analizan procesos, herramientas e información, nunca personas. Los nombres de autores no aparecen en el informe.
4. **Privacidad:** sin datos personales de usuarios ni secretos en el análisis (reportes y logs se resumen).
5. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir (analizar)

1. **Recopila** los defectos con su evidencia (issue, commit de la corrección, fecha). Para un lote desde git, usa [patterns.md § Hotspots](references/patterns.md#hotspots-y-regresiones-en-el-historial) y confirma leyendo el commit que cada uno es de verdad una corrección.
2. **Clasifica** cada defecto: tipo, fase en que se introdujo, fase en que se detectó y **por qué escapó**. Ver [patterns.md § Clasificación](references/patterns.md#clasificación-de-defectos).
3. **Hotspots y regresiones:** archivos o módulos con más correcciones y defectos que volvieron. Una regresión se **comprueba en git** (el comportamiento funcionó antes); lo que nació con el fallo es un defecto de origen. Ver [patterns.md § Clasificación](references/patterns.md#clasificación-de-defectos).
4. **Causa raíz:** 5 porqués por defecto relevante y **diagrama de Ishikawa en Mermaid** con las 5 ramas. Ver [patterns.md § Causa raíz](references/patterns.md#causa-raíz-5-porqués) e [§ Ishikawa](references/patterns.md#diagrama-de-ishikawa).
5. **Pareto 80/20** de las causas (o de los motivos de escape) con sus frecuencias reales. Con menos de ~20 defectos, el Pareto es orientativo y se dice. Ver [patterns.md § Pareto](references/patterns.md#pareto-8020).
6. **Matriz de acciones Kaizen:** contramedidas contra las causas del grupo vital, clasificadas en Quick Win, Táctico o Estratégico, con dificultad, plazo, impacto y KPI. Ver [patterns.md § Matriz](references/patterns.md#matriz-de-acciones-kaizen).
7. **Criterios de cierre** por defecto o causa: test de no regresión que falla con el comportamiento antiguo, 14 días sin recurrencia tras desplegar la contramedida y lección incorporada al checklist o al CI. Ver [patterns.md § Cierre](references/patterns.md#criterios-de-cierre).
8. Entrega el análisis con [report-template.md](references/report-template.md) (en `docs/quality/defect-analysis-<fecha>.md` o donde el proyecto guarde su documentación) según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir).

## Modo Auditar (el proceso de defectos)

1. Revisa cómo se registran los defectos (pasos, severidad, origen) y si se distingue lo escapado.
2. Comprueba en el historial si las correcciones llevan **test de no regresión** y si hay regresiones repetidas.
3. Revisa si los defectos graves tienen análisis de causa raíz y si sus acciones se cumplen y se miden.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-DEFECT`.

## Principios

1. **Datos con fuente:** cada defecto, frecuencia y porcentaje se puede rastrear a un issue o commit. Un Pareto inventado es peor que ninguno, y una métrica que las fuentes no pueden medir sale "n.a.", no con un valor.
2. **Sin culpables:** "la persona se equivocó" no es una causa raíz; la pregunta es por qué el proceso lo permitió y no lo detectó.
3. **La causa del escape importa tanto como la del defecto:** por qué se introdujo y por qué nadie lo vio antes de producción.
4. **Pocas acciones, medibles:** atacar el grupo vital del Pareto, con KPI y plazo; "tener más cuidado" no es una acción.
5. **Cerrar es verificar:** test de no regresión, tiempo sin recurrencia y la lección dentro del proceso.
6. **El análisis vive:** se revisa en el siguiente ciclo si las acciones funcionaron.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Un defecto escapado no tiene test de no regresión | `test-design` | Defecto, regla violada y entrada que lo provoca |
| El test de no regresión pertenece a una capa concreta | `frontend:testing` · `backend:testing` | Casos de `test-design`, archivo y comportamiento antiguo |
| La causa del escape es un control ausente o saltable en el pipeline | `quality-gates` | Etapa, check que faltó y defectos que lo habrían detectado |
| Un área concentra defectos (hotspot) sin cobertura acorde a su riesgo | `test-strategy` | Hotspot, defectos y mapa de riesgos afectado |
| Las correcciones del hotspot son difíciles por acoplamiento o lógica dispersa | `backend:architecture` · `frontend:architecture` | Módulo, defectos y dependencias observadas |
| La causa raíz cruza capas (contrato divergente entre cliente y API) | `fullstack:contracts` | Defectos, endpoint y consumidor |
| No está claro en qué capa se origina un defecto recurrente | `fullstack:flow-diagnosis` | Reporte, pasos y evidencia |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: datos, clasificación, hotspots, 5 porqués, Ishikawa, Pareto, matriz Kaizen, cierre y métricas. |
| [report-template.md](references/report-template.md) | Modo Construir: plantilla del análisis. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `test-design`: convierte cada defecto en casos de no regresión.
- `quality-gates`: donde las lecciones se convierten en controles automáticos.
- `test-strategy`: actualiza el mapa de riesgos con lo aprendido.
- `exploratory-testing`: sesiones dirigidas a los hotspots.
