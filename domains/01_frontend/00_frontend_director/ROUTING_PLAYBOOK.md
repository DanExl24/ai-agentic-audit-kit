# 🧭 Manual de Enrutamiento y Rutas de Auditoría (Frontend Routing Playbook)

Este manual define las rutas de ejecución estándar que el **`00_frontend_director`** debe seleccionar según el requerimiento del usuario, contemplando al escuadrón completo de 5 especialistas:

---

## 🛣️ Rutas de Ejecución Predefinidas

### Ruta 1: "Auditoría Completa de un Módulo o Vista (Full Feature Enterprise Audit)"
* **Secuencia de Cadena:**
  ```text
  01_arch_and_network
         ↓ (Handoff Memo)
  02_state_and_reactivity
         ↓ (Handoff Memo)
  03_forms_and_data_flow
         ↓ (Handoff Memo)
  04_design_system_and_styling
         ↓ (Handoff Memo)
  05_accessibility_and_wcag
  ```
* **Objetivo:** Radiografía 360° de una pantalla o módulo completo. Asegura cimientos de red, reactividad sin leaks, formularios seguros, arquitectura visual estricta y conformidad legal de accesibilidad WCAG.

---

### Ruta 2: "Rendimiento, Congelamiento y Fugas de Memoria (Performance Crisis)"
* **Secuencia de Cadena:**
  ```text
  02_state_and_reactivity ➔ (Handoff Memo) ➔ 04_design_system_and_styling (evalúa repaints, CLS y GPU animations)
  ```
* **Objetivo:** Detectar render loops infinitos, fugas de memoria en desmontaje, mutaciones descontroladas de stores y animaciones CSS costosas.

---

### Ruta 3: "Fallos de Entrada, Formularios y Envío de Datos (Data Input Flow)"
* **Secuencia de Cadena:**
  ```text
  01_arch_and_network (verifica endpoints y tipos DTO) ➔ (Handoff Memo) ➔ 03_forms_and_data_flow (valida Zod y submit)
  ```
* **Objetivo:** Solucionar errores de envío, estados de carga ausentes, validaciones rotas y prevención de doble submit.

---

### Ruta 4: "Dúo Visual & Inclusivo (Design System + Certificación WCAG)"
* **Secuencia de Cadena (Bimodal Complementaria):**
  ```text
  04_design_system_and_styling ⇄ (Handoff Bimodal) ⇄ 05_accessibility_and_wcag
  ```
* **Objetivo:** Auditoría exhaustiva de la capa de interfaz. `04` audita tokens, variantes, estados interactivos y responsividad; `05` audita navegación por teclado, focus traps, lectores de pantalla y contraste. Si `05` detecta violación de contraste o touch target, `04` ajusta el token en el sistema de diseño.

---

### Ruta 5: "Certificación Forense de Accesibilidad Aislada (A11y Fast Track)"
* **Secuencia de Cadena:**
  ```text
  05_accessibility_and_wcag (Auditoría Quirúrgica Aislada)
  ```
* **Objetivo:** Revisar cumplimiento estricto WCAG 2.1 / 2.2 AA ante auditorías legales o certificaciones de accesibilidad.

---

## ⚖️ Criterios de Selección Rápida

| Requerimiento del Usuario | Ruta Recomendada | Tiempo Estimado |
| :--- | :---: | :---: |
| "Revisa este nuevo módulo que acabamos de programar" | **Ruta 1** (Full Feature) | Exhaustivo |
| "La pestaña se congela o consume 2GB de RAM" | **Ruta 2** (Performance) | Rápido y Focalizado |
| "El formulario no guarda o se envían datos erróneos" | **Ruta 3** (Data Input) | Quirúrgico |
| "Revisa el diseño, los componentes y la accesibilidad" | **Ruta 4** (Dúo Visual & A11y) | Profundo |
| "Certifica si esta pantalla cumple la norma WCAG" | **Ruta 5** (A11y Fast Track) | Quirúrgico |
