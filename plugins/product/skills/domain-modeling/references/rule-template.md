# Plantillas: regla de negocio y glosario

Si el proyecto ya tiene un formato de reglas (p. ej. secciones "Descripción", "Motivo", "Archivos donde se implementa"), **se respeta** y se añaden solo los campos que falten (estado, origen, ejemplos).

## Regla de negocio

```markdown
### RN-BUZ-004
Una nota anclada se muestra antes que cualquier nota sin anclar.

- **Tipo:** restricción | cálculo | derivación | permiso | temporal
- **Enunciado:** <condición y resultado, atómico y con cifras>
- **Motivo:** <negocio, normativa, decisión técnica> · **Origen:** INT-… / documento / inferido del código (`ruta` → `símbolo`)
- **Estado:** borrador | acordado | implementado | obsoleto (sustituida por RN-…)
- **Ejemplos:**

  | Caso | Entrada | Resultado esperado |
  | :--- | :--- | :--- |
  | Cumple | <…> | <…> |
  | No cumple | <…> | <…> |
  | Límite | <…> | <…> |

- **Excepciones:** <ninguna | excepción — motivo>
- **Entidades:** Nota · **Módulo:** buzon
- **Relacionado:** HU-BUZ-002 · RN-BUZ-001 · DEC-…
- **Implementación:** `hub/src/notes.ts` → `NotesStore.list` · `POST /api/notes/pin` (si existe)
```

## Glosario

```markdown
# Glosario — <producto>

| Término | Definición | No confundir con / sinónimos prohibidos | Ejemplo | Contraejemplo | Módulo |
| :--- | :--- | :--- | :--- | :--- | :--- |

## Correspondencia con el código
| Término del negocio | Nombre en el código | Nombre en la interfaz |
| :--- | :--- | :--- |
```
