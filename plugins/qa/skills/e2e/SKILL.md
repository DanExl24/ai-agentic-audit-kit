---
name: e2e
description: "Diseña, construye y audita suites de pruebas end-to-end con Playwright o Cypress: qué recorridos merecen E2E, estructura con fixtures y page objects ligeros, localizadores por rol accesible, esperas basadas en condiciones, datos sembrados por API con aislamiento entre tests, autenticación reutilizada, paralelismo, qué simular y qué no en la red, entornos (local, preview por PR, staging), artefactos (trazas, vídeo), cuarentena de tests intermitentes, smoke tests tras desplegar, regresión visual y comprobaciones de accesibilidad. Úsala al crear la suite E2E, ante tests intermitentes o lentos, o para definir el smoke de producción. No para tests de componentes o de API en proceso (frontend:testing, backend:testing)."
---

# Suites end-to-end

Un test E2E recorre la aplicación como un usuario, con frontend, backend y base de datos reales. Es el único que demuestra que el **recorrido completo** funciona, y también el más lento, caro e intermitente. Una buena suite E2E es **pequeña, determinista y rápida de diagnosticar**: pocos recorridos críticos, datos propios por test y una traza que explica cada fallo.

## Cuándo usarla

- Crear la suite E2E de un proyecto o ampliarla con un recorrido crítico.
- Tests E2E intermitentes, lentos o que nadie mira cuando fallan.
- Definir el smoke test que corre tras cada despliegue.
- Añadir regresión visual o comprobaciones de accesibilidad automáticas.
- Auditar una suite existente.

**No es para:** tests de componentes, hooks o stores → `frontend:testing` · tests de API en proceso o de integración con base de datos → `backend:testing` · decidir qué recorridos son críticos → `test-strategy` · dónde y cuándo corre la suite en CI → `quality-gates`.

## Paso 0: contexto (ambos modos)

1. **Herramienta y configuración:** Playwright o Cypress (versión), configuración, carpeta de tests, cómo se arranca la app para los tests. Carga [playwright.md](references/playwright.md) o [cypress.md](references/cypress.md). Si no hay ninguna, recomienda Playwright salvo que el equipo ya use Cypress.
2. **Recorridos críticos:** de `test-strategy` si existe; si no, los del dinero, el acceso y los datos principales.
3. **Entornos y datos:** contra qué se ejecuta (local, preview, staging), cómo se crean y limpian los datos, usuarios de prueba. Los tests que escriben van contra una **instancia desechable** (modo demo, base en memoria); si la app de pruebas comparte puerto con la instancia real, `reuseExistingServer` puede reutilizar la real y escribir en sus datos: dale un **puerto propio**. Ver [output-formats.md § Instalaciones y datos reales](../../standards/output-formats.md#instalaciones-y-datos-reales).
4. **Estado actual** (Auditar): número de tests, duración, tasa de fallos e intermitentes en los últimos runs de CI.
5. Si existe `.sdlc/context.md`, léelo y respeta sus convenciones y decisiones ([context.md](../../standards/context.md)).

## Modo Construir

1. **Selecciona los recorridos:** pocos y críticos; lo demás, en niveles inferiores. Ver [patterns.md § Qué merece E2E](references/patterns.md#qué-merece-e2e).
2. **Estructura:** fixtures para datos, autenticación y páginas; page objects ligeros solo donde se repiten interacciones. Ver [patterns.md § Estructura](references/patterns.md#estructura).
3. **Localizadores por rol** y esperas basadas en condiciones, nunca tiempos fijos. Ver [patterns.md § Localizadores y esperas](references/patterns.md#localizadores-y-esperas).
4. **Datos y aislamiento:** cada test crea sus datos por API o base de datos, únicos, y no depende de otro test. Ver [patterns.md § Datos](references/patterns.md#datos-y-aislamiento).
5. **Autenticación reutilizada,** con un test propio para el login de verdad.
6. **Red:** backend real; se simulan solo terceros (pagos, email) o fallos difíciles de provocar.
7. **Diagnóstico:** traza, captura y vídeo en los fallos; informe en CI.
8. **Smoke tras desplegar:** subconjunto etiquetado, de solo lectura o con cuentas de prueba. Ver [patterns.md § Smoke](references/patterns.md#smoke-tras-desplegar).
9. **Tipos:** los archivos de tests y la configuración entran en un tsconfig (o en el linter) que corra el proyecto; Playwright transpila sin comprobar tipos.
10. Ejecuta la suite varias veces (repetición) antes de darla por estable y entrega según [output-formats.md § Construir](../../standards/output-formats.md#modo-construir).

## Modo Auditar

1. Inventaria tests, recorridos cubiertos, duración e historial de fallos.
2. Lee una muestra representativa buscando los anti-patrones de [patterns.md § Anti-patrones](references/patterns.md#anti-patrones).
3. Si puedes ejecutar, repite los tests sospechosos (`--repeat-each` o equivalente) para medir intermitencia.
4. Recorre [checklist.md](references/checklist.md).
5. Clasifica con [severity.md](../../standards/severity.md) y entrega según [output-formats.md § Auditar](../../standards/output-formats.md#modo-auditar) con código `QA-E2E`.

## Principios

1. **Pocos recorridos, críticos y completos:** el resto de comprobaciones va en niveles más baratos.
2. **Como un usuario:** localizadores por rol y texto visible, no por clases o estructura del DOM.
3. **Esperar condiciones, nunca tiempo.**
4. **Cada test es dueño de sus datos** y puede correr solo, en cualquier orden y en paralelo.
5. **Un fallo se diagnostica con su traza,** sin volver a ejecutarlo en local.
6. **Un test intermitente es un bug** (del test o de la app), no algo que se reintenta hasta que pasa.

## Handoffs

Según [handoffs.md](../../standards/handoffs.md): profundidad máxima de 2, alcance acotado, sin reinvocar skills ya aplicadas y registro de pendientes.

| Disparador (observable) | Skill | Alcance y contexto que se pasa |
| :--- | :--- | :--- |
| Los localizadores por rol no encuentran elementos porque no tienen nombre accesible | `frontend:accessibility` | Componentes y elementos sin nombre |
| Un recorrido falla de forma intermitente por una carrera real de la aplicación (no del test) | `fullstack:flow-diagnosis` | Recorrido, traza y frecuencia |
| Comprobaciones de detalle (validaciones, estados de un componente) metidas en E2E | `frontend:testing` | Tests y casos a bajar de nivel |
| No hay forma de sembrar datos o limpiar el estado por API | `backend:testing` | Entidades necesarias y entorno |
| La suite no corre en CI, tarda demasiado o los fallos no bloquean | `quality-gates` | Configuración de CI y tiempos |
| No está claro qué recorridos son críticos | `test-strategy` | Recorridos actuales y producto |

## Referencias

| Archivo | Cuándo cargarlo |
| :--- | :--- |
| [patterns.md](references/patterns.md) | Siempre: qué merece E2E, estructura, localizadores, datos, red, entornos, intermitencia, smoke, visual y accesibilidad. |
| [playwright.md](references/playwright.md) · [cypress.md](references/cypress.md) | Según la herramienta. |
| [checklist.md](references/checklist.md) | Modo Auditar. |

## Skills relacionadas

- `test-strategy`: qué recorridos son críticos.
- `quality-gates`: cuándo corre la suite y qué bloquea.
- `frontend:testing` y `backend:testing`: los niveles por debajo.
- `frontend:accessibility`: localizadores por rol y comprobaciones con axe.
