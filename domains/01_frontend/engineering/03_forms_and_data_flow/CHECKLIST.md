# 📋 Checklist Forense — Formularios, Validación y Flujo de Datos

- [ ] **1. Validación Declarativa**
  - ¿Todo formulario valida sus entradas mediante un esquema formal (Zod / VeeValidate)?
  - ¿Los mensajes de error son específicos y claros para el usuario final?

- [ ] **2. Control de Envío y Doble Clic**
  - ¿El botón de envío se deshabilita y muestra un indicador de carga mientras la petición está en vuelo?
  - ¿Se restablece el estado del formulario tras un envío exitoso?

- [ ] **3. Dinamismo y Manejo de Errores**
  - ¿Los campos dinámicos usan identificadores únicos como `:key` y no el índice del array?
  - ¿Los errores 422 del backend se asocian visualmente al campo específico que falló?
