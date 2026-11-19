# Plantilla del plan y de la entrega

## Plan (Paso 1, se presenta antes de construir)

```markdown
# Plan: <objetivo>

- Criterios de aceptación: <lista breve y comprobable>
- Stack: <frontend> ↔ <backend> · contrato: <OpenAPI | shared/ | nuevo>
- Receta base: <nombre> — ajustes: <qué se quitó o añadió y por qué>
- Contexto compartido: <.sdlc/context.md leído | se creará>
- Entornos: <cómo se sirven frontend y API en desarrollo y producción: esquema, host, puerto, proxy>
- Huella estimada: <≈ N archivos: n backend, n frontend, n compartido> · <propuesta de partir en sesiones si supera ~15>

| # | Skill | Capa | Entregable | Depende de | Modo |
| :-: | :--- | :--- | :--- | :-: | :--- |
| 1 | backend:api-design | Contrato | Endpoints y errores de `POST /orders` | — | ★ |
| 2 | fullstack:contracts | Contrato | Esquema `CreateOrder` compartido | 1 | ★ |
| 3 | backend:schema-and-migrations | Backend | Migración `orders` | 1 | ★ |
| … | | | | | |

**Requieren aprobación (se confirman siempre):** <cambio incompatible del contrato Z y su variante compatible · sesiones invalidadas · migración sobre tabla de N filas · dependencia nueva X · secreto o variable nueva Y · cambio de CORS, cookies o proxy>

**Modos:** completa (todos los pasos, ≈ N skills) · enfocada (★, ≈ M skills, por defecto) · mínima (pasos 1–k).
```

## Entrega (Paso 4)

```markdown
# Funcionalidad: <objetivo> — <modo>

## Resumen
<2–3 frases: qué puede hacer ahora el usuario y estado de la verificación>

## Cambios por capa
- **Contrato:** `<archivos>`
- **Backend:** `<archivos>` (migraciones: `<archivo>`)
- **Frontend:** `<archivos>`
- **Tests:** `<archivos>`

## Verificación
| Comprobación | Resultado |
| :--- | :--- |
| Type-check y lint (ambas capas) | ✅ / ❌ |
| Tests | ✅ n pasan / ❌ |
| Checklists rápidos de las skills aplicadas | n hallazgos (lista) |
| `fullstack:contracts` sobre endpoints nuevos | ✅ / desajustes |
| No verificado | <p. ej. webhook real del proveedor, sin entorno> |

## Despliegue
<orden: migración → backend → frontend; flags; compatibilidad con clientes en circulación>

## Pendientes
- <paso omitido por el modo / handoff no ejecutado / decisión abierta>

## Anexo: skills aplicadas
**Leyenda (veracidad):** ✅ leído completo en esta sesión · ◐ leído en parte (indica las líneas, p. ej. `L1-60`) · ❌ no leído (explica el motivo) · n.a. no existe para esa skill o ese stack. Un ✅ que no corresponde a una lectura real invalida el informe: ante la duda, ◐ o ❌.

| Skill | SKILL.md | patterns.md | Nota de stack | Checklist (verificación) |
| :--- | :-: | :-: | :-: | :-: |
| backend:api-design | ✅ | ✅ | ✅ node.md | ✅ rápido |

**Áreas tocadas sin cargar su skill:**
| Área (skill) | Archivos | Motivo |
| :--- | :--- | :--- |
| frontend:data-fetching | `src/services/apiClient.ts` + 5 servicios | Modo mínima: cambio mecánico de cabeceras |
```
