# Plantillas: estrategia y plan de release

## Estrategia de pruebas (una página)

```markdown
# Estrategia de pruebas — <producto>
Actualizada: YYYY-MM-DD

## Contexto
<qué hace el producto, quién lo usa, coste de un fallo, frecuencia de despliegue>

## Mapa de riesgos
| Área | I | P | D | Riesgo | Control |
| :--- | :-: | :-: | :-: | :-: | :--- |

## Forma de la cobertura
<pirámide / trofeo / diamante y por qué; herramientas por nivel>

## Qué se automatiza, qué se explora y qué se vigila
<lista breve>

## Definición de terminado de calidad
<lista de comprobación>

## Riesgos aceptados
| Riesgo | Motivo | Aceptado por | Revisión |
| :--- | :--- | :--- | :--- |
```

## Plan de pruebas de un release

```markdown
# Plan de pruebas — <release / versión>

- Alcance: <cambios incluidos, enlazados>
- Fuera de alcance: <qué no se prueba y por qué>
- Entorno y datos: <dónde, con qué datos, quién los prepara>

## Riesgos del release
| Cambio | Riesgo | Verificación | Responsable | Estado |
| :--- | :-: | :--- | :--- | :-: |

## Regresión
<suites automatizadas y sesiones exploratorias previstas>

## Criterios de salida
- [ ] 0 CRITICAL abiertos; HIGH aceptados: <lista>
- [ ] Flujos de riesgo alto verificados en este build
- [ ] Smoke y regresión en verde
- [ ] Plan de vuelta atrás: <cómo>

## Decisión
<go / no-go, fecha, quién decide, riesgos aceptados>
```
