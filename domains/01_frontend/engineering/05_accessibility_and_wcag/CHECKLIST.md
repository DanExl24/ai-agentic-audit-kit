# 📋 Checklist Forense — Accesibilidad Web y Conformidad WCAG 2.1/2.2 AA

Ejecuta esta auditoría estricta verificando cada criterio contra el código fuente:

---

### Dimensión 1: Navegabilidad por Teclado y Foco
- [ ] **1.1. Operabilidad Exclusiva por Teclado (WCAG 2.1.1):**
  - ¿Todas las funciones (abrir menús, enviar formularios, paginar tablas, accionar modales) son ejecutables sin tocar el ratón?
  - ¿Se evitan eventos exclusivos de ratón (`@mouseenter`, `onMouseOver`) sin su equivalente de teclado (`@focus`, `onFocus`)?
- [ ] **1.2. Sin Trampas de Teclado (WCAG 2.1.2):**
  - ¿Se puede entrar y salir libremente de cualquier componente interactivo usando Tab / Shift+Tab?
- [ ] **1.3. Anillo de Foco Visible y Nítido (WCAG 2.4.7):**
  - ¿Existe un contorno de foco visual explícito (`focus-visible:ring-...` o `outline`)?
  - ¿Se eliminó algún `outline: none` o `outline-none` sin proveer un reemplazo visual contrastante?
- [ ] **1.4. Gestión de Foco en Modales y Diálogos:**
  - ¿El foco queda confinado (*Focus Trap*) dentro del modal mientras esté abierto?
  - ¿Presionar la tecla `Escape` cierra inmediatamente el modal o drawer?
  - ¿Al cerrarse, el foco regresa al botón o enlace exacto que lo abrió (*Focus Restoration*)?

---

### Dimensión 2: Semántica HTML5 y Estructura ARIA
- [ ] **2.1. Elementos Nativos vs 'Div Soup':**
  - ¿Las acciones interactivas usan `<button>` y los enlaces de navegación usan `<a href="...">`?
  - ¿Se erradicaron etiquetas `<div @click="...">` o `<span onClick="...">` sin rol ni accesibilidad nativa?
- [ ] **2.2. Jerarquía de Encabezados (WCAG 1.3.1):**
  - ¿La página tiene exactamente un `<h1>` que describe el contenido principal?
  - ¿Los encabezados siguen un orden jerárquico lógico (`h1` ➔ `h2` ➔ `h3`) sin saltos arbitrarios?
- [ ] **2.3. Roles y Atributos ARIA Dinámicos:**
  - ¿Los componentes desplegables usan `aria-expanded="true/false"`?
  - ¿Los íconos interactivos sin texto visible tienen `aria-label` descriptivo?
  - ¿Los íconos meramente decorativos tienen `aria-hidden="true"`?
  - ¿Los sistemas de pestañas implementan el patrón ARIA `tablist` ➔ `tab` (con `aria-selected`) ➔ `tabpanel`?

---

### Dimensión 3: Contraste Cromático y Color
- [ ] **3.1. Ratio de Contraste de Texto (WCAG 1.4.3):**
  - ¿El texto normal tiene un ratio de contraste mínimo de **4.5:1** respecto a su fondo?
  - ¿El texto grande (≥ 18pt o ≥ 14pt negrita) cumple al menos **3:1**?
  - ¿El contraste se mantiene legible tanto en Modo Claro como en Modo Oscuro?
- [ ] **3.2. Contraste de Elementos de Interfaz (WCAG 1.4.11):**
  - ¿Los bordes de campos de entrada, botones y checkboxes tienen contraste mínimo de **3:1** con el fondo?
- [ ] **3.3. No Dependencia Exclusiva del Color (WCAG 1.4.1):**
  - ¿Los mensajes de error, estados de éxito o alertas incluyen íconos o texto aclaratorio, y no dependen únicamente del cambio de color?

---

### Dimensión 4: Formularios y Prevención de Errores
- [ ] **4.1. Etiquetas de Entrada (WCAG 3.3.2):**
  - ¿Todo `<input>`, `<select>` y `<textarea>` tiene su respectivo `<label>` enlazado mediante `for` e `id`?
  - Si un campo no tiene etiqueta visual por diseño, ¿tiene `aria-label` explícito?
- [ ] **4.2. Notificación de Errores (WCAG 3.3.1):**
  - ¿Los mensajes de error en línea están asociados al input mediante `aria-describedby="[id-del-error]"`?
  - ¿El input en estado de error incluye `aria-invalid="true"`?

---

### Dimensión 5: Regiones Activas y Cambios Dinámicos
- [ ] **5.1. Anuncios Dinámicos (WCAG 4.1.3):**
  - ¿Las alertas dinámicas, toasts o notificaciones flotantes tienen `role="status"` o `aria-live="polite"`?
  - ¿Los errores críticos o bloqueantes usan `role="alert"` o `aria-live="assertive"`?

---

### Dimensión 6: Pantallas Táctiles y Movimiento
- [ ] **6.1. Tamaño Mínimo de Toque (WCAG 2.2 Criterio 2.5.8):**
  - ¿Los botones y controles táctiles en móvil tienen un área mínima de **24x24px** (o idealmente **44x44px**)?
- [ ] **6.2. Reducción de Movimiento (WCAG 2.3.3):**
  - ¿Las animaciones y transiciones respetan `@media (prefers-reduced-motion: reduce)`?

---

### 🤝 Interacción con Design System
- [ ] Si detectas problemas de contraste de color o tamaños táctiles deficientes, emite una nota en tu memo para **`04_design_system_and_styling`** solicitando el ajuste del token de color o el padding del componente base.
