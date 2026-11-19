# Formatos de entrega

## Modo Construir

1. **Plan breve** si el entregable es grande (plan de pruebas, suite nueva): qué se crea y por qué.
2. **Entregable** en el repositorio siguiendo las convenciones del proyecto: documento de estrategia o plan (`docs/testing/…` o donde el proyecto guarde su documentación), casos de prueba, tests o configuración.
3. **Verificación:** ejecuta lo que se pueda (tests, linters de Gherkin, la propia sesión exploratoria). La verificación debe **cubrir los archivos nuevos**: si el typecheck o el linter no los incluye (p. ej. `e2e/` fuera del `include` del tsconfig), inclúyelos o di que no se comprobaron; "typecheck sin errores" no vale si no los miró. Lo que no se pudo verificar, se dice.
4. **Resumen:** qué cambió, decisiones y pendientes, incluidas las instalaciones (ver abajo).
5. **Contexto:** actualiza `.sdlc/context.md` si existe ([context.md](context.md)).
6. **Handoffs** hechos y pendientes ([handoffs.md](handoffs.md#bloque-de-traza-en-la-entrega)).

### Instalaciones y datos reales

- **Dependencias del proyecto** (`devDependencies`, navegadores de Playwright en la caché del proyecto): se pueden añadir si la petición implica la herramienta; se declaran en el resumen.
- **Instalaciones a nivel de sistema** (winget, choco, brew, apt, `npm -g`, `pip` global): **pregunta antes**, con la alternativa sin instalar si existe (Docker, `npx`, binario portable en una carpeta del proyecto ignorada por git).
- **Escrituras contra datos reales:** las pruebas que crean, modifican o borran datos se ejecutan contra una **instancia desechable** (modo demo, base en memoria, datos de prueba). Si el proyecto tiene una, úsala aunque el usuario autorice su entorno. Contra la instancia con datos reales, solo lecturas, salvo autorización expresa para escribir; entonces los datos de prueba llevan un marcador reconocible y se comprueba que la limpieza no dejó restos.

## Modo Auditar

```markdown
# Auditoría <skill> — <alcance>

## Resumen
- Alcance: <módulos, suites, flujos o release revisados>
- Contexto: <tipo de producto, riesgo, herramientas de test detectadas>
- Hallazgos: 🔴 n · 🟠 n · 🟡 n · 🔵 n · ℹ️ n
- Veredicto: <una o dos frases>

## Hallazgos

### [QA-<CÓDIGO>-001] <título>
- **Severidad:** HIGH — <justificación: riesgo × detección>
- **Ubicación:** `ruta/de/tests` o área / flujo / documento
- **Problema y escenario:** <qué defecto podría escapar y cómo>
- **Evidencia:** <caso ausente, test que pasa con la funcionalidad rota, ejecución, reporte>
- **Corrección:** <casos, tests, cambio de proceso; concreto y aplicable>

## Lo que está bien
## Por verificar
<configuración remota o datos no accesibles: qué comprobar y dónde; sin severidad>
## Fuera de alcance / otras skills
## Handoffs
- Hechos: <skill> (<alcance>) → <códigos>
- Pendientes: <skill> — <disparador y evidencia>
```

| Skill | Código |
| :--- | :--- |
| test-strategy | `QA-STRAT` |
| test-design | `QA-DESIGN` |
| exploratory-testing | `QA-EXPL` |
| e2e | `QA-E2E` |
| quality-gates | `QA-GATE` |
| load-testing | `QA-LOAD` |
| dast | `QA-DAST` |
| defect-analysis | `QA-DEFECT` |

`audit` no tiene código propio: conserva el de la skill que detectó cada hallazgo (el de la causa raíz si se deduplicó).

La numeración es siempre secuencial (`QA-STRAT-001`); no se inventan sufijos descriptivos.

## Veracidad de lo cargado (todas las entregas)

El anexo de referencias o skills aplicadas dice **exactamente** qué se leyó en esta sesión:

- ✅ solo para archivos **leídos completos**; ◐ con las líneas para lecturas parciales; ❌ con el motivo para lo no leído; n.a. si no existe.
- Una comprobación ("checklist aplicado: 0 hallazgos") solo se afirma si se cargó su `checklist.md`; si no, se escribe **"no aplicado"** y el motivo.
- "Inferido" o "por conocimiento general" no cuenta como aplicado: va como ❌ con esa nota.
- Lo que se dejó de cargar por coste aparece como ❌ (coste), no se omite.

## Handoffs en la entrega

Toda entrega termina con el bloque de handoffs hechos y pendientes de [handoffs.md](handoffs.md#bloque-de-traza-en-la-entrega). Si existe `.sdlc/context.md` ([context.md](context.md)), los pendientes se registran allí.
