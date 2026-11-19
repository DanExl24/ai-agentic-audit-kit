---
name: quality-gates
description: "Diseña y audita las puertas de calidad del pipeline: qué pruebas corren en cada etapa (local, PR, merge, nocturno, release, tras desplegar), presupuestos de tiempo, selección de tests afectados, paralelismo y sharding, política de tests intermitentes (detección, cuarentena con caducidad, reintentos visibles), informes y artefactos, umbrales de cobertura y mutación sobre el código cambiado, datos y entornos de prueba efímeros, y checks obligatorios en la rama principal. Úsala al montar o reorganizar el CI de pruebas, cuando el pipeline es lento, los fallos se ignoran o los tests intermitentes se acumulan. No para la configuración general de lint, tipos y build (frontend:tooling, backend:tooling)."
---

# Puertas de calidad

Los tests solo protegen si **corren en el momento adecuado y su fallo bloquea**. Un pipeline de 40 minutos se salta; uno que falla al azar se ignora; uno que nunca bloquea es decoración. Esta skill decide **qué corre dónde, cuánto puede tardar y qué pasa cuando falla**, para que la señal de calidad sea rápida y creíble.

## Cuándo usarla

- Montar el CI de pruebas de un proyecto o reorganizarlo.
- El pipeline es lento y la gente lo esquiva (merge sin esperar, reintentos manuales).
- Tests intermitentes acumulados, reintentos que esconden fallos.
- Definir umbrales de cobertura o mutación que no se puedan engañar.
- Auditar qué protege de verdad la rama principal.

**No es para:** configurar lint, type-check, build o la imagen del contenedor → `frontend:tooling`, `backend:tooling` · escribir o arreglar los tests en sí → `frontend:testing`, `backend:testing`, `e2e` · decidir qué riesgos cubrir → `test-strategy`.

## Paso 0: contexto (ambos modos)

1. **Plataforma de CI** y archivos de pipeline (`.github/workflows/`, `.gitlab-ci.yml`, otros). Carga [github-actions.md](references/github-actions.md) o [gitlab-ci.md](references/gitlab-ci.md); para otras plataformas aplica [patterns.md](references/patterns.md).
2. **Suites existentes** por tipo (unitarias, integración, E2E, contrato, carga), cuánto tarda cada una y dónde corre hoy.
3. **Historial:** duración del pipeline, tasa de fallos, tests intermitentes conocidos, reintentos manuales, merges con checks en rojo.
4. **Protección de ramas:** checks obligatorios, revisiones, quién puede saltárselos.
5. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Mapa de etapas:** qué corre en local, en cada PR, al hacer merge, cada noche, antes del release y tras desplegar. Ver [patterns.md § Etapas](references/patterns.md#etapas).
2. **Presupuestos de tiempo** por etapa y técnicas para cumplirlos: caché, paralelismo, sharding, selección de tests afectados. Ver [patterns.md § Velocidad](references/patterns.md#velocidad).
3. **Política de intermitencia:** detección, cuarentena con issue y caducidad, reintentos que se informan. Ver [patterns.md § Intermitencia](references/patterns.md#política-de-intermitencia).
4. **Umbrales** sobre el código cambiado (cobertura, mutación) y lo que bloquea frente a lo que solo informa. Ver [patterns.md § Umbrales](references/patterns.md#umbrales).
5. **Informes y artefactos:** JUnit para el resumen, HTML y trazas para diagnosticar, siempre subidos aunque el job falle.
6. **Datos y entornos:** servicios efímeros (base de datos en contenedor), siembra reproducible, entornos de preview.
7. **Checks obligatorios** en la rama principal, sin posibilidad de saltarlos sin rastro.
8. Entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir), probando el pipeline en un PR.

## Modo Auditar

1. Dibuja el mapa real de etapas y tiempos a partir de los archivos de pipeline y del historial.
2. Compara con [patterns.md](references/patterns.md): huecos (algo crítico que no corre nunca), duplicados, etapas lentas, fallos que no bloquean.
3. Revisa la política de intermitencia y los umbrales: ¿se pueden engañar o ignorar?
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-GATE`.

## Principios

1. **Rápido donde se decide:** la señal del PR en minutos; lo lento, más tarde y en paralelo.
2. **Un fallo bloquea o no existe:** lo que solo informa se etiqueta como informativo, a la vista.
3. **Intermitente es un bug,** con dueño y fecha; nunca un reintento silencioso.
4. **Umbrales sobre lo que cambia,** no sobre totales que se maquillan.
5. **Todo fallo es diagnosticable** con los artefactos del job, sin reproducir en local.
6. **La rama principal está protegida** por checks obligatorios, sin atajos sin rastro.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Tests E2E lentos, intermitentes o mal estructurados | `e2e` | Suite, tiempos y tests intermitentes |
| Tests intermitentes de frontend por esperas, red o estado compartido | `frontend:testing` | Tests y causa sospechada |
| Tests intermitentes de backend por base de datos compartida, tiempo o concurrencia | `backend:testing` | Tests y causa sospechada |
| El pipeline carece de lint, type-check, build reproducible o escaneo de dependencias | `frontend:tooling` · `backend:tooling` | Archivos de pipeline |
| Secretos en el pipeline, en logs o en artefactos | `backend:api-security` | Variables, pasos y artefactos |
| No está claro qué suites son imprescindibles en cada etapa | `test-strategy` | Mapa de riesgos y suites existentes |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: etapas, velocidad, intermitencia, umbrales, informes, datos y entornos, protección de ramas. |
| [github-actions.md](references/github-actions.md) · [gitlab-ci.md](references/gitlab-ci.md) | Según la plataforma de CI. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `test-strategy`: qué riesgos debe proteger cada etapa.
- `e2e`: la suite más cara del pipeline.
- `frontend:tooling` y `backend:tooling`: el resto del pipeline (lint, tipos, build, imágenes).
