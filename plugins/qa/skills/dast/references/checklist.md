# Checklist de auditoría: seguridad dinámica

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md). Una vulnerabilidad confirmada por el escaneo se clasifica por su impacto real (escala del kit), no por el riesgo genérico de la herramienta.

## Autorización y entorno

- [ ] Los escaneos tienen autorización y alcance escritos. **[HIGH si se escanean sistemas sin permiso claro]**
- [ ] El escaneo activo solo corre en entornos aislados con datos de prueba. **[HIGH si corre contra producción o datos reales]**
- [ ] Las rutas con efectos externos o destructivos están excluidas del escaneo activo. **[MEDIUM–HIGH]**

## Cobertura

- [ ] Existe algún DAST (al menos baseline) en aplicaciones expuestas a Internet. **[MEDIUM; HIGH en aplicaciones con datos personales o pagos]**
- [ ] El escaneo está autenticado, con cuentas de prueba por rol. **[MEDIUM]**
- [ ] Las APIs se escanean con su especificación OpenAPI. **[MEDIUM]**

## Proceso

- [ ] El baseline corre en PR o en cada despliegue a un entorno de pruebas; el completo, de forma programada. **[MEDIUM]**
- [ ] Las alertas ignoradas tienen justificación y fecha de revisión. **[MEDIUM]**
- [ ] Los hallazgos de riesgo medio y alto se verifican y se corrigen o se aceptan formalmente. **[HIGH si hay hallazgos altos confirmados sin tratar]**
- [ ] Los informes no contienen tokens ni datos sensibles. **[MEDIUM; HIGH si exponen credenciales]**

## Resultados típicos a confirmar (con la skill de código)

- [ ] Cabeceras de seguridad (CSP, HSTS en HTTPS, `X-Content-Type-Options`, protección contra iframes) presentes en las respuestas reales. **[MEDIUM; HIGH sin CSP en apps con contenido de usuarios]**
- [ ] Errores sin trazas, rutas internas ni versiones. **[HIGH si filtran detalles internos; CRITICAL si incluyen secretos]**
- [ ] Cookies de sesión con `HttpOnly`, `Secure` y `SameSite`. **[HIGH]**
- [ ] CORS sin reflejar orígenes arbitrarios con credenciales. **[HIGH]**
- [ ] Sin inyecciones o XSS explotables. **[CRITICAL si se confirma la explotación con impacto en datos]**

## Cómo verificar

- Buscar configuración de DAST: workflows con `zaproxy`, `zap-baseline`, `zap-full-scan`, `zap-api-scan`, archivos de reglas (`.zap/rules.tsv`) o planes de automatización.
- Revisar el último informe y la lista de supresiones.
- Si el usuario autoriza, ejecutar un baseline (pasivo) contra un entorno no productivo y comparar con la configuración esperada.
