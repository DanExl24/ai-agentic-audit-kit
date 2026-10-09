# 📋 Checklist Forense — Senior UI/UX Designer & Design Critic

Ejecuta esta evaluación desde la perspectiva del usuario final (CERO ANÁLISIS DE CÓDIGO TÉCNICO):

---

### Dimensión 1: Jerarquía Visual y Foco de Atención
- [ ] **1.1. Primer Impacto:** ¿Qué elemento atrae la mirada en los primeros 3 segundos? ¿Es el elemento principal o un elemento decorativo/irrelevante?
- [ ] **1.2. Competencia Visual:** ¿Existen múltiples botones primarios o tarjetas del mismo color que compiten agresivamente entre sí?
- [ ] **1.3. Subordinación:** ¿Los títulos, subtítulos y datos secundarios están claramente diferenciados por tamaño, peso y color?
- [ ] **1.4. Ley de Von Restorff:** ¿La acción principal deseada (CTA) es inconfundible respecto a las acciones secundarias o destructivas?

---

### Dimensión 2: Densidad de Información y Ergonomía Cognitiva
- [ ] **2.1. Fatiga Visual:** ¿La pantalla agobia al usuario con un exceso de cards, widgets o números simultáneos?
- [ ] **2.2. Ratio Señal/Ruido:** ¿Cada elemento en pantalla aporta valor real o hay decoraciones innecesarias?
- [ ] **2.3. Espaciado y Respiración:** ¿El padding y gap permiten una lectura descansada o los elementos se sienten comprimidos y asfixiados?

---

### Dimensión 3: Coherencia del Sistema Visual
- [ ] **3.1. Semántica del Color:** ¿Los colores comunican significado (éxito, alerta, peligro, estado) o se usan arbitrariamente "porque se ven bonitos"?
- [ ] **3.2. Armonía Cromática:** ¿La combinación de colores es profesional y agradable o chillona y desgastante?
- [ ] **3.3. Tipografía y Escaneo:** ¿Se lee cómodamente el texto largo? ¿El line-height permite un escaneo vertical rápido?
- [ ] **3.4. Consistencia de Bordes y Formas:** ¿Los radios de esquina (border-radius) y sombras son uniformes en todo el producto?

---

### Dimensión 4: Auditoría Responsive en las 10 Resoluciones Físicas
- [ ] **4.1. Mobile Ultra-compacto (320 × 720 / 375 × 812):**
  - ¿Los textos se rompen o desbordan la pantalla?
  - ¿Los botones tienen un área táctil cómoda de mínimo 44×44px?
  - ¿Se puede usar con una sola mano sin forzar el pulgar?
- [ ] **4.2. Mobile Estándar y Grande (390 × 844 / 414 × 896):**
  - ¿El contenido se reorganiza verticalmente o solo se hace más pequeño?
  - ¿El sidebar se transforma en un Drawer lateral o barra inferior cómoda?
- [ ] **4.3. Tablet (768 × 1024 / 1024 × 768):**
  - ¿Se aprovecha el ancho adicional con grids de 2 columnas o se deja un vacío gigante?
- [ ] **4.4. Desktop y Widescreen (1280 × 720 / 1366 × 768 / 1440 × 900 / 1920 × 1080):**
  - ¿La interfaz aprovecha el espacio panorámico de forma equilibrada o se estira grotescamente?

---

### Dimensión 5: Tablas de Datos en Mobile
- [ ] **5.1. Rechazo a 'overflow-x: auto' perezoso:** ¿Se obliga al usuario móvil a arrastrar horizontalmente 8 columnas para ver un dato?
- [ ] **5.2. Alternativa Ergonómica:** ¿La tabla en mobile se convierte en tarjetas (Cards) verticales con acordeón expandible para ver detalles?
- [ ] **5.3. Acciones Accesibles:** ¿Los botones de acción (editar, ver, borrar) están al alcance inmediato sin desplazarse?

---

### Dimensión 6: Formularios desde la Perspectiva de UX
- [ ] **6.1. Etiquetas Permanentes:** ¿Los campos tienen labels visibles para que el usuario no olvide qué escribe tras rellenar el campo?
- [ ] **6.2. Agrupación Lógica:** ¿Los campos están organizados en bloques temáticos (ej. Información Personal vs Facturación)?
- [ ] **6.3. Longitud y Wizards:** Si el formulario supera los 8 campos, ¿está dividido en pasos (Wizard) para reducir la fricción inicial?
- [ ] **6.4. Claridad en Errores:** ¿Los mensajes de error dicen exactamente qué falló y cómo solucionarlo?

---

### Dimensión 7: Estados Visuales de Interfaz
- [ ] **7.1. Estados Vacíos (Empty States):** ¿Cuando no hay datos se muestra una pantalla en blanco o un mensaje cordial con botón de acción ("Crear primer registro")?
- [ ] **7.2. Estados de Carga (Loading Skeletons):** ¿Se usan skeletons que imitan la forma del contenido real en lugar de spinners genéricos?
- [ ] **7.3. Confirmaciones y Alertas:** ¿Las acciones destructivas (borrar) tienen advertencias claras con botones de color diferencial?

---

### Dimensión 8: Flujos de Usuario y Fricción (User Flows)
- [ ] **8.1. Clics Innecesarios:** ¿Se puede completar la tarea en menos de 3 pasos?
- [ ] **8.2. Context Switching:** ¿El usuario tiene que salir de la pantalla para consultar un dato que podría mostrarse en un tooltip o panel lateral?
- [ ] **8.3. Before vs After:** ¿Existe una propuesta concreta de rediseño para cada problema crítico detectado?
