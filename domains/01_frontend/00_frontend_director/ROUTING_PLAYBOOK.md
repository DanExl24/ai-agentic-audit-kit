# 🧭 Manual de Enrutamiento y Rutas de Auditoría (Frontend Routing Playbook)

> **Manual Rector del `00_frontend_director` para coordinar el Escuadrón de Frontend:**  
> Divide el dominio en dos vertientes: **Experiencia y Crítica Visual (CERO CÓDIGO)** vs **Ingeniería e Implementación Técnica (CÓDIGO)**.

---

## 🗂️ Las Dos Vertientes del Dominio Frontend

```mermaid
flowchart TD
    DIR["👑 00_frontend_director<br/>(Director Rector del Dominio)"]

    subgraph "Vertiente A: UI/UX & Experiencia (CERO CÓDIGO)"
        UX["👁️ ui_ux_experience/01_senior_design_critic<br/>(Psicología Visual, Fatiga, 10 Viewports, Before vs After)"]
    end

    subgraph "Vertiente B: Engineering & Implementación (CÓDIGO)"
        E1["🏗️ engineering/01_arch_and_network"]
        E2["🧠 engineering/02_state_and_reactivity"]
        E3["📝 engineering/03_forms_and_data_flow"]
        E4["🎨 engineering/04_design_system_and_styling"]
        E5["♿ engineering/05_accessibility_and_wcag"]
    end

    DIR -->|Revisión de Producto/UX| UX
    DIR -->|Revisión de Código/Técnica| E1
    UX ==>|"Propuestas de Rediseño Before vs After"| E4
    UX ==>|"Simplificación de Flujos de Formulario"| E3
    E4 <-->|"Memo Bimodal"| E5

    style DIR fill:#003366,stroke:#38bdf8,color:#ffffff,stroke-width:2px
    style UX fill:#7c2d12,stroke:#f97316,color:#ffffff,stroke-width:2px
    style E1 fill:#1e293b,stroke:#94a3b8,color:#ffffff
    style E2 fill:#1e293b,stroke:#94a3b8,color:#ffffff
    style E3 fill:#1e293b,stroke:#94a3b8,color:#ffffff
    style E4 fill:#1e293b,stroke:#94a3b8,color:#ffffff
    style E5 fill:#1e293b,stroke:#94a3b8,color:#ffffff
```

---

## 🛣️ Rutas de Ejecución Predefinidas

### Ruta 0: "Auditoría de Producto y Experiencia Integral (UX-First Full Audit)"
* **Secuencia de Cadena:**
  ```text
  1. ui_ux_experience/01_senior_design_critic (Evalúa interfaz en 10 resoluciones, fatiga, jerarquía y Before vs After)
         ↓ (Handoff de Diseño a Código)
  2. engineering/01_arch_and_network (Cimientos de carpetas y cliente de red)
         ↓ (Handoff Memo)
  3. engineering/02_state_and_reactivity (Stores y reactividad)
         ↓ (Handoff Memo)
  4. engineering/03_forms_and_data_flow (Implementación de formularios simplificados)
         ↓ (Handoff Memo)
  5. engineering/04_design_system_and_styling (Ajuste de tokens, variantes y componentes base)
         ↓ (Handoff Memo)
  6. engineering/05_accessibility_and_wcag (Certificación de lectores de pantalla y teclado)
  ```
* **Cuándo activarla:** Para auditorías completas de nuevas funcionalidades donde importa tanto la usabilidad humana como la solidez técnica del software.

---

### Ruta 1: "Crítica Pura de UI/UX y Mobile (Zero-Code Design Critique)"
* **Secuencia de Cadena:**
  ```text
  ui_ux_experience/01_senior_design_critic (Ejecución Aislada Rápida)
  ```
* **Cuándo activarla:**
  - Cuando el cliente o equipo dice: *"La pantalla se ve anticuada, incómoda o el teléfono muestra todo apretado"*.
  - Cuando necesitas evaluar las 10 resoluciones de pantalla (320px a 1920px) sin perder tiempo leyendo código TypeScript.
  - Para obtener el informe *Before vs After* y roadmap P0-P3 de rediseño.

---

### Ruta 2: "Crisis de Rendimiento y Memoria (Performance Crisis)"
* **Secuencia de Cadena:**
  ```text
  engineering/02_state_and_reactivity ➔ engineering/04_design_system_and_styling
  ```
* **Cuándo activarla:** Pestaña congelada, memory leaks o animaciones CSS que saturan la GPU.

---

### Ruta 3: "Flujo de Formularios y Captura (Data Input Flow)"
* **Secuencia de Cadena:**
  ```text
  engineering/01_arch_and_network ➔ engineering/03_forms_and_data_flow
  ```
* **Cuándo activarla:** Errores de envío, validaciones Zod rotas o doble clic accidental.

---

### Ruta 4: "Dúo Visual & Inclusivo (Design System + Certificación WCAG)"
* **Secuencia de Cadena (Bimodal Complementaria):**
  ```text
  engineering/04_design_system_and_styling ⇄ engineering/05_accessibility_and_wcag
  ```
* **Cuándo activarla:** Auditoría técnica de tokens, estados interactivos y cumplimiento de accesibilidad legal.

---

## ⚖️ Criterios de Selección Rápida

| Requerimiento del Usuario | Ruta Recomendada | Enfoque Principal |
| :--- | :---: | :--- |
| "Audita la experiencia, el diseño y dime si es cómodo en teléfonos" | **Ruta 1** (UI/UX Pure Critique) | 👁️ Cero código, 10 viewports, fatiga visual. |
| "Revisa este nuevo módulo de principio a fin (diseño + código)" | **Ruta 0** (UX-First Full Audit) | 🌟 Producto + Ingeniería completa. |
| "La pestaña se congela o consume 2GB de RAM" | **Ruta 2** (Performance Crisis) | ⚙️ Stores, memory leaks y GPU. |
| "El formulario no guarda o se envían datos erróneos" | **Ruta 3** (Data Input Flow) | ⚙️ Zod, submit y endpoints. |
| "Audita tokens, temas y conformidad de accesibilidad WCAG" | **Ruta 4** (Dúo Visual & A11y) | 🎨 Tokens, teclado y lectores de pantalla. |
