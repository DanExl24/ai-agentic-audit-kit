---
name: audit
description: "Orquesta una auditoría de la calidad y las pruebas de un proyecto combinando las skills del plugin qa (y, si están instalados, frontend:testing y backend:testing). Hace el triage del objetivo, elige una ruta (madurez integral, pre-release, regresiones, pipeline e intermitencia, resiliencia en ejecución, cimientos), declara qué áreas aplican al contexto, aplica cada skill en modo Auditar, deduplica hallazgos y entrega una puntuación de madurez de QA de 0 a 100 por pilares con nivel, un dictamen único y un plan de remediación por lotes. Úsala para saber cómo está la calidad de un proyecto, si un release está listo o cuando no está claro qué skill de QA aplicar. No la uses si ya sabes qué área revisar."
---

# Auditoría orquestada de QA

Esta skill no audita por sí misma: **decide qué skills de calidad aplicar, en qué orden y sobre qué alcance, y convierte sus resultados en un único dictamen** con una puntuación de madurez por pilares. Es la puerta de entrada cuando la pregunta es amplia ("¿cómo estamos de pruebas?", "¿podemos publicar?", "se nos escapan bugs").

## Cuándo usarla

- Conocer la madurez de QA de un proyecto y tener una línea base para comparar.
- Decidir si un release está listo.
- Síntoma difuso: bugs que vuelven, pipeline lento o ignorado, miedo a desplegar.

**No es para:** un área concreta y conocida → la skill directamente (`/qa:e2e`, `/qa:quality-gates`…) · la calidad del código de producción del frontend o del backend → `frontend:audit`, `backend:audit` · auditar la aplicación completa entre capas → `fullstack:audit`.

## Paso 0: triage

