# Formatos de entrega

## Modo Construir

1. **Plan breve** si el entregable es grande (plan de pruebas, suite nueva): qué se crea y por qué.
2. **Entregable** en el repositorio siguiendo las convenciones del proyecto: documento de estrategia o plan (`docs/testing/…` o donde el proyecto guarde su documentación), casos de prueba, tests o configuración.
3. **Verificación:** ejecuta lo que se pueda (tests, linters de Gherkin, la propia sesión exploratoria). Lo que no se pudo verificar, se dice.
4. **Resumen:** qué cambió, decisiones y pendientes.
5. **Handoffs** hechos y pendientes ([handoffs.md](handoffs.md#bloque-de-traza-en-la-entrega)).

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

La numeración es siempre secuencial (`QA-STRAT-001`); no se inventan sufijos descriptivos.

## Veracidad de lo cargado (todas las entregas)

El anexo de referencias o skills aplicadas dice **exactamente** qué se leyó en esta sesión:

- ✅ solo para archivos **leídos completos**; ◐ con las líneas para lecturas parciales; ❌ con el motivo para lo no leído; n.a. si no existe.
- Una comprobación ("checklist aplicado: 0 hallazgos") solo se afirma si se cargó su `checklist.md`; si no, se escribe **"no aplicado"** y el motivo.
- "Inferido" o "por conocimiento general" no cuenta como aplicado: va como ❌ con esa nota.
- Lo que se dejó de cargar por coste aparece como ❌ (coste), no se omite.

## Handoffs en la entrega

Toda entrega termina con el bloque de handoffs hechos y pendientes de [handoffs.md](handoffs.md#bloque-de-traza-en-la-entrega). Si existe `.sdlc/context.md` ([context.md](context.md)), los pendientes se registran allí.
