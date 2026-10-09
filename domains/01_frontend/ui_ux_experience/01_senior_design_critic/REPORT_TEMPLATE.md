# 📋 Plantilla de Informe: UI/UX AUDIT & DESIGN CRITIQUE

> **Documento emitido por:** `01_senior_design_critic` (Subdominio UI/UX & Experiencia)  
> **Sistema / Pantalla Auditada:** [Nombre de la Vista o Flujo]  
> **Fecha de Evaluación:** YYYY-MM-DD  
> **Resoluciones Probadas:** 320px, 375px, 390px, 414px, 768px, 1024px, 1280px, 1366px, 1440px, 1920px

---

# UI/UX AUDIT

## 1. Executive Summary
- **Fortalezas principales:** [Qué decisiones visuales/UX funcionan bien y deben conservarse]
- **Problemas principales:** [Los mayores puntos de fricción, sobrecarga o quiebre responsive]
- **Estado general de UX:** [Diagnóstico cualitativo de comodidad y ergonomía]
- **Estado general de UI:** [Diagnóstico cualitativo de consistencia estética y jerarquía]
- **Estado general de responsive:** [Diagnóstico en móviles y tablets reales]

---

## 2. Overall Score (Calificación de 0 a 10)

| Dimensión de Experiencia | Puntuación (0-10) | Breve Justificación |
| :--- | :---: | :--- |
| **Visual Design** | 0.0 | Calidad estética, equilibrio y armonía visual. |
| **UX & Ergonomía** | 0.0 | Facilidad de uso, fricción y fatiga cognitiva tras uso prolongado. |
| **Responsive (10 Viewports)** | 0.0 | Adaptabilidad real y reorganización de contenido en móviles. |
| **Accesibilidad Visual** | 0.0 | Legibilidad, contraste cromático y percepción clara. |
| **Consistencia** | 0.0 | Coherencia de componentes, botones y estilos entre pantallas. |
| **Arquitectura de Información** | 0.0 | Jerarquía de contenidos, claridad de títulos y navegación. |
| **Mobile Experience** | 0.0 | Usabilidad con una sola mano, touch targets y menús mobile. |
| **🎯 PUNTUACIÓN GLOBAL** | **0.0 / 10** | **Veredicto global de calidad de producto.** |

---

## 3. Critical Issues
*Lista únicamente los problemas más graves que arruinan la experiencia o bloquean al usuario:*

### [CRITICAL-UX-01] {Título del Problema}
- **Problema:** [Descripción cruda y directa del fallo]
- **Evidencia Visual:** [Dónde ocurre, pantalla o componente específico]
- **Impacto en el Usuario:** [Frustración, abandono, fatiga, clics erróneos]
- **Severidad:** `CRITICAL` | `HIGH`
- **Solución Propuesta:** [Cómo debe resolverse visual o conceptualmente]

---

## 4. Screen-by-Screen Review (Revisión Pantalla por Pantalla)

### Pantalla / Módulo: [Nombre de la Pantalla]

#### A. Estado Actual
[Describe cómo está organizada actualmente la información].

#### B. Problemas Detectados
- **Jerarquía:** [Qué compite por atención y qué debería destacar].
- **Densidad:** [Sobrecarga de cards, tablas o botones].
- **Espaciado:** [Zonas comprimidas o vacíos innecesarios].

#### C. Comportamiento Responsive (Desktop, Tablet, Mobile)
- **Desktop (1440px / 1920px):** [Comportamiento en monitores anchos].
- **Tablet (768px / 1024px):** [Comportamiento en pantallas medianas].
- **Mobile (320px / 375px / 390px):** [Comportamiento en smartphones].

#### D. Recomendación de Rediseño
[Explicación de cómo debería reorganizarse la pantalla].

---

## 5. Responsive Audit (Matriz de Viewports Físicos)

| Dispositivo / Viewport | Resolución | Estado Visual | Problema de UX Detectado | Acción Recomendada |
| :--- | :---: | :---: | :--- | :--- |
| **Móvil Ultra-compacto** | 320 × 720 | 🔴 / 🟡 / 🟢 | Desborde, botones pegados, etc. | Ocultar/Colapsar/Cards |
| **Móvil Estándar** | 375 × 812 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Móvil Moderno** | 390 × 844 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Móvil Grande** | 414 × 896 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Tablet Vertical** | 768 × 1024 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Tablet Horizontal** | 1024 × 768 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Desktop HD** | 1280 × 720 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Laptop Corporativa** | 1366 × 768 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Desktop Trabajo** | 1440 × 900 | 🔴 / 🟡 / 🟢 | ... | ... |
| **Monitor Widescreen** | 1920 × 1080 | 🔴 / 🟡 / 🟢 | ... | ... |

---

## 6. Design System Recommendations
*Propuesta de estándares visuales coherentes:*
- **Colores:** [Paleta recomendada y corrección de colores no semánticos]
- **Tipografía:** [Escala modular y jerarquía recomendada]
- **Espaciado:** [Regla de espaciado recomendada, ej. múltiplos de 4px / 8px]
- **Botones e Inputs:** [Estandarización de variantes y touch targets mínimos de 44px]
- **Tablas:** [Estándar de transformación a cards en pantallas < 768px]
- **Modales y Drawers:** [Cuándo usar modal centrado vs drawer lateral en mobile]

---

## 7. UX Redesign Proposal (Visión Global Ideal)
[Propón la estructura completa de cómo debería funcionar la interfaz ideal, sin temor a sugerir una demolición y reestructuración completa si la actual es deficiente].

---

## 8. Before vs After (Comparativa de Transformación)

### Caso 1: [Componente o Flujo Específico]
* **Actual:** [Descripción exacta de la interfaz y experiencia actual]
* **Propuesta:** [Descripción detallada de la nueva experiencia propuesta]
* **Motivo UX:** [Justificación de por qué la nueva alternativa reduce fricción y mejora la usabilidad]

---

## 9. Prioritized Improvement Roadmap

- **P0 (Crítico - Resolver de Inmediato):**
  - [ ] Acción P0.1
- **P1 (Importante - Próximo Sprint):**
  - [ ] Acción P1.1
- **P2 (Mejora de Calidad y Confort):**
  - [ ] Acción P2.1
- **P3 (Refinamiento Estético Secundario):**
  - [ ] Acción P3.1

---

## 10. Final Verdict

- **Qué está bien (Conservar):** [Decisiones acertadas que NO deben destruirse]
- **Qué está mal (Corregir):** [Deficiencias mayores que deben rediseñarse]
- **Qué debería eliminarse:** [Elementos decorativos, cards o pasos que sobran]
- **Veredicto de Madurez:** [¿Qué tan cerca está el producto de una experiencia profesional de clase mundial?]
