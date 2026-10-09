# 📋 Checklist Forense — Arquitectura, Topología y Red

- [ ] **1. Modularización y Límites de Dominio**
  - ¿El código está estructurado en módulos verticales coherentes o disperso en carpetas monolíticas planas?
  - ¿Las vistas importan lógica únicamente desde sus servicios de módulo correspondientes?

- [ ] **2. Cliente HTTP y Resiliencia**
  - ¿Existe un único cliente de API centralizado (`apiClient.ts`) sin instancias dispersas de `axios.create()`?
  - ¿Los interceptores manejan correctamente el token JWT y la redirección a login ante un 401 definitivo?
  - ¿Se implementa timeout preventivo y opción de cancelación con `AbortController`?

- [ ] **3. Higiene de Tipos en TypeScript**
  - ¿El código está 100% libre del tipo `any`?
  - ¿Las respuestas del backend están tipadas mediante DTOs o esquemas Zod en compile-time?
  - ¿Las props y eventos de los componentes están fuertemente tipados?
