# 📋 Checklist Forense — Auditor de UI y Accesibilidad (WCAG 2.1 AA)

- [ ] **1. Semántica y Roles ARIA**
  - ¿Se utilizan elementos nativos (`<button>`, `<a>`, `<dialog>`) para acciones interactivas?
  - ¿Los íconos interactivos sin texto visible tienen `aria-label` descriptivo?
  - ¿Los íconos meramente decorativos tienen `aria-hidden="true"`?

- [ ] **2. Navegación por Teclado y Gestión de Foco**
  - ¿Existe un anillo de foco visible (`focus-visible`) al navegar con la tecla Tab?
  - Al abrir un modal, ¿el foco queda atrapado dentro y se cierra al presionar `Escape`?
  - Al cerrar un modal, ¿el foco regresa al elemento que lo activó?

- [ ] **3. Formularios y Notificaciones Dinámicas**
  - ¿Cada campo tiene un `<label>` asociado formalmente con `for`/`id`?
  - ¿Los errores de validación están vinculados mediante `aria-describedby` y `aria-invalid="true"`?
  - ¿Las alertas o toasts en pantalla usan `role="alert"` o `aria-live="polite"`?

- [ ] **4. Contraste y Tokens de Diseño**
  - ¿El contraste entre texto y fondo cumple el ratio mínimo de 4.5:1?
  - ¿Todos los colores y tipografías derivan de tokens semánticos (Tailwind / CSS Variables) sin valores hexadecimales hardcodeados?
