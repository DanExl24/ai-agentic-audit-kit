# Dictamen de QA y rúbrica de madurez

## Rúbrica de madurez

### Por área (cada skill aplicada)

```text
nota del área = max(0, 100 − 25·CRITICAL − 10·HIGH − 4·MEDIUM − 1·LOW)
```

- INFO no resta. Un hallazgo agrupado cuenta **una vez**; uno deduplicado resta **solo** en el área de su **causa raíz** (las demás áreas que lo vieron aparecen en "Áreas", sin restar). Dos hallazgos con la misma corrección son el mismo hallazgo.
- **Ausencia de la capacidad central:** si el área aplica pero no existe (cero tests en `frontend:testing` o `backend:testing` con esa capa presente; sin E2E en una aplicación con interfaz y flujos críticos; sin CI en `quality-gates`; sin ningún criterio de terminado ni de salida en `test-strategy`; sin test de no regresión en ninguna corrección en `defect-analysis`), la nota del área **no supera 40**.
- **No aplica** (declarado en el triage): el área no se puntúa ni cuenta en su pilar.

### Por pilar

```text
nota del pilar (0–20) = media de las notas de sus áreas evaluadas × 0,2
```

- Un pilar sin ninguna área evaluada (no aplica, plugin no instalado o fuera del modo) se marca **"no evaluado"** y no cuenta en la global.
- Un pilar es **"parcial"** si alguna de sus áreas aplica y no se evaluó (p. ej. pilar 2 puntuado solo con `e2e` cuando el proyecto tiene frontend y backend sin `frontend:testing` ni `backend:testing`). Se puntúa con lo evaluado, se marca en la tabla y hace provisional la global.

### Global

```text
madurez global (0–100) = suma de los pilares evaluados × 100 / (20 × número de pilares evaluados)
```

- **Tope:** con algún CRITICAL abierto, la global no supera **49**.
- En modo **rápido** no se calcula global ni nivel: solo hallazgos y notas de las áreas revisadas.
- Se declaran los pilares no evaluados: una global sobre 3 pilares no es comparable con una sobre 5.

| Rango | Nivel | Lectura |
| :--- | :--- | :--- |
| 0–39 | **1 — Reactivo** | Pruebas inexistentes o decorativas; los defectos los encuentran los usuarios |
| 40–69 | **2 — Básico** | Hay tests y CI, pero con huecos en flujos principales, poca estrategia o fallos ignorados |
| 70–89 | **3 — Gestionado** | Cobertura guiada por el riesgo, puertas fiables, E2E estables y defectos analizados |
| 90–100 | **4 — Continuo** | Calidad integrada en cada cambio: no funcionales en CI, exploración regular, ciclos Kaizen medidos |

### Requisitos mínimos por nivel

La puntuación resta por defectos de lo que existe; los requisitos comprueban que existe lo que el nivel promete. **Nivel = el menor entre el de la puntuación y el más alto cuyos requisitos se cumplen todos.** El informe dice qué requisito limitó el nivel.

| Nivel | Requisitos (todos) |
| :--- | :--- |
| **2 — Básico** | Tests automatizados en al menos una capa · CI que los ejecuta en cada cambio |
| **3 — Gestionado** | Los del 2 · el CI verifica **todas las capas presentes** (tipos, tests y build de cada una) y bloquea el merge · Definición de Terminado o criterios de salida escritos · E2E (o equivalente) en los flujos críticos, no en uno solo · las correcciones de defectos llevan test de no regresión · ningún HIGH abierto en los pilares 2 y 3 |
| **4 — Continuo** | Los del 3 · pruebas no funcionales que apliquen (rendimiento, seguridad dinámica) en CI o programadas · exploración regular antes de publicar · análisis de defectos con acciones medidas en al menos un ciclo |

Un requisito que no se pudo comprobar (p. ej. la protección de rama) no se da por cumplido: va a "Por verificar" y el nivel se marca provisional.

### Global y nivel provisionales

Con algún pilar **parcial** o **no evaluado**, o con requisitos por verificar, la global y el nivel se presentan como **provisionales** ("82 / 100 provisional · nivel 2 provisional") y no se comparan con una auditoría completa.

La madurez sirve para priorizar y comparar en el tiempo con la misma rúbrica; no es una certificación.

---

## Plantilla del dictamen

