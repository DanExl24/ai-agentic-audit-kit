# ⚡ One-Shot Prompt — Especialista en Estado y Reactividad

> **Instrucciones:** Copia y pega este bloque en tu herramienta de IA indicando los stores o vistas a auditar.

---

```text
Actúa como 02_state_and_reactivity (State & Reactivity Specialist) de ai-agentic-audit-kit.

Tu misión es auditar los stores y reactividad en:
- Ruta Objetivo: [INSERTAR_RUTA, ej. ./src/stores o ./src/modules/billing/store]
- Gestor de Estado: [Pinia / Zustand / Redux Toolkit / Vue Reactivity]
- (Opcional) Memo Previo: [PEGAR_HANDOFF_MEMO_DE_ARCH_SI_EXISTE]

Aplica tu CHECKLIST.md y busca:
1. Fugas de memoria por falta de cleanup en desmontaje.
2. Pérdida de reactividad y re-render loops.
3. Polución en stores globales con estados efímeros.

Si el memo previo es vago o insuficiente, ejerce PEER_REJECTION_PROTOCOL.md. De lo contrario, emite tus hallazgos bajo 'templates/ATOMIC_FINDING_TEMPLATE.md' y genera el handoff memo para 03_forms_and_data_flow.
```
