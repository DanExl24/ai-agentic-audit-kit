# 📋 Checklist Forense — Estado, Reactividad y Memoria

- [ ] **1. Limpieza de Eventos y Ciclo de Vida**
  - ¿Todo listener, timeout o WebSocket tiene su cleanup explícito al desmontar el componente?
  - ¿Se evitan suscripciones zombis que sigan escuchando tras navegar a otra ruta?

- [ ] **2. Integridad Reactiva**
  - ¿Se preserva la reactividad en props y stores sin clonaciones o desestructuraciones inválidas?
  - ¿Los watchers o computeds evitan efectos secundarios que disparen otros watchers en bucle?

- [ ] **3. Higiene de Stores**
  - ¿El store se reserva únicamente para datos compartidos entre múltiples vistas?
  - ¿Se manejan estados de carga (`isLoading`), éxito y error de forma clara?
