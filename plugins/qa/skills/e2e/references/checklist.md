# Checklist de auditoría: suites E2E

Severidad orientativa; ajústala con [severity.md](../../../standards/severity.md).

## Alcance

- [ ] Los recorridos críticos (acceso, dinero, entidad principal) tienen E2E. **[HIGH si el recorrido de pago o de acceso no tiene ninguna verificación automatizada]**
- [ ] La suite no está llena de comprobaciones de detalle que corresponden a otros niveles. **[MEDIUM]**
- [ ] La suite completa tarda un tiempo asumible (≲ 15 min con paralelismo). **[MEDIUM]**

## Robustez

- [ ] Localizadores por rol, etiqueta, texto o `data-testid`; sin clases de estilo ni XPath posicional. **[MEDIUM]**
- [ ] Sin esperas fijas (`sleep`, `waitForTimeout`, `cy.wait(<número>)`). **[MEDIUM; HIGH si son la causa de intermitencia en recorridos críticos]**
- [ ] Cada test crea sus datos, únicos, y no depende de otro test ni del orden. **[HIGH si impide el paralelismo o causa fallos en cadena]**
- [ ] La autenticación se reutiliza y el login real tiene su propio test. **[LOW–MEDIUM]**
- [ ] Solo se simulan terceros o fallos concretos; el backend propio es real. **[MEDIUM]**
- [ ] Animaciones, reloj y zona horaria controlados en el entorno de test. **[LOW–MEDIUM]**

## Intermitencia y diagnóstico

- [ ] No hay tests intermitentes conocidos sin issue, o reintentos que los esconden. **[MEDIUM; HIGH en recorridos críticos o si el equipo ya ignora los fallos]**
- [ ] Los fallos dejan traza, captura o vídeo, accesibles desde CI. **[MEDIUM]**
- [ ] Los tests en cuarentena tienen issue, responsable y fecha de caducidad. **[MEDIUM]**

## Entornos y seguridad

- [ ] La suite corre en un entorno con datos limpios (preview efímero, base de datos de prueba). **[MEDIUM]**
- [ ] Los mecanismos de siembra de datos no están disponibles en producción. **[HIGH si un endpoint de siembra o de reseteo está accesible en producción]**
- [ ] El smoke de producción es de solo lectura o usa cuentas de prueba, sin efectos irreversibles. **[HIGH si crea cobros, envía emails reales o modifica datos de clientes]**

## Cómo verificar

- Medir intermitencia: repetir los tests sospechosos 5–10 veces (`--repeat-each` en Playwright; bucle o `cypress-repeat` en Cypress).
- Historial de CI: tasa de fallos por test en los últimos 20–50 runs.
- Buscar anti-patrones: `waitForTimeout`, `cy.wait(\d`, `nth-child`, `xpath=`, `.click({ force: true })`.
