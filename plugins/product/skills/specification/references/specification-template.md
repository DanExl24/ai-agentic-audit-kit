# Plantilla de especificación

Los IDs ilustran el formato. Usa los que correspondan al proyecto y al módulo.

~~~markdown
# <PRD o SRS> — <alcance>
- Estado: borrador | acordado
- Quién aprueba y fuente: <…>
- Problema, actores y resultado: <…>
- Objetivos o evidencia: <enlaces OBJ, brief o entrevista>

## Alcance y restricciones
- Dentro: <… con fuente y estado>
- Fuera: <…>
- Dependencias y restricciones: <… con evidencia>
- Pendientes que afectan al alcance: <enlaces PRE/SUP>

## Requisitos funcionales

### RF-BUZ-001
Cuando <condición>, el sistema <resultado verificable>.
- Estado y origen: <estado, enlace a RN, HU, CA o DEC>
- Alternativas aplicables: <…>
- Verificación: <criterio, método y evidencia si existe>

## Requisitos no funcionales

### RNF-BUZ-001
En <escenario y entorno>, <métrica> debe cumplir <umbral o pendiente>.
- Estado y origen: <…>
- Condiciones: <carga, datos, ventana y punto de medición>
- Verificación: <procedimiento, criterio de éxito y evidencia si existe>

## Interfaces
| Productor y consumidor | Operación o evento | Contrato o requisito | Estado y origen |
| :--- | :--- | :--- | :--- |
| <…> | <…> | <enlace> | <…> |

## Decisiones, supuestos y preguntas
<Enlaces a los registros vigentes>
~~~
