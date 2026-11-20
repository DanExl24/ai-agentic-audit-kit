# Identificadores y enlaces

Todo lo que el plugin `product` produce se puede **citar y enlazar**: reglas, historias, criterios, requisitos, decisiones. Sin identificadores estables no hay trazabilidad (`traceability`), ni análisis de impacto, ni forma de decir qué test cubre qué criterio. Este estándar es común a todas las skills del plugin.

## Si el proyecto ya tiene convención, manda la suya

Antes de crear IDs, busca los existentes (`grep -rE "\b(RN|HU|CU|RF|RNF)-" docs/`). Si el proyecto ya numera de otra forma (`BR-12`, `US-4`, `RN-BUZ-001`), **se adopta su convención** y se declara en el contexto; no se mezclan dos esquemas.

## Convención por defecto

```text
<TIPO>-<MÓDULO>-<NNN>      RN-BUZ-001   (con módulos)
<TIPO>-<NNN>               RN-001       (proyecto pequeño, sin módulos)
<TIPO>-<MÓDULO>-<NNN>.<n>  CA-BUZ-001.2 (elemento hijo: criterio 2 de la historia 001)
```

- **MÓDULO:** 3–5 letras en mayúsculas, estable (`BUZ`, `ARCH`, `PAGO`). Se lista en el glosario de módulos del contexto.
- **NNN:** tres dígitos, secuencial por tipo y módulo.

| Tipo | Qué identifica | Skill que lo crea |
| :--- | :--- | :--- |
| `OBJ` | Objetivo de negocio o métrica de éxito | `discovery` |
| `SUP` | Supuesto (de negocio, de usuario o técnico) pendiente de validar | `discovery`, `elicitation` |
| `INT` | Interesado (persona, rol o sistema con interés en el producto) | `elicitation` |
| `PRE` | Pregunta abierta | `elicitation` |
| `DEC` | Decisión tomada, con su motivo | todas |
| `RN` | Regla de negocio | `domain-modeling` |
| `EP` | Épica | `user-stories` |
| `HU` | Historia de usuario | `user-stories` |
| `CA` | Criterio de aceptación (hijo de una HU: `CA-BUZ-001.2`) | `user-stories` |
| `CU` | Caso de uso | `user-stories` |
| `RF` / `RNF` | Requisito funcional / no funcional | `specification` |

Los términos del glosario y las entidades del modelo se citan **por su nombre**, no por número.

## Reglas

1. **Estables:** un ID nunca se reutiliza ni se renumera. Si un elemento se elimina o se sustituye, se marca como obsoleto (`Estado: obsoleto · sustituido por RN-BUZ-007 · 2026-11-20`) y conserva su número.
2. **Únicos en el proyecto:** antes de asignar uno, busca el último usado de ese tipo y módulo.
3. **Un elemento, un encabezado:** cada elemento de catálogo es un encabezado con **solo su ID** (`### RN-BUZ-001`) y el título en la primera línea debajo. Así el ancla es estable (`#rn-buz-001`) aunque cambie el título.
4. **Estado y origen** en cada elemento: `borrador` · `acordado` · `implementado` · `obsoleto`, y de dónde sale (entrevista `INT-002` del 2026-11-20, documento, código existente, decisión `DEC-004`). Lo deducido del código se marca **"inferido del código"** hasta que alguien lo confirme.

## Enlaces

| Hacia | Formato | Ejemplo |
| :--- | :--- | :--- |
| Otro elemento del producto | Enlace relativo con ancla | `[RN-BUZ-001](../domain/reglas.md#rn-buz-001)` |
| Código | Ruta desde la raíz del repositorio y símbolo; líneas solo como apoyo, porque se desplazan | `hub/src/notes.ts` → `parseDataUrlImage` |
| Endpoint | Método y ruta | `POST /api/notes` |
| Test | Ruta y nombre del test | `test/notes.test.ts` → "rechaza SVG" |
| Commit, PR o issue | Hash corto o número con el repositorio | `706a4fa` · `owner/repo#12` |
| Documento externo | URL o ruta, con fecha de consulta | `docs/MANUAL.md` |

- Los enlaces son **bidireccionales** cuando ambos lados están en el repositorio: la historia cita sus reglas y la regla cita sus historias (sección "Relacionado").
- Un enlace a código que ya no existe es un hallazgo de trazabilidad, no se deja colgando.

## Ubicación por defecto

Si el proyecto no tiene ya una estructura de documentación de producto (p. ej. `docs/modules/<módulo>/`), se usa:

```text
docs/product/
├── brief.md                 # discovery: problema, usuarios, propuesta de valor, OBJ y SUP
├── elicitation/
│   ├── interesados.md       # INT
│   ├── preguntas.md         # PRE (abiertas y respondidas)
│   ├── decisiones.md        # DEC
│   └── notas/AAAA-MM-DD-<tema>.md
├── domain/
│   ├── glosario.md
│   ├── modelo.md            # diagrama y entidades
│   └── reglas.md            # RN (o reglas por módulo)
├── backlog/                 # EP, HU, CA, CU (ola de user-stories)
├── especificacion/          # RF, RNF, SRS o PRD
└── trazabilidad.md
```

Con documentación por módulo, cada módulo tiene sus catálogos (`docs/modules/buzon/reglas_negocio.md`) y el prefijo de módulo en los IDs.
