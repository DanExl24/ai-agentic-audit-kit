# Patrones de especificación

## Documento y estado

Un PRD explica para quién se resuelve qué problema, con qué resultado, qué entra en la entrega y cómo se evaluará. Un SRS detalla qué debe hacer el sistema y en qué condiciones, qué límites debe respetar y cómo se comprobará. Un documento puede enlazar el otro o reunir ambos niveles si el proyecto ya usa ese formato.

Usa `borrador` para una propuesta que todavía requiere aprobación. Un requisito puede estar acordado dentro de un documento en borrador si hay una fuente vigente que respalda ese enunciado completo. La presencia de un comportamiento en código evidencia que existe o se observa, sin confirmar por sí sola que sea el comportamiento deseado. Si la fuente acordada y el código discrepan, escribe ambos con sus referencias y conserva el desacuerdo visible.

## Requisitos verificables

- **RF:** indica sistema o actor, disparador, condición y resultado. Separa efectos que puedan verificarse o aprobarse por separado. Si una nota vence y tiene respaldo, la política acordada puede exigir un intento de borrado remoto antes del local. El número de reintentos puede seguir en borrador con su `PRE`, sin invalidar la parte confirmada de la política.
- **RNF:** especifica propiedad, escenario, métrica, umbral, carga, ventana de medición y método. Por ejemplo, «p95 de la consulta de historial ≤ 200 ms con 10.000 registros y 20 clientes concurrentes en el entorno acordado». Las cifras del ejemplo ilustran la forma. Usa valores respaldados por el proyecto, o etiqueta los valores sugeridos como propuesta.
- **Interfaz:** identifica consumidor, productor, operación o evento y fuente del contrato. Incluye resultados y fallos que sean requisitos. Reutiliza OpenAPI o esquemas existentes. Si la elección técnica está abierta, registra la necesidad de negocio y la pregunta.
- **Restricción:** indica qué se limita, por qué y qué fuente vigente lo exige. Un precedente del código puede orientar la solución. Por ejemplo, preservar datos y estado al actualizar y reiniciar es un resultado verificable. La técnica SQL usada en migraciones anteriores va como referencia de diseño, salvo que una decisión o restricción explícita la exija.

## Verificación y fuentes

Vincula cada requisito con un criterio o método de comprobación. Puede ser una prueba funcional, medición, inspección o demostración. Indica si ya hay evidencia o si solo está previsto el método. Conserva IDs existentes al revisar requisitos y deja enlaces bidireccionales cuando ambos artefactos se puedan actualizar dentro del alcance.
