---
name: load-testing
description: "Diseña, ejecuta y audita pruebas de carga y rendimiento con k6, Locust o Gatling: objetivo y tipo de prueba (smoke, carga, estrés, pico, resistencia, punto de ruptura), modelo de carga abierto o cerrado, escenarios a partir del tráfico real, datos parametrizados, think time, umbrales derivados de los SLO, entorno representativo y autorizado, observación del sistema durante la prueba, interpretación de percentiles y saturación, y smoke de rendimiento en CI. Úsala antes de un lanzamiento o de un pico esperado, para conocer la capacidad o para fijar un presupuesto de rendimiento. No para localizar y corregir el cuello de botella en el código (backend:performance) ni para el rendimiento del cliente (frontend:performance)."
---

# Pruebas de carga

Una prueba de carga responde a una pregunta concreta: **¿aguanta el sistema el tráfico esperado con la latencia y la tasa de errores aceptables, y dónde se rompe?** Sin pregunta, sin umbrales y sin observar el sistema mientras tanto, solo produce un gráfico bonito. Esta skill diseña pruebas que dan respuestas y las convierte en una puerta automática.

## Cuándo usarla

- Antes de un lanzamiento, una campaña o un pico de tráfico previsto.
- Conocer la capacidad actual (usuarios o peticiones por segundo hasta degradarse).
- Verificar que un cambio no empeora el rendimiento (presupuesto en CI).
- Detectar fugas o degradación con el tiempo (resistencia).
- Auditar scripts de carga existentes.

**No es para:** encontrar y corregir el cuello de botella en el código, la base de datos o el runtime → `backend:performance` · rendimiento del navegador y Web Vitals → `frontend:performance` · caché y capacidad de la base de datos en detalle → `backend:caching`, `backend:data-access`.

## Paso 0: contexto y autorización (ambos modos)

1. **Autorización y entorno:** una prueba de carga puede tumbar un servicio, disparar alertas, generar costes y bloquear IPs. Confirma **contra qué entorno** se ejecuta, que es del usuario o tiene permiso escrito, que no comparte infraestructura crítica sin aviso y quién debe saberlo. **Nunca contra producción ni contra servicios de terceros sin autorización explícita**; los terceros (pagos, email) se simulan.
2. **Pregunta y objetivos:** qué se quiere saber y los SLO o expectativas (p. ej. p95 < 300 ms y < 1 % de errores con 200 peticiones/s).
3. **Tráfico real o esperado:** endpoints más usados, mezcla de operaciones, picos, tamaño de los datos (de métricas, logs o estimación de negocio).
4. **Herramienta:** k6, Locust o Gatling según el equipo y el stack; carga [k6.md](references/k6.md), [locust.md](references/locust.md) o [gatling.md](references/gatling.md). Si no hay ninguna, recomienda k6.
5. **Observabilidad disponible** durante la prueba: métricas del servidor, base de datos, trazas.
6. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Tipo de prueba** según la pregunta. Ver [patterns.md § Tipos](references/patterns.md#tipos-de-prueba).
2. **Modelo de carga** abierto (llegadas por segundo) o cerrado (usuarios concurrentes). Ver [patterns.md § Modelo](references/patterns.md#modelo-de-carga).
3. **Escenarios** con la mezcla real de operaciones, datos parametrizados y think time. Ver [patterns.md § Escenarios](references/patterns.md#escenarios-realistas).
4. **Umbrales** derivados de los SLO, que hacen fallar la prueba. Ver [patterns.md § Umbrales](references/patterns.md#umbrales).
5. **Entorno y preparación:** entorno representativo, datos sembrados, terceros simulados, generador de carga con capacidad suficiente y fuera del sistema bajo prueba.
6. **Ejecuta** empezando por un smoke (1–2 usuarios) y subiendo; observa servidor y base de datos durante la prueba.
7. **Interpreta** con [patterns.md § Interpretación](references/patterns.md#interpretación): percentiles, errores, saturación, punto de inflexión.
8. **Automatiza** un smoke de rendimiento en CI con umbrales (ver `quality-gates`) y deja la prueba completa como ejecución manual o programada.
9. Entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir): script, resultados con gráficos o tablas, conclusión respecto a la pregunta y siguientes pasos.

## Modo Auditar

1. Revisa scripts y resultados existentes contra [patterns.md § Anti-patrones](references/patterns.md#anti-patrones): sin umbrales, sin think time, datos repetidos que solo prueban la caché, generador saturado, entorno no representativo.
2. Comprueba que las conclusiones se sostienen con los datos (percentiles, errores, duración suficiente).
3. Recorre [checklist.md](references/checklist.md).
4. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-LOAD`.

## Principios

1. **Una pregunta por prueba** y una respuesta al final.
2. **Autorización primero:** nunca contra producción ni terceros sin permiso explícito.
3. **Umbrales que fallan:** una prueba sin criterio de éxito no prueba nada.
4. **Tráfico realista:** mezcla, datos y ritmo parecidos a los reales.
5. **Percentiles, no medias,** junto con la tasa de errores.
6. **Observar el sistema durante la prueba:** el resultado del generador dice qué pasó; las métricas del servidor dicen por qué.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| La prueba localiza degradación en endpoints concretos (latencia, errores, saturación) | `backend:performance` | Endpoints, carga a la que degradan, métricas y trazas |
| Lecturas repetidas que aguantarían más con caché | `backend:caching` | Endpoints y patrón de acceso |
| No hay métricas del servidor o de la base de datos para interpretar la prueba | `backend:observability` | Servicios y métricas que faltan |
| El rate limiting propio frena la prueba o, al revés, no existe y el sistema cae | `backend:api-security` | Endpoints y límites observados |
| El smoke de rendimiento debe convertirse en puerta de CI | `quality-gates` | Script, umbrales y etapa |
| El tiempo se va en el cliente (render, bundle), no en el servidor | `frontend:performance` | Páginas y mediciones |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: tipos, modelo de carga, escenarios, umbrales, entorno, interpretación y anti-patrones. |
| [k6.md](references/k6.md) · [locust.md](references/locust.md) · [gatling.md](references/gatling.md) | Según la herramienta. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `backend:performance`: diagnóstico y corrección del cuello de botella.
- `backend:observability`: métricas para interpretar la prueba.
- `quality-gates`: el smoke de rendimiento en CI.
- `test-strategy`: si el rendimiento es un riesgo que merece esta prueba.