1. **Alcance:** repositorio, módulos o release; entornos accesibles (local, staging) y acceso al historial de CI o al gestor de issues.
2. **Objetivo:** madurez integral, release, regresiones, pipeline o resiliencia.
3. **Contexto:** tipo de producto (expuesto a Internet o red privada, con dinero o datos personales), equipo (una persona o varios), frecuencia de publicación, capas presentes (frontend, backend) y herramientas de test detectadas.
4. **Aplicabilidad:** declara qué áreas **no aplican** y por qué (p. ej. `dast` en una herramienta local sin exposición, `load-testing` en una app de un solo usuario). Un área que no aplica no se puntúa ni penaliza; una que aplica y no existe, sí (ver [report-template.md § Rúbrica](references/report-template.md#rúbrica-de-madurez)).
5. **Ruta:** elige una de [routes.md](references/routes.md) y explica en una línea por qué.
6. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Paso 1: elegir modo y confirmar el coste

Cada skill cargada son del orden de 3.000–4.500 tokens (SKILL.md, checklist y nota de herramienta), más la lectura del código, la configuración de CI y el historial. **Antes de empezar, presenta la ruta, las áreas que no aplican y estos modos con las skills concretas de cada uno, y espera la elección:**

| Modo | Qué incluye | Skills | Coste orientativo |
| :--- | :--- | :---: | :--- |
| **Completa** | Todas las áreas aplicables de la ruta, checklists completos, madurez por pilares y global | las de la ruta (hasta 10, incluidas `frontend:testing` y `backend:testing`) | Alto |
| **Enfocada** (por defecto) | Las 4–5 áreas de mayor riesgo para el contexto | 4–5 | Medio |
| **Rápida** | Las 2–3 más críticas, solo puntos CRITICAL/HIGH, sin nota global | 2–3 | Bajo |

- `frontend:testing` y `backend:testing` son de otros plugins: entran en el modo Completa (o si el usuario las pide) y cuentan en el coste. Si el plugin no está instalado, el área queda como pendiente y su pilar se puntúa con lo evaluado, declarándolo.
- **No preguntes** si el usuario ya fijó el alcance o la ejecución no es interactiva: aplica lo pedido (o el modo enfocado) y decláralo.
- Tras la confirmación, no vuelvas a preguntar entre una skill y otra.

## Modo Auditar (por defecto)

1. **Carga las skills del modo elegido:** de cada una, `SKILL.md`, `references/checklist.md` y la nota de la herramienta detectada (`playwright.md`, `github-actions.md`, `k6.md`…). Con herramienta de skills, `qa:<skill>`; si no, lee los archivos (`../<skill>/…`). Completos, no fragmentos. Registra lo cargado en el anexo con la [regla de veracidad](../../standards/output-formats.md#veracidad-de-lo-cargado-todas-las-entregas). Un área cuyo checklist no se cargó no se puntúa.
2. **Inventaria una sola vez:** suites y número de tests por capa, configuración de CI, scripts de carga y DAST, documentación de pruebas, historial reciente de correcciones (`git log`). Ejecuta las comprobaciones baratas y sin efectos externos (la suite de tests, el typecheck). **No ejecutes pruebas de carga ni escaneos DAST** salvo que el usuario lo autorice expresamente; se audita su configuración.
3. **Aplica cada checklist** sobre ese inventario.
4. **Control de calidad:** hallazgos sin evidencia, severidad o corrección se rehacen o se descartan; lo no inspeccionable va a "Por verificar".
5. **Consolida** con [report-template.md](references/report-template.md):
   - **Deduplica:** el mismo hueco visto por varias skills es un hallazgo, en el área de su causa raíz. Asignaciones fijas:
     - "El frontend (o una capa) no se verifica en CI" → `quality-gates` (no en `test-strategy`).
     - "Correcciones de defectos sin test de no regresión" → `defect-analysis` (el proceso); `test-design` solo aporta los casos en la corrección.
     - "Capa sin tests" → `frontend:testing` o `backend:testing` si se evaluaron; si no, `test-strategy`.
   - **Métricas con fundamento:** un hallazgo basado en una métrica (tasa de escape, de regresión, cobertura) exige que la métrica se pueda calcular con las fuentes disponibles; si no, no hay hallazgo, solo el límite declarado.
   - Ordena por severidad y, a igual severidad, por esfuerzo.
   - Puntúa con la [rúbrica de madurez](references/report-template.md#rúbrica-de-madurez) y aplica los [requisitos por nivel](references/report-template.md#requisitos-mínimos-por-nivel): marca los pilares parciales y, si los hay, presenta global y nivel como provisionales.
6. **Entrega** en el chat y, si es largo o se pide, en `audit-qa-<fecha>.md`. **Actualiza `.sdlc/context.md`** según [context.md](../../standards/context.md): "no toques el código" no impide escribirlo; si el usuario prohibió escribir archivos, incluye el bloque "Contexto propuesto".

## Modo Remediar

1. Agrupa los hallazgos en **lotes** por prioridad y skill (primero CRITICAL/HIGH).
2. Aplica cada lote con la skill correspondiente en modo **Construir**.
3. Tras cada lote, ejecuta la suite y el pipeline local que exista; informa de lo hecho y de lo no verificado.
4. Pruebas de carga, escaneos DAST, instalaciones a nivel de sistema y cambios en la protección de ramas se presentan para aprobación antes de hacerlos.
5. Al terminar, actualiza la puntuación.

## Principios

1. **Aplicabilidad antes que puntuación:** no se penaliza lo que el contexto no necesita, y se dice qué se excluyó.
2. **Ruta justificada;** cada skill aplicada tiene un motivo.
3. **Un problema, un hallazgo,** en su causa raíz.
4. **Evidencia o nada:** archivo y líneas, ejecución, configuración o commit.
5. **Leer antes que ejecutar:** la auditoría no lanza carga ni ataques sin autorización.
6. **La madurez orienta;** se compara solo con auditorías hechas con la misma rúbrica.
7. **Coste a la vista** antes de una auditoría extensa.

## Handoffs

Como orquestador, no dispara handoffs por separado ([handoffs.md](../../standards/handoffs.md) regla 6): las skills se planifican en el Paso 1 y los disparadores de las aplicadas se consolidan como escalado sugerido. Además:

| Disparador (observable) | Destino | Alcance y contexto |
| :--- | :--- | :--- |
| Los hallazgos apuntan a defectos en el código de producción (seguridad, contratos, lógica) | Escalado sugerido (`frontend:audit`, `backend:audit` o la skill concreta) | Hallazgo y evidencia |
| Un riesgo necesita las dos capas para existir | `fullstack:contracts` o `fullstack:audit` | Se propone con su coste |
| La remediación pide construir una suite o una funcionalidad completa | La skill en modo Construir o `fullstack:feature` | Se propone con su coste |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [routes.md](references/routes.md) | Siempre: rutas, pilares y escalado. |
| [report-template.md](references/report-template.md) | Al consolidar: rúbrica de madurez y plantilla del dictamen. |

## Skills que orquesta

`test-strategy` · `test-design` · `exploratory-testing` · `e2e` · `quality-gates` · `load-testing` · `dast` · `defect-analysis` · y, de otros plugins, `frontend:testing` · `backend:testing`
