---
name: domain-modeling
description: "Construye y audita el modelo del dominio desde el punto de vista del negocio: glosario y lenguaje común (un término, un significado), modelo conceptual de entidades, atributos clave y relaciones en Mermaid, ciclo de vida y estados de las entidades principales, eventos del dominio, módulos o contextos con sus fronteras, y catálogo de reglas de negocio (RN) atómicas, verificables, con tipo, motivo, origen, ejemplos, excepciones y enlaces a historias y código. Úsala al empezar un producto o módulo, cuando el equipo usa las mismas palabras para cosas distintas o para documentar las reglas de un sistema existente. No para diseñar el esquema de la base de datos (backend:schema-and-migrations) ni para implementar las reglas (backend:domain-logic)."
---

# Modelo del dominio

Cada malentendido entre negocio y desarrollo suele empezar en una palabra: "cliente", "pedido cerrado", "usuario activo". Esta skill fija el **lenguaje común** del producto, dibuja qué cosas existen y cómo se relacionan, y escribe las **reglas de negocio** de forma que cualquiera, persona o test, pueda comprobar si se cumplen.

## Cuándo usarla

- Al empezar un producto o un módulo, después de `discovery` y `elicitation`.
- Se usan las mismas palabras con significados distintos (o palabras distintas para lo mismo).
- Hay que documentar las reglas de negocio de un sistema existente.
- Revisar un glosario, un modelo conceptual o un catálogo de reglas.

**No es para:** tablas, tipos de columna, índices y migraciones → `backend:schema-and-migrations` · implementar reglas, casos de uso y máquinas de estado en el código → `backend:domain-logic` · estructura de módulos del código → `backend:architecture`, `frontend:architecture` · historias y criterios de aceptación → `user-stories`.

## Paso 0: contexto (ambos modos)

1. **Material de partida:** brief (`discovery`), notas y requisitos candidatos (`elicitation`), documentación funcional, código existente.
2. **Alcance:** todo el producto o un módulo; si hay módulos, sus prefijos de ID.
3. **Convención de IDs y ubicación** del proyecto o la de [ids-and-links.md](../../standards/ids-and-links.md). Si ya hay reglas numeradas, se continúa su numeración.
4. **Datos de negocio:** no se inventan reglas, límites ni importes ([output-formats.md § Datos de negocio](../../standards/output-formats.md#datos-de-negocio-preguntar-no-inventar)); lo inferido del código se marca.
5. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Glosario:** término, definición, sinónimos prohibidos, ejemplo y contraejemplo. Ver [patterns.md § Glosario](references/patterns.md#glosario).
2. **Modelo conceptual** en Mermaid: entidades, atributos que importan al negocio y relaciones con cardinalidad. Ver [patterns.md § Modelo conceptual](references/patterns.md#modelo-conceptual).
3. **Ciclo de vida** de las entidades con estados: estados, transiciones, quién las provoca y qué las impide. Ver [patterns.md § Ciclo de vida](references/patterns.md#ciclo-de-vida-y-estados).
4. **Eventos del dominio** y **módulos o contextos** si el producto tiene varias áreas. Ver [patterns.md § Eventos y módulos](references/patterns.md#eventos-y-módulos).
5. **Reglas de negocio** (`RN`): atómicas, verificables, con tipo, motivo, origen, ejemplos y excepciones. Contrasta cada condición y efecto con las decisiones y preguntas abiertas. Mantén como borrador lo que dependa de un supuesto, incluso en diagramas y eventos. Para cada cambio de política, distingue activación inicial, cambios posteriores, desactivación y reactivación cuando apliquen. Comprueba qué pasa con los datos de cada etapa y con las excepciones elegidas por el usuario. Para un borrado, confirma el alcance sobre las copias conocidas. Registra las dudas como pendientes. Ver [patterns.md § Reglas](references/patterns.md#reglas-de-negocio) y [rule-template.md](references/rule-template.md).
6. **Enlaces:** cada regla a sus entidades, historias (cuando existan) y, si está implementada, al código (archivo y símbolo).
7. Entrega en `docs/product/domain/` (o la estructura del proyecto) según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir).

## Modo Auditar

1. Localiza glosario, modelos y reglas (`docs/`, documentación por módulo, comentarios de dominio).
2. Comprueba consistencia del vocabulario entre documentos, interfaz y código (nombres de entidades y estados).
3. Revisa la calidad de cada regla (atómica, verificable, con motivo y origen) y contrástala con su implementación si existe.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `PR-DOMAIN`.
6. Antes de entregar, guarda y verifica los hallazgos abiertos y el registro de la auditoría en el contexto según [context.md](../../standards/context.md), también si el usuario pidió «no toques el código». Si otra área queda fuera del alcance, indica qué comprobación quedó pendiente.

## Principios

1. **Un término, un significado,** en documentos, interfaz y código.
2. **El modelo es del negocio,** no de la base de datos: entidades y relaciones que un usuario reconoce.
3. **Reglas atómicas y verificables:** una regla, una condición, un resultado, con ejemplos.
4. **Cada regla tiene motivo y origen;** si no, es un supuesto.
5. **Las excepciones son reglas,** no notas al pie.
6. **El código dice qué pasa hoy;** el negocio decide qué debería pasar.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

Registra las correcciones propias de modelado como hallazgos abiertos. Si una corrección necesita un ID nuevo, asígnalo al aplicarla tras revisar la numeración vigente.

Antes de entregar un handoff de implementación, contrasta sus IDs con el estado del catálogo. Registra los borradores y el `PRE` o `SUP` que bloquea cada uno fuera del alcance ejecutable, tanto en la entrega como en el contexto compartido.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Reglas acordadas que el código no implementa o implementa distinto | `backend:domain-logic` | `RN`, código actual (archivo y símbolo) y discrepancia |
| El modelo conceptual introduce entidades, relaciones o estados nuevos que deben persistirse | `backend:schema-and-migrations` | Entidades, cardinalidades y restricciones |
| Los nombres del modelo difieren de los del contrato o de los tipos compartidos | `fullstack:contracts` | Término del glosario y nombres en el código |
| Reglas con límites, combinaciones o estados que necesitan casos de prueba | `qa:test-design` | `RN` con ejemplos y excepciones |
| Las reglas están listas para repartirse en historias | `user-stories` | Catálogo de `RN` y entidades |
| Reglas sin historia o historias que citan reglas inexistentes | `traceability` | IDs afectados |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [ids-and-links.md](../../standards/ids-and-links.md), [output-formats.md](../../standards/output-formats.md), [context.md](../../standards/context.md), [handoffs.md](../../standards/handoffs.md) | Ambos modos. Reutiliza la lectura si sigue vigente en esta conversación. |
| [patterns.md](references/patterns.md) | Siempre: glosario, modelo, ciclo de vida, eventos, módulos y reglas. |
| [rule-template.md](references/rule-template.md) | Al escribir o reescribir reglas de negocio y el glosario. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `elicitation`: de donde salen términos y reglas candidatas.
- `user-stories`: reparte las reglas en historias y criterios.
- `backend:domain-logic` y `backend:schema-and-migrations`: llevan el modelo al código.
