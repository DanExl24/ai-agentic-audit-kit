---
name: test-design
description: "Diseña y audita casos de prueba con técnicas sistemáticas: particiones de equivalencia, valores límite, tablas de decisión, transiciones de estado, combinaciones por pares (pairwise), casos negativos y de error, property-based testing y escenarios Gherkin bien escritos. Convierte criterios de aceptación y reglas de negocio en un conjunto mínimo de casos que detecta defectos reales. Úsala al definir los casos de una funcionalidad, al revisar si una suite solo cubre el camino feliz o al preparar casos para automatizar. No para decidir qué áreas probar (test-strategy) ni para implementar los tests en una capa (frontend:testing, backend:testing)."
---

# Diseño de casos de prueba

Escribir tests no es lo difícil: lo difícil es **elegir los casos que encuentran defectos**. Sin técnica, los casos se parecen al camino feliz con variaciones cosméticas y los fallos viven justo donde nadie mira: en el límite, en la combinación rara, en la transición prohibida. Las técnicas de esta skill producen el **conjunto mínimo de casos con máxima capacidad de detección**.

## Cuándo usarla

- Definir los casos de una funcionalidad a partir de sus criterios de aceptación.
- Reglas de negocio con condiciones (descuentos, permisos, validaciones, cálculos).
- Flujos con estados (pedidos, suscripciones, aprobaciones).
- Formularios o APIs con muchas combinaciones de entrada.
- Auditar si una suite solo prueba el camino feliz.

**No es para:** decidir qué áreas merecen pruebas → `test-strategy` · implementar los tests en el código → `frontend:testing`, `backend:testing` · explorar sin guion → `exploratory-testing`.

## Paso 0: contexto (ambos modos)

1. **Fuente de verdad:** criterios de aceptación, reglas de negocio, especificación de la API, código de validación y del dominio. Si las reglas no están escritas, extráelas del código y confírmalas con el usuario antes de diseñar.
2. **Entradas y salidas:** variables de entrada (con sus tipos y rangos), estados, configuraciones y resultados observables.
3. **Riesgo del área** (de `test-strategy` o del contexto): decide cuánta profundidad merece.
4. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Elige la técnica** según la forma del problema con [patterns.md § Elegir técnica](references/patterns.md#elegir-técnica).
2. **Diseña los casos** con la técnica: clases válidas e inválidas, límites a cada lado, reglas de la tabla, transiciones válidas y prohibidas, combinaciones por pares.
3. **Añade los negativos y errores** que la técnica no da por sí sola: entradas vacías, nulas, enormes, con caracteres especiales; fallos de dependencias; permisos.
4. **Reduce:** elimina casos que no aportan una clase, un límite o una regla nueva.
5. **Expresa los casos** en el formato que el equipo usa: tabla de casos, `test.each`/`parametrize`, escenarios Gherkin ([patterns.md § Gherkin](references/patterns.md#escenarios-gherkin)) o propiedades.
6. Si se automatizan, pasa los casos a la skill de la capa (`frontend:testing`, `backend:testing`) indicando el nivel.
7. Entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir).

## Modo Auditar

1. Reconstruye las reglas y las entradas del área.
2. Aplica la técnica que corresponde y compara los casos que **deberían** existir con los tests reales.
3. Marca lo que falta: límites, clases inválidas, reglas de la tabla sin caso, transiciones prohibidas sin probar.
4. Comprueba también la calidad de los casos existentes: aserciones que no verifican nada, casos duplicados.
5. Recorre [checklist.md](references/checklist.md).
6. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-DESIGN`.

## Principios

1. **Cada caso cubre algo nuevo:** una clase, un límite, una regla o una transición.
2. **Los defectos viven en los bordes:** límites, combinaciones y transiciones antes que el centro.
3. **Lo inválido importa tanto como lo válido.**
4. **Reglas escritas antes que casos:** si no se sabe qué debería pasar, no hay caso, hay una pregunta.
5. **El resultado esperado es concreto:** un valor, un estado o un error con código, nunca "funciona".

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Los casos diseñados deben automatizarse en el frontend | `frontend:testing` | Tabla de casos y nivel (componente, integración) |
| Los casos diseñados deben automatizarse en el backend | `backend:testing` | Tabla de casos y nivel (unitario, integración, API) |
| Las reglas no están escritas o se contradicen entre código y requisitos | `test-strategy` | Área y contradicciones (riesgo aceptado o aclaración) |
| Una transición prohibida es posible en el código | `backend:domain-logic` | Máquina de estados y transición |
| El servidor acepta entradas que deberían ser inválidas | `backend:http-layer` | Endpoint, campo y caso |
| Casos difíciles de imaginar o de combinar a mano | `exploratory-testing` | Área y heurísticas sugeridas |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: elegir técnica, cada técnica con ejemplo, negativos, property-based y Gherkin. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `test-strategy`: decide dónde aplicar esta skill con más profundidad.
- `frontend:testing`, `backend:testing`: implementan los casos.
- `frontend:forms` y `backend:http-layer`: validaciones donde viven muchos límites.
