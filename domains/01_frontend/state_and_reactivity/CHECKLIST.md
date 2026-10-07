# 📋 Checklist Forense — Auditor de Estado y Reactividad

Ejecuta esta verificación punto por punto:

- [ ] **1. Limpieza de Efectos y Suscripciones (Memory Leaks)**
  - ¿Todo `addEventListener`, `setInterval`, `setTimeout` o `WebSocket` tiene su respectivo `removeEventListener` / `clearInterval` / `disconnect` al desmontarse la vista?
  - ¿Hay suscripciones a RxJS o listeners globales que queden huérfanos al navegar?

- [ ] **2. Integridad de Reactividad**
  - En Vue: ¿Se desestructuran props o objetos reactivos perdiendo su reactividad nativa?
  - En React: ¿Se crean funciones u objetos inline en el renderizado que invaliden `React.memo` en componentes hijos?
  - ¿Existen mutaciones directas de arrays o estados reactivos sin usar inmutabilidad o métodos reactivos (`push` directo vs spread)?

- [ ] **3. Higiene del Store Global**
  - ¿El store global almacena solo datos compartidos entre múltiples vistas no jerárquicas?
  - ¿Los estados de formularios o modales están confinados al estado local del componente (`ref`, `useState`)?
  - ¿Hay selectores o computed properties costosas recalculándose en cada render?

- [ ] **4. Manejo de Concurrencia y Carrera Asíncrona**
  - En campos de búsqueda con autocompletado, ¿se usa debounce o `AbortController` para cancelar requests obsoletos?
  - ¿Se manejan adecuadamente estados de `isLoading`, `isError` y `isEmpty` de forma explícita?
