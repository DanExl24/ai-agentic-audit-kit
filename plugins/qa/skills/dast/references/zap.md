# Notas: OWASP ZAP

ZAP (Zed Attack Proxy) es un escáner DAST de código abierto. Para automatizar se usan sus **escaneos empaquetados** en Docker o su **Automation Framework**.

## Escaneos empaquetados (Docker)

```bash
# Pasivo (baseline): spider + análisis pasivo, sin atacar
docker run --rm -v "$(pwd):/zap/wrk:rw" -t ghcr.io/zaproxy/zaproxy:stable \
  zap-baseline.py -t https://preview-123.example.com -r baseline.html -J baseline.json -c rules.tsv

# Activo (completo): ataca. Solo entornos aislados con datos de prueba
docker run --rm -v "$(pwd):/zap/wrk:rw" -t ghcr.io/zaproxy/zaproxy:stable \
  zap-full-scan.py -t https://staging.example.com -r full.html -c rules.tsv

# API guiada por OpenAPI. Activo
docker run --rm -v "$(pwd):/zap/wrk:rw" -t ghcr.io/zaproxy/zaproxy:stable \
  zap-api-scan.py -t https://staging.example.com/openapi.json -f openapi -r api.html -c rules.tsv
```

Opciones útiles:
- `-r` informe HTML, `-J` JSON, `-w` Markdown (en `/zap/wrk`).
- `-m <minutos>` duración del spider; `-j` añade el spider AJAX para SPAs.
- `-c rules.tsv` aplica las reglas; `-g rules.tsv` genera un archivo de reglas inicial con todas en WARN para empezar.
- `-I` no falla por avisos (WARN), solo por FAIL.

Códigos de salida: `0` sin problemas, `1` al menos una alerta FAIL, `2` avisos sin FAIL, `3` otro error. El pipeline bloquea con `1`.

## Archivo de reglas

```text
# rules.tsv — ID de regla <TAB> acción <TAB> motivo
10038	FAIL	(Content Security Policy no definida)
10021	FAIL	(X-Content-Type-Options ausente)
10035	FAIL	(HSTS ausente; el entorno de preview sirve HTTPS)
10096	IGNORE	(Marca de tiempo divulgada: son fechas públicas de publicación, revisado 2026-11-18)
```

Cada IGNORE lleva su justificación y fecha de revisión. Los IDs de regla aparecen en el informe junto a cada alerta.

## Escaneo autenticado

Con un token de una cuenta de prueba, los escaneos empaquetados admiten variables de entorno que añaden una cabecera a cada petición:

```bash
docker run --rm -v "$(pwd):/zap/wrk:rw" \
  -e ZAP_AUTH_HEADER_VALUE="Bearer $TEST_TOKEN" \
  -e ZAP_AUTH_HEADER_SITE="staging.example.com" \
  -t ghcr.io/zaproxy/zaproxy:stable zap-api-scan.py -t https://staging.example.com/openapi.json -f openapi -r api.html
```

(`ZAP_AUTH_HEADER` cambia el nombre de la cabecera; por defecto, `Authorization`.)

Para sesiones por formulario o cookie que caducan, varios roles o verificación de sesión iniciada, usa el **Automation Framework**:

```bash
docker run --rm -v "$(pwd):/zap/wrk:rw" -t ghcr.io/zaproxy/zaproxy:stable zap.sh -cmd -autorun /zap/wrk/zap-plan.yaml
```

El plan YAML define contextos (URLs incluidas y excluidas), usuarios y método de autenticación, y una secuencia de trabajos (spider, espera del escaneo pasivo, escaneo activo, informe). Se puede generar desde la interfaz de ZAP y versionar.

## GitHub Actions

Existen acciones oficiales que envuelven los escaneos empaquetados: `zaproxy/action-baseline`, `zaproxy/action-full-scan` y `zaproxy/action-api-scan` (entradas como `target`, `rules_file_name`, `cmd_options`). Por defecto pueden **abrir o actualizar una issue** con los resultados; desactívalo (`allow_issue_writing: false`) si no lo quieres. Fija la versión de la acción y guarda el informe como artefacto.

## Interpretar

- Cada alerta trae riesgo (High, Medium, Low, Informational) y confianza. Prioriza riesgo alto con confianza media o alta, y **verifícala** antes de reportarla.
- Agrupa por regla: una cabecera ausente en 300 URLs es un hallazgo con una corrección (normalmente en un middleware o en el proxy).
- El escaneo pasivo no prueba inyecciones; "baseline limpio" no significa "sin vulnerabilidades".
