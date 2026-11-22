---
name: discovery
description: "Construye y audita el descubrimiento de producto, lo primero antes de crear software: problema y evidencia, usuarios y segmentos (trabajos por hacer y proto-personas como supuestos), propuesta de valor, Lean Canvas (o su versión para herramientas internas), supuestos de mayor riesgo con su plan de validación, alcance del MVP (dentro y fuera) y objetivos con métricas de éxito. Entrega un brief de producto con IDs OBJ y SUP. Úsala con una idea nueva, antes de un proyecto o una funcionalidad grande, o para revisar si un producto sabe qué problema resuelve y para quién. No para levantar requisitos detallados con los interesados (elicitation) ni para escribir historias (user-stories)."
---

# Descubrimiento de producto

Antes de decidir **cómo** construir hay que saber **qué problema se resuelve, para quién y cómo se sabrá que funcionó**. Esta skill convierte una idea en un brief con el problema, los usuarios, la propuesta de valor, lo que se está suponiendo y cómo comprobarlo, y el MVP más pequeño que responde a la pregunta más arriesgada.

## Cuándo usarla

- Una idea nueva de producto o de una funcionalidad grande.
- Antes de un proyecto, para alinear a quien lo pide y a quien lo construye.
- El producto existe pero nadie sabe decir qué problema resuelve ni cómo se mide el éxito.
- Revisar un brief, un canvas o un documento de visión existente.

**No es para:** entrevistar a interesados y levantar requisitos detallados → `elicitation` · definir términos, entidades y reglas → `domain-modeling` · escribir el backlog → `user-stories` · ordenar qué va primero → `prioritization` · estudios de mercado, planes financieros o de inversión (fuera del kit).

## Paso 0: contexto (ambos modos)

1. **Qué existe:** idea en una frase, documentos previos (visión, canvas, README, presentación), producto en marcha o no.
2. **Tipo de producto:** comercial (B2C, B2B), herramienta interna o proyecto personal. Cambia qué partes del canvas aplican (ver [patterns.md § Lean Canvas](references/patterns.md#lean-canvas)).
3. **Quién decide** y quién usará el producto; si el autor es el único usuario, se declara.
4. **Lo que el usuario sabe y lo que no:** los datos de negocio no se inventan ([output-formats.md § Datos de negocio](../../standards/output-formats.md#datos-de-negocio-preguntar-no-inventar)). Haz como mucho 3–5 preguntas que bloqueen; el resto se registra como `SUP` o `PRE`.
5. **IDs:** antes de asignar `OBJ`, `SUP`, `PRE` o `DEC`, busca sus definiciones en la documentación del proyecto, incluidas las notas de sesión, según [ids-and-links.md](../../standards/ids-and-links.md).
6. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Problema:** quién lo tiene, cuándo, cómo lo resuelve hoy y qué le cuesta, con la evidencia disponible. Ver [patterns.md § Problema](references/patterns.md#problema).
2. **Usuarios y segmentos:** trabajos por hacer y proto-personas, marcadas como supuestos hasta validarlas. Ver [patterns.md § Usuarios](references/patterns.md#usuarios-y-segmentos).
3. **Propuesta de valor:** qué cambia para el usuario y en qué se diferencia de su alternativa actual. Ver [patterns.md § Propuesta de valor](references/patterns.md#propuesta-de-valor).
4. **Lean Canvas** (o la versión interna). Ver [patterns.md § Lean Canvas](references/patterns.md#lean-canvas).
5. **Supuestos de mayor riesgo** (`SUP`): clasificados por importancia y evidencia, con un experimento y su criterio de éxito definido antes. Ver [patterns.md § Supuestos](references/patterns.md#supuestos-de-mayor-riesgo).
6. **Alcance del MVP:** lo mínimo que valida el supuesto más arriesgado. Lista qué entra y qué queda fuera, con su decisión de origen o estado de propuesta. Si al resolver una pregunta se amplía el MVP, presenta el nuevo alcance para confirmación. El brief sigue en `borrador` hasta que quien decide confirme el alcance completo. Ver [patterns.md § MVP](references/patterns.md#alcance-del-mvp).
7. **Objetivos y métricas** (`OBJ`): registra la fuente de cada línea base medida. Si falta, escribe `pendiente de medir` e indica cómo obtenerla. Identifica metas y umbrales como propuestos o acordados. Incluye plazo y métrica de control. Ver [patterns.md § Métricas](references/patterns.md#objetivos-y-métricas).
8. Entrega el brief con [brief-template.md](references/brief-template.md) en `docs/product/brief.md` (o donde el proyecto lo guarde) según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir).
9. **Antes de entregar o actualizar el brief**, verifica que cada encabezado de un supuesto, pregunta o decisión contiene solo su ID. Pon el estado y las referencias debajo. Comprueba que los enlaces al elemento siguen resolviendo al ancla del ID.

## Modo Auditar

1. Localiza el material de descubrimiento: brief, visión, canvas, README, presentaciones, `docs/`.
2. Comprueba que el problema tiene evidencia, que los segmentos son concretos, que los supuestos críticos tienen plan de validación y que los objetivos son medibles.
3. Contrasta el brief con el producto actual: ¿sigue describiendo lo que se construye?
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `PR-DISC`.
6. Antes de entregar, registra la auditoría en el contexto según [context.md](../../standards/context.md), también si el usuario pidió «no toques el código».

## Principios

1. **Problema antes que solución:** una funcionalidad sin problema asociado es una apuesta sin nombre.
2. **Supuestos explícitos:** lo que no se ha comprobado se escribe como supuesto, con cómo comprobarlo.
3. **Validar lo más arriesgado primero,** con el experimento más barato que dé una respuesta.
4. **El MVP es un experimento,** no la versión 1 recortada.
5. **Métricas de resultado, no de vanidad:** cambian decisiones si se mueven.
6. **No inventar datos de negocio:** se preguntan o se marcan como supuestos.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Supuestos críticos sobre usuarios o necesidades que solo se resuelven hablando con ellos | `elicitation` | `SUP` y `PRE` afectados, segmentos e interesados |
| Aparecen conceptos del negocio con nombres ambiguos o reglas que el MVP debe respetar | `domain-modeling` | Términos y reglas candidatas |
| El alcance del MVP está acordado y hay que convertirlo en backlog | `user-stories` | Brief, alcance dentro/fuera y `OBJ` |
| Hay que decidir el orden de varias apuestas o funcionalidades | `prioritization` | Opciones, `OBJ` y supuestos |
| El producto tratará datos personales, de salud, menores o pagos | `backend:data-privacy` | Datos previstos y finalidad |
| La validación necesita un prototipo de interfaz | `frontend:ux-review` | Flujo a prototipar y supuesto que valida |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: problema, usuarios, propuesta de valor, Lean Canvas, supuestos, MVP y métricas. |
| [brief-template.md](references/brief-template.md) | Modo Construir: plantilla del brief. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `elicitation`: valida los supuestos con los interesados.
- `domain-modeling`: fija el lenguaje del producto.
- `user-stories` y `prioritization`: del alcance al backlog ordenado.