```markdown
# Auditoría de QA — <proyecto / alcance>

- Fecha: YYYY-MM-DD
- Alcance: <repositorio, módulos o release> · entornos evaluados: <repo | local | staging> · historial: <CI, issues, git desde <fecha>>
- Contexto: <tipo de producto, exposición, datos sensibles, equipo, frecuencia de publicación, capas>
- Ruta aplicada: <número y nombre> — <por qué>
- Modo: <completa | enfocada | rápida> — <elegido por el usuario | por defecto> · skills aplicadas: <lista>
- No aplican: <áreas y motivo>
- Límites: <qué no se pudo verificar o ejecutar>

## 1. Resumen ejecutivo
<3–5 frases: estado general, los 2–3 riesgos principales, recomendación>

| Madurez global | Nivel | Hallazgos |
| :---: | :---: | :--- |
| **NN / 100** <(provisional)> | <1–4 — nombre> <(provisional)> | 🔴 n · 🟠 n · 🟡 n · 🔵 n · ℹ️ n |

**Nivel:** la puntuación da <N>; los requisitos dan <M> porque <requisito incumplido o por verificar>.

## 2. Madurez por pilar

| Pilar | Nota (0–20) | Estado | Áreas evaluadas | Comentario |
| :--- | :---: | :--- | :--- | :--- |
| 1. Estrategia y diseño | | completo | test-strategy (NN), test-design (NN) | |
| 2. Automatización por niveles | | parcial | e2e (NN) | sin frontend:testing ni backend:testing (fuera del modo) |
| 3. Pipeline y puertas | | | | |
| 4. Calidad en ejecución | — | no evaluado | — | no aplica: <motivo> |
| 5. Exploración y aprendizaje | | | | |

### Requisitos de nivel

| Requisito | Nivel | ¿Cumple? | Evidencia |
| :--- | :-: | :-: | :--- |
| CI verifica todas las capas presentes y bloquea | 3 | ✅ / ❌ / por verificar | |

## 3. Nota por área

| Área (skill) | Nota | 🔴 | 🟠 | 🟡 | 🔵 | Comentario |
| :--- | :---: | :-: | :-: | :-: | :-: | :--- |

## 4. Riesgos inmediatos (CRITICAL y HIGH)

### [QA-XXX-001] <título>
- **Severidad:** HIGH — <riesgo × detección>
- **Áreas:** <skills que lo detectaron; resta en la de la causa raíz>
- **Ubicación:** `ruta` · flujo · etapa del pipeline
- **Escenario:** <qué defecto podría escapar y cómo>
- **Corrección:** <concreta>
- **Esfuerzo:** S / M / L

## 5. Resto de hallazgos por área
<MEDIUM, LOW e INFO agrupados por skill, formato abreviado>

## 6. Lo que está bien

## 7. Por verificar
<configuración remota o datos no accesibles: qué comprobar y dónde>

## 8. Plan de remediación

| Lote | Hallazgos | Skill (modo Construir) | Esfuerzo | Requiere aprobación | Orden |
| :--- | :--- | :--- | :---: | :---: | :---: |

## 9. Escalado a otros dominios
| Problema | Evidencia | Destino |
| :--- | :--- | :--- |

## 10. (Solo ruta 1) Veredicto

| Bloque | ¿Listo? | Riesgos abiertos |
| :--- | :---: | :--- |
| Criterios de salida | ✅ / ❌ | |
| Pipeline y checks obligatorios | | |
| Recorridos críticos (E2E) | | |
| Exploración de lo cambiado | | |
| Rendimiento y seguridad (si aplica) | | |

**Decisión recomendada:** publicar / publicar con riesgos aceptados (listarlos) / no publicar hasta resolver <hallazgos>.

## Handoffs
- Pendientes: <skill> — <disparador y evidencia>

## Anexo (obligatorio): referencias cargadas

| Skill | SKILL.md | checklist.md | Nota de herramienta |
| :--- | :-: | :-: | :-: |
| <skill> | ✅ / ❌ | ✅ / ❌ | ✅ <archivo> / ❌ / n.a. |

**Leyenda (veracidad):** ✅ leído completo en esta sesión · ◐ leído en parte (con las líneas) · ❌ no leído (con el motivo) · n.a. no existe. Un ✅ que no corresponde a una lectura real invalida el informe.
```
