# 🛑 Protocolo de Veto y Devolución Inter-Agente (Peer Rejection Protocol)

> **Mecanismo de Control de Calidad Horizontal.**  
> Ningún especialista está obligado a trabajar sobre entregables deficientes, ambiguos o desorganizados. Todo agente receptor tiene la **autoridad y el mandato explícito de frenar la línea y devolver el trabajo** al agente emisor.

---

## 1. Criterios de Devolución Obligatoria (Triggers de Veto)

Un agente receptor DEBE rechazar el entregable si ocurre cualquiera de los siguientes escenarios:
1. **Falta de Evidencia:** El emisor afirma que algo falla o que algo está bien, pero no proporciona rutas de archivo ni números de línea.
2. **Ambigüedad en el Alcance:** No queda claro qué archivos fueron realmente inspeccionados y cuáles quedaron fuera.
3. **Puntos Ciegos Ignorados:** El emisor pasó por alto advertencias evidentes de su propio checklist.
4. **Desorden o Falta de Estructura:** El entregable no respeta la plantilla canónica `INTER_AGENT_HANDOFF_MEMO.md`.

---

## 2. Formato Estándar del Veto

Cuando un agente rechaza una entrega, debe emitir el siguiente dictamen público:

```markdown
# 🛑 RECHAZO DE ENTREGABLE (VETO INTER-AGENTE)

- **Agente que ejerce el Veto:** [ui_ux_experience/01_senior_design_critic | engineering/02_state_and_reactivity | engineering/03_forms_and_data_flow | engineering/04_design_system_and_styling | engineering/05_accessibility_and_wcag | 00_frontend_director]
- **Agente Devuelto:** [ui_ux_experience/01_senior_design_critic | engineering/01_arch_and_network | engineering/02_state_and_reactivity | engineering/03_forms_and_data_flow | engineering/04_design_system_and_styling]
- **Módulo Afectado:** `ruta/del/modulo`
- **Estado de la Cadena:** ⏸️ STOP THE LINE (Pausada hasta subsanación)

---

### 1. Veredicto del Rechazo
"El análisis entregado por el Agente Emisor es insuficiente / incompleto / desorganizado para poder realizar mi auditoría de forma rigurosa y transparente."

### 2. Deficiencias Específicas Detectadas (Hallazgos Faltantes)
1. **[Deficiencia 1]:** [Explicación detallada de lo que falta o está mal sustentado].
2. **[Deficiencia 2]:** [Explicación detallada].

### 3. Puntos Obligatorios a Subsanar por el Agente Emisor
Para que este entregable sea aceptado en segunda ronda, el Agente Emisor debe:
- [ ] Acción requerida 1 (ej. auditar el archivo `apiClient.ts` y documentar sus interceptores con número de línea).
- [ ] Acción requerida 2 (ej. clasificar los hallazgos según la escala de severidad canónica).

---
*Nota: La cadena de auditoría no avanzará hacia mi rol hasta que el Agente Emisor vuelva a entregar el memo corregido.*
```

---

## 3. Resolución del Conflicto (Arbitraje)

1. **Ciclo de Subsanación Directa:** El agente emisor toma los puntos requeridos, reabre su auditoría y emite una versión corregida `v2` del memo.
2. **Intervención del Director:** Si tras 2 intentos persiste el desacuerdo, el **`00_frontend_director`** interviene como árbitro final, decidiendo si el análisis es aceptado o si reasigna la auditoría con pautas explícitas.
