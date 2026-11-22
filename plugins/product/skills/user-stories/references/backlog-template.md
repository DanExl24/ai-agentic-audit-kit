# Plantilla de backlog

Usa los IDs y la estructura vigentes. Los identificadores siguientes ilustran el formato y se sustituyen por los disponibles en el proyecto.

~~~markdown
# Backlog — <módulo>
- Objetivo y fuente: <enlace al brief, requisito o decisión>
- Recorrido y corte de entrega: <actividades y qué se puede completar>

## EP-BUZ-001
<resultado que agrupa las historias>
- Objetivo: <enlace>
- Estado: borrador | acordado | implementado | obsoleto
- Historias: <enlaces a HU>

## HU-BUZ-001
Como <actor>, quiero <capacidad> para <beneficio>.
- Estado: borrador | acordado | implementado | obsoleto
- Origen: <enlaces a OBJ, INT, RN o DEC>
- Alcance: <dentro y fuera cuando importe>
- Dependencias: <ID, capacidad requerida y evidencia de disponibilidad o de inclusión en el mismo incremento listo>
- Preparación: lista | pendiente de refinamiento | bloqueada — <evidencia o PRE/SUP>

### CA-BUZ-001.1
Dado <estado>, cuando <acción>, entonces <resultado observable>.
- Origen: <regla, decisión o requisito>
- Estado: <estado y enlace al pendiente si aplica>

## CU-BUZ-001
<objetivo del actor>
- Origen y estado: <enlace y estado>
- Actor y disparador: <…>
- Precondiciones: <…>
- Flujo principal: <pasos>
- Alternativas y excepciones: <condición y resultado>
- Postcondiciones: <…>
- Historias y criterios: <enlaces>
~~~
