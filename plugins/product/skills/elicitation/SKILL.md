---
name: elicitation
description: "Planifica, ejecuta y audita el levantamiento de requisitos: mapa de interesados (interés e influencia), elección de técnicas (entrevistas, observación, talleres, análisis de documentos y del sistema existente, cuestionarios, prototipos), guiones de entrevista con preguntas sobre hechos pasados, notas de sesión con citas, registro de preguntas abiertas (PRE), supuestos (SUP) y decisiones (DEC), conflictos entre interesados y requisitos inferidos de un sistema ya construido. El agente puede entrevistar al usuario en el chat por bloques. Úsala al empezar un proyecto o funcionalidad, cuando los requisitos son vagos o contradictorios, o para documentar un sistema existente. No para validar la idea de negocio (discovery) ni para redactar historias o reglas definitivas (user-stories, domain-modeling)."
---

# Levantamiento de requisitos

Los requisitos no se "recogen" como si estuvieran escritos en algún sitio: se **descubren** hablando con quien tiene el problema, observando cómo trabaja y leyendo lo que ya existe. Esta skill organiza ese trabajo para que cada requisito tenga un origen, cada duda un responsable y cada decisión su motivo.

## Cuándo usarla

- Al empezar un proyecto o una funcionalidad con requisitos vagos.
- Los interesados piden cosas distintas o contradictorias.
- Hay que documentar un sistema ya construido (requisitos inferidos del código y de la documentación).
- Revisar si los requisitos de un proyecto tienen origen, si las dudas se resuelven y si las decisiones están registradas.

**No es para:** decidir si la idea merece la pena, propuesta de valor y MVP → `discovery` · fijar el glosario, el modelo y las reglas de negocio → `domain-modeling` · redactar historias y criterios de aceptación → `user-stories` · investigación de usabilidad con prototipos en detalle → `frontend:ux-review`.

## Paso 0: contexto (ambos modos)

1. **Objetivo del levantamiento:** qué decisión o entregable desbloquea (brief, backlog del MVP, documentar un módulo).
2. **Material previo:** brief de `discovery`, documentación, tickets de soporte, el sistema actual si existe.
3. **Quién puede responder:** el usuario del chat, otros interesados a los que el usuario tiene acceso, documentos. En un proyecto personal, el autor es el principal interesado y se declara.
4. **Cómo se hará:** el agente entrevista al usuario en el chat, prepara guiones para que el usuario entreviste a otros, o analiza documentos y código.
5. **IDs:** convención del proyecto o la de [ids-and-links.md](../../standards/ids-and-links.md).
6. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir (levantar)

1. **Interesados** (`INT`): rol, interés, influencia y cómo consultarlo. Ver [patterns.md § Interesados](references/patterns.md#mapa-de-interesados).
2. **Técnicas** según el objetivo y el acceso. Ver [patterns.md § Técnicas](references/patterns.md#elección-de-técnicas).
3. **Guion** por sesión, con preguntas sobre hechos pasados y concretos. Ver [interview-guide.md](references/interview-guide.md).
4. **Ejecuta:**
   - **Entrevista en el chat:** bloques de 3–5 preguntas, resumen de lo entendido y confirmación antes de seguir. Ver [patterns.md § Entrevistar en el chat](references/patterns.md#entrevistar-al-usuario-en-el-chat).
   - **Sistema existente:** requisitos inferidos del código y la documentación, marcados como "inferido" y convertidos en preguntas de confirmación. Ver [patterns.md § Sistema existente](references/patterns.md#análisis-del-sistema-existente).
5. **Registra** tras cada sesión: notas con citas, requisitos candidatos, preguntas (`PRE`), supuestos (`SUP`) validados o refutados y decisiones (`DEC`). Ver [patterns.md § Registros](references/patterns.md#registros).
6. **Conflictos** entre interesados: se registran las posiciones y quién decide; no se resuelven en silencio. Ver [patterns.md § Conflictos](references/patterns.md#conflictos-entre-interesados).
7. Entrega en `docs/product/elicitation/` (o donde el proyecto guarde su documentación) según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir), con los requisitos candidatos listos para `domain-modeling` y `user-stories`.

## Modo Auditar

1. Localiza el material: notas, actas, documentos de requisitos, tickets.
2. Comprueba si los requisitos tienen origen, si las preguntas abiertas tienen responsable y fecha, si las decisiones tienen motivo y si se consultó a los interesados relevantes.
3. Busca requisitos contradictorios entre documentos o con el código.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `PR-ELIC`.

## Principios

1. **Hechos antes que opiniones:** "cuéntame la última vez que…" vale más que "¿usarías…?".
2. **Cada requisito tiene origen:** quién lo dijo, qué documento o qué parte del código.
3. **Las dudas se registran,** con responsable; nadie las resuelve suponiendo.
4. **Las decisiones llevan motivo** y fecha, para no reabrirlas cada semana.
5. **Los conflictos se hacen visibles** y los decide quien tiene la autoridad.
6. **Lo inferido se confirma** antes de tratarlo como requisito.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| No está claro qué problema se resuelve o para quién | `discovery` | Notas y contradicciones sobre el problema o el usuario |
| Términos usados con significados distintos o reglas de negocio enunciadas en las sesiones | `domain-modeling` | Citas, términos y reglas candidatas con su origen |
| Hay requisitos candidatos suficientes para escribir el backlog | `user-stories` | Requisitos candidatos, interesados y decisiones |
| Se mencionan datos personales, retención o consentimiento | `backend:data-privacy` | Datos, finalidad y citas |
| Requisitos de rendimiento, disponibilidad o seguridad con cifras | `specification` | Cifras, contexto y origen |
| El requisito inferido del código contradice la documentación | `traceability` | Documento, código (archivo y símbolo) y discrepancia |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: interesados, técnicas, entrevista en el chat, sistema existente, registros y conflictos. |
| [interview-guide.md](references/interview-guide.md) | Modo Construir: guion de entrevista y plantillas de notas y registros. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `discovery`: los supuestos que el levantamiento valida.
- `domain-modeling`: convierte el vocabulario y las reglas en un modelo.
- `user-stories`: convierte los requisitos candidatos en historias con criterios.
