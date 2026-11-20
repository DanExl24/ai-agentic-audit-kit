# Formatos de entrega

## Datos de negocio: preguntar, no inventar

Las skills de producto trabajan con información que **solo el usuario o sus interesados tienen**: quiénes son los usuarios, qué problema pagan por resolver, precios, volúmenes, plazos, reglas de la empresa.

- **No inventes** cifras, segmentos, competidores, precios ni reglas. Si faltan, pregunta (pocas preguntas, las que bloquean) o regístralas como supuesto `SUP-…` con estado "pendiente de validar" y como pregunta `PRE-…`.
- Lo deducido del código o de documentos existentes se marca **"inferido"** con su fuente hasta que alguien lo confirme.
- Distingue en la entrega lo **confirmado** (lo dijo el usuario o un documento), lo **inferido** y lo **supuesto**.

## Modo Construir

1. **Plan breve** si el entregable es grande (brief completo, modelo de dominio de varios módulos): qué se crea, dónde y qué preguntas bloquean.
2. **Entregable** en el repositorio, en la estructura del proyecto o en la de [ids-and-links.md § Ubicación](ids-and-links.md#ubicación-por-defecto), con IDs y enlaces según ese estándar.
3. **Verificación:** IDs únicos y sin huecos de numeración no justificados (búsqueda en `docs/`), enlaces relativos que resuelven, diagramas Mermaid con sintaxis válida, y cada elemento con estado y origen. Lo que no se pudo verificar, se dice.
4. **Resumen:** qué se creó o cambió, decisiones (`DEC-…`), supuestos (`SUP-…`) y preguntas abiertas (`PRE-…`) que quedan.
5. **Contexto:** actualiza `.sdlc/context.md` si existe ([context.md](context.md)), incluida la convención de IDs si es nueva.
6. **Handoffs** hechos y pendientes ([handoffs.md](handoffs.md#bloque-de-traza-en-la-entrega)).

## Modo Auditar

```markdown
# Auditoría <skill> — <alcance>

## Resumen
- Alcance: <documentos, módulos o carpeta revisados>
- Contexto: <tipo de producto, etapa (idea, MVP, en producción), interesados, convención de IDs detectada>
- Hallazgos: 🔴 n · 🟠 n · 🟡 n · 🔵 n · ℹ️ n
- Veredicto: <una o dos frases>

## Hallazgos

### [PR-<CÓDIGO>-001] <título>
- **Severidad:** HIGH — <justificación: coste × probabilidad de malentendido>
- **Ubicación:** `docs/…/archivo.md` § elemento (`RN-BUZ-003`) o ausencia concreta
- **Problema y escenario:** <qué se construiría mal o qué duda surgirá, y cuándo>
- **Evidencia:** <cita del texto, contradicción entre documentos, discrepancia con el código (archivo y símbolo)>
- **Corrección:** <redacción propuesta, regla completa, pregunta a resolver con quién>

## Lo que está bien
## Preguntas para el usuario
<lo que solo el usuario puede resolver, con el elemento afectado>
## Por verificar
## Fuera de alcance / otras skills
## Handoffs
- Hechos: <skill> (<alcance>) → <códigos>
- Pendientes: <skill> — <disparador y evidencia>
```

| Skill | Código |
| :--- | :--- |
| discovery | `PR-DISC` |
| elicitation | `PR-ELIC` |
| domain-modeling | `PR-DOMAIN` |

La numeración es siempre secuencial (`PR-DOMAIN-001`); no se inventan sufijos descriptivos.

## Veracidad de lo cargado (todas las entregas)

El anexo de referencias o skills aplicadas dice **exactamente** qué se leyó en esta sesión:

- ✅ solo para archivos **leídos completos**; ◐ con las líneas para lecturas parciales; ❌ con el motivo para lo no leído; n.a. si no existe.
- Una comprobación ("checklist aplicado: 0 hallazgos") solo se afirma si se cargó su `checklist.md`; si no, se escribe **"no aplicado"** y el motivo.
- "Inferido" o "por conocimiento general" no cuenta como aplicado: va como ❌ con esa nota.
- Lo que se dejó de cargar por coste aparece como ❌ (coste), no se omite.
- En auditorías de documentación, se listan los documentos del proyecto revisados con el mismo criterio: un `reglas_negocio.md` hojeado es ◐, no ✅.

## Handoffs en la entrega

Toda entrega termina con el bloque de handoffs hechos y pendientes de [handoffs.md](handoffs.md#bloque-de-traza-en-la-entrega). Si existe `.sdlc/context.md` ([context.md](context.md)), los pendientes se registran allí.
