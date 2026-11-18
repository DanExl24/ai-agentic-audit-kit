# 📬 Protocolo Canónico de Memo de Traspaso (Inter-Agent Handoff Memo)

> **Estándar de comunicación horizontal entre especialistas del dominio Frontend.**  
> Ningún especialista comienza de cero. Cuando un agente termina su fase de auditoría, debe redactar y dejar este memo como testigo para el siguiente especialista de la cadena.

---

## 1. Estructura Obligatoria del Memo

Todo traspaso debe redactarse bajo la siguiente plantilla estándar:

```markdown
# 📬 MEMO DE TRASPASO INTER-AGENTE

- **De (Agente Emisor):** [ui_ux_experience/01_senior_design_critic | frontend:architecture | frontend:typescript | frontend:data-fetching | frontend:state-management | frontend:forms | engineering/04_design_system_and_styling | engineering/05_accessibility_and_wcag]
- **Para (Agente Receptor):** [ui_ux_experience/01_senior_design_critic | frontend:architecture | frontend:typescript | frontend:data-fetching | frontend:state-management | frontend:forms | engineering/04_design_system_and_styling | engineering/05_accessibility_and_wcag | 00_frontend_director]
- **Módulo / Ruta Auditada:** `ruta/del/modulo`
- **Fecha y Hora:** YYYY-MM-DD HH:mm

---

### 1. Resumen Ejecutivo de lo Entregado
> Síntesis de 2-3 párrafos explicando qué se auditó, qué hallazgos clave se encontraron y en qué estado queda la base técnica para el siguiente rol.

### 2. Mapa de Archivos e Insumos Preparados
- [`ruta/al/archivo_a.ts`](file:///ruta/al/archivo_a.ts#L10-L40): Resumen del archivo analizado.
- [`ruta/al/archivo_b.vue`](file:///ruta/al/archivo_b.vue#L1-L25): Componente con puntos clave.

### 3. ⚠️ Puntos Ciegos y Advertencias Especiales para TI
> Especifica qué cosas sospechosas o anomalías detectaste que caen fuera de tu alcance pero son críticas para el rol receptor.  
> *Ejemplo:* "Noté que el servicio emite eventos a un EventBus en la línea 45. Revisa con lupa el store `useBillingStore.ts`, sospecho que se suscribe pero jamás se desuscribe al desmontar la vista."

### 4. Objetivo Específico para tu Auditoría
> Instrucción puntual y sin ambigüedades de qué esperas que audite el siguiente rol.
```

---

## 2. Reglas Sagradas del Traspaso

1. **Evidencia Concreta:** Prohibido emitir frases genéricas como *"el código se ve bien"* o *"hay errores menores"*. Todo señalamiento debe incluir la ruta del archivo y número de línea.
2. **Contexto Continuo:** El agente receptor debe leer este memo **antes** de abrir el código fuente, tomándolo como su mapa de navegación preliminar.
3. **Sujeto a Aprobación:** El emisor entiende que su entrega puede ser devuelta si no cumple con la calidad mínima requerida en `PEER_REJECTION_PROTOCOL.md`.
