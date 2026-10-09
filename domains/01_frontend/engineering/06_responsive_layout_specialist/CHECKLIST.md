# 📋 Checklist de Auditoría y Corrección Responsive

> **Guía técnica forense para verificar la resiliencia espacial y adaptación de pantallas en código (Tailwind CSS / Vue 3 / CSS)**

---

## 📐 1. Matriz de los 13 Viewports Obligatorios

| # | Viewport | Categoría | ¿Sin overflow global? | ¿Texto legible? | ¿Botones accesibles? | Estado |
| :-: | :--- | :--- | :-: | :-: | :-: | :-: |
| 1 | `320 × 568` | Mobile ultra-compacto | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 2 | `360 × 640` | Mobile Android estándar | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 3 | `375 × 667` | Mobile clásico (iPhone SE) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 4 | `390 × 844` | Mobile moderno base | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 5 | `414 × 896` | Mobile grande / Max | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 6 | `768 × 1024` | Tablet vertical (`md:`) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 7 | `820 × 1180` | Tablet intermedia (iPad Air) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 8 | `1024 × 768` | Tablet horizontal (`lg:`) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 9 | `1280 × 720` | Laptop compacta (altura 720) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 10 | `1366 × 768` | Laptop estándar corporativa | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 11 | `1440 × 900` | Laptop widescreen (`xl:`) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 12 | `1600 × 900` | Desktop estándar | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |
| 13 | `1920 × 1080` | Desktop FHD (`2xl:`) | [ ] | [ ] | [ ] | [ ] Pasa / [ ] Falla |

---

## 🧱 2. Layout, Contenedores y Cajas

- [ ] **Ausencia de anchos fijos rígidos:** Ningún contenedor principal tiene clases como `w-[900px]` o `width: 850px` sin `max-w-full`.
- [ ] **Contención elástica:** Los contenedores principales usan `w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8`.
- [ ] **Flexbox resiliente:** Los contenedores `flex` con múltiples elementos tienen `flex-wrap` cuando el ancho disminuye, o cambian a `flex-col md:flex-row`.
- [ ] **Prevención de compresión flex:** Elementos que no deben aplastarse (badges, iconos, avatars) cuentan con `shrink-0`.
- [ ] **Gaps proporcionales:** El espaciado entre tarjetas escala progresivamente (`gap-3 sm:gap-4 lg:gap-6`).
- [ ] **Cero scroll horizontal en `body`:** La barra de desplazamiento horizontal de la ventana completa NUNCA aparece (`overflow-x: hidden` en wrapper global como salvaguarda, pero resolviendo la causa raíz).

---

## 📊 3. Tablas y Datos Tabulares

- [ ] **Aislamiento de desborde tabular:** Toda tabla está envuelta en un contenedor con `w-full overflow-x-auto`.
- [ ] **Independencia del viewport:** Al desplazarse horizontalmente la tabla, los headers y sidebars de la aplicación se mantienen estáticos.
- [ ] **Encabezados claros:** Los encabezados (`<th>`) tienen `whitespace-nowrap` o anchos mínimos para no deformar los títulos.
- [ ] **Columna de acciones asegurada:** La columna de botones de acción permanece accesible o visible al final del scroll horizontal.
- [ ] **Preservación del formato tabular:** No se destruyó la tabla para convertirla forzosamente en tarjetas a menos que fuera explícitamente requerido.

---

## 🪟 4. Modales, Drawers y Overlays

- [ ] **Límite de altura vertical:** Todo modal tiene `max-h-[90vh]` o `max-h-[85vh]` para caber holgadamente en `1366×768` y `1280×720`.
- [ ] **Estructura flex interna:** El modal implementa `flex flex-col`:
  - Header: `flex-shrink-0`
  - Body: `flex-1 overflow-y-auto`
  - Footer: `flex-shrink-0 border-t`
- [ ] **Acciones siempre visibles:** Los botones "Guardar" y "Cancelar" nunca quedan enterrados debajo del fold de la pantalla ni fuera del viewport.
- [ ] **Ancho adaptable:** En pantallas móviles (`<640px`) el modal ocupa `w-full mx-2 sm:max-w-lg`.

---

## 📝 5. Formularios y Filtros

- [ ] **Columnado progresivo:** Formularios con múltiples campos usan `grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4`.
- [ ] **Campos relacionados respetados:** Inputs vinculados (ej. Tipo de Documento + Número) no se separan de manera extraña en tablet.
- [ ] **Inputs y botones full-width en móvil:** En pantallas menores a `640px`, los botones primarios ocupan `w-full` o se apilan verticalmente si colisionan.
- [ ] **Barra de filtros elástica:** Filtros de búsqueda con múltiples selects se adaptan con `flex-wrap gap-2` o `grid` sin desbordar el header.

---

## 📈 6. Dashboards, KPIs y Gráficos

- [ ] **Grid adaptativo de métricas:** Los KPIs no generan scroll horizontal; transicionan fluidamente (`grid-cols-1 sm:grid-cols-2 lg:grid-cols-4`).
- [ ] **Redimensionamiento de gráficos:** Los contenedores de gráficos (ECharts, Canvas, SVG) tienen `w-full` y escuchan eventos de redimensionamiento sin desbordar su tarjeta contenedora.
- [ ] **Alturas controladas:** Los gráficos tienen alturas proporcionales (`h-64 sm:h-80 md:h-96`) evitando colapsar a 0px o expandirse infinitamente.

---

## 🔤 7. Textos, Tipografía y Botones

- [ ] **Nombres largos seguros:** Textos que reciben datos dinámicos (nombres de instituciones, estudiantes, correos) tienen `break-words` para evitar romper cajas.
- [ ] **Truncamiento responsable:** Si se usa `truncate`, es en columnas donde el texto no es crítico o cuenta con tooltip accesible.
- [ ] **Tamaño táctil de botones:** En pantallas táctiles (`<1024px`), los botones interactivos miden como mínimo `min-h-[40px]` o `min-h-[44px]`.
- [ ] **Botones en headers:** En títulos con botones a la derecha (`flex justify-between`), se aplica `flex-col sm:flex-row sm:items-center gap-3` para que el botón no aplaste el título.

---

## 🧭 8. Header, Sidebar y Shell de Aplicación

- [ ] **Sidebar colapsable:** En pantallas `<1024px` (`lg:`), el sidebar se oculta o se convierte en drawer deslizable para no consumir el 40% del ancho útil.
- [ ] **Contenido principal holgado:** En resoluciones de tablet (`768px - 1024px`), el área de trabajo central dispone de espacio cómodo para interactuar.
- [ ] **Header institucional resiliente:** Si el nombre del colegio o usuario es muy largo, no oculta las notificaciones ni el avatar.

---

## 🛡️ 9. Verificación de No-Rediseño (Gobernanza)

- [ ] **Colores intactos:** ¿Se mantuvieron exactamente los mismos tokens y clases de color originales?
- [ ] **Tipografía intacta:** ¿No se modificaron fuentes ni tamaños base innecesariamente?
- [ ] **Jerarquía respetada:** ¿El orden de importancia de la información sigue siendo idéntico?
- [ ] **Cero sobre-optimización:** ¿Se evitaron ajustes microscópicos irrelevantes de 1-2px?
