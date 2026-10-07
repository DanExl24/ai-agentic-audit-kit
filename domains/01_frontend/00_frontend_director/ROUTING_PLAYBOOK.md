# 🧭 Manual de Enrutamiento y Rutas de Auditoría (Frontend Routing Playbook)

Este manual define las rutas de ejecución estándar que el **`00_frontend_director`** debe seleccionar según el requerimiento del usuario:

---

## 🛣️ Rutas de Ejecución Predefinidas

### Ruta 1: "Auditoría Completa de un Módulo o Vista (Full Feature Audit)"
* **Secuencia de Cadena:**
  ```text
  01_arch_and_network ➔ (Handoff Memo) ➔ 02_state_and_reactivity ➔ (Handoff Memo) ➔ 03_forms_and_data_flow ➔ (Handoff Memo) ➔ 04_ui_design_and_a11y
  ```
* **Objetivo:** Radiografía 360° de una pantalla o módulo completo. Asegura que la arquitectura de red, el estado, la entrada de datos y la presentación visual cumplan estándares de producción.

---

### Ruta 2: "Rendimiento, Congelamiento y Fugas de Memoria (Performance Crisis)"
* **Secuencia de Cadena:**
  ```text
  02_state_and_reactivity ➔ (Handoff Memo si hay problemas de render) ➔ 04_ui_design_and_a11y
  ```
* **Objetivo:** Detectar render loops infinitos, fugas de memoria en desmontaje, mutaciones descontroladas de stores y cálculos pesados sin memoización.

---

### Ruta 3: "Fallos de Entrada, Formularios y Envío de Datos (Data Input Flow)"
* **Secuencia de Cadena:**
  ```text
  01_arch_and_network (verifica endpoints y tipos DTO) ➔ (Handoff Memo) ➔ 03_forms_and_data_flow (valida Zod y submit)
  ```
* **Objetivo:** Solucionar errores de envío, estados de carga ausentes, validaciones rotas y prevención de doble submit.

---

### Ruta 4: "Certificación de Accesibilidad y Design System (A11y Release Gate)"
* **Secuencia de Cadena:**
  ```text
  04_ui_design_and_a11y (Auditoría Quirúrgica Aislada)
  ```
* **Objetivo:** Verificar conformidad con WCAG 2.1 AA (contraste, foco por teclado, roles ARIA) y apego estricto a los tokens del sistema de diseño.

---

## ⚖️ Criterios de Selección Rápida

| Requerimiento del Usuario | Ruta Recomendada | Tiempo Estimado |
| :--- | :---: | :---: |
| "Revisa este nuevo módulo que acabamos de programar" | **Ruta 1** (Full Feature) | Exhaustivo |
| "La pestaña se congela o consume 2GB de RAM" | **Ruta 2** (Performance) | Rápido y Focalizado |
| "El formulario no guarda o se envían datos erróneos" | **Ruta 3** (Data Input) | Quirúrgico |
| "Audita la accesibilidad y los estilos de estos componentes" | **Ruta 4** (A11y & Design) | Quirúrgico |
