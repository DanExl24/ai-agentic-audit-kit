# 📋 Checklist Forense — Design System, Estilos y Arquitectura UI

Ejecuta esta verificación punto por punto sobre el código visual:

---

### Dimensión 1: Higiene de Tokens y Temas
- [ ] **1.1. Erradicación de Valores Hardcodeados:**
  - ¿Todo color, padding, margin y tamaño tipográfico proviene de clases de utilidad Tailwind o variables CSS del tema?
  - ¿Hay colores hexadecimales (`#...`), `rgb()` o `hsl()` definidos directamente en atributos `style="..."` o archivos de componentes?
- [ ] **1.2. Integridad de Modo Oscuro / Claro:**
  - ¿Los textos en modo oscuro (`dark:...`) mantienen contraste y legibilidad con el fondo?
  - ¿Se evitan fondos oscuros fijos con textos oscuros fijos que se vuelvan invisibles al cambiar de tema?

---

### Dimensión 2: Arquitectura y Reutilización de Componentes
- [ ] **2.1. Componentes Base Primitivos:**
  - ¿Existen componentes atómicos reutilizables (`BaseButton`, `BaseInput`, `BaseModal`, `BaseBadge`, `BaseCard`) libres de lógica de negocio?
  - ¿Se reutilizan los componentes base en las vistas en lugar de duplicar etiquetas `<button>` o `<input>` con 15 clases Tailwind repetidas?
- [ ] **2.2. Estandarización de Variantes (CVA):**
  - ¿Las variantes (`primary`, `secondary`, `danger`, `outline`) y tamaños (`sm`, `md`, `lg`) están centralizados mediante un patrón de variantes predecible?

---

### Dimensión 3: Matriz Completa de Estados Interactivos
- [ ] **3.1. Cobertura de Estados:**
  - ¿Los botones y enlaces cuentan con estilos visuales explícitos para:
    - [ ] `hover` (cambio de tono o elevación sutil)
    - [ ] `active` (sensación táctil al presionar)
    - [ ] `focus-visible` (anillo de foco nítido)
    - [ ] `disabled` (cursor `not-allowed`, opacidad y prevención de clic)
    - [ ] `loading` (spinner visible sin cambiar el ancho ni altura del botón)
- [ ] **3.2. Estados de Entrada (Inputs):**
  - ¿Los inputs tienen estilos diferenciados para `default`, `focus`, `error` (borde rojo/alerta) y `disabled`?

---

### Dimensión 4: Resiliencia de Layout y Responsividad
- [ ] **4.1. Layout Widescreen y Contenedores:**
  - ¿La aplicación maneja pantallas ultra-anchas (Widescreen 100%) sin cajas flotando desarticuladas ni tablas colapsadas?
  - ¿Se previene el scroll horizontal involuntario en cualquier ancho de pantalla?
- [ ] **4.2. Textos Dinámicos Extremos:**
  - ¿Los nombres de usuario largos, correos o textos dinámicos tienen `truncate`, `line-clamp` o `break-words` para evitar romper las tarjetas o columnas de tablas?
- [ ] **4.3. Estabilidad Visual (Anti-CLS):**
  - ¿Las imágenes, avatares e íconos tienen dimensiones explícitas (`width`, `height`) o clases `aspect-ratio` para evitar saltos de layout durante la carga?

---

### Dimensión 5: Iconografía y Rendimiento Visual
- [ ] **5.1. Optimización de SVGs:**
  - ¿Se utiliza un sistema unificado de íconos en lugar de bloques masivos de SVG inline duplicados en cada iteración de tabla?
- [ ] **5.2. Aceleración por GPU en Animaciones:**
  - ¿Las transiciones visuales se limitan a propiedades económicas para la GPU (`transform`, `opacity`) evitando animar `height`, `width` o `top`?

---

### 🤝 Interacción con Accesibilidad
- [ ] Si detectas componentes compuestos interactivos (Dropdowns, Tabs, Modales, Drawers), anota en tu memo si carecen de atributos ARIA o foco para que **`05_accessibility_and_wcag`** realice la auditoría profunda.
