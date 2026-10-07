# 📋 Checklist Forense — Auditor de Lógica de Negocio y Servicios

- [ ] **1. Desacople de Capas y Controladores**
  - ¿Los controladores HTTP se limitan a recibir el request, llamar al servicio y retornar el status HTTP adecuado?
  - ¿Los servicios de dominio están libres de dependencias de `Express`, `Fastify` o referencias a objetos `req`/`res`?

- [ ] **2. Transaccionalidad ACID en Operaciones Compuestas**
  - Si una operación modifica más de una tabla o entidad relacionada, ¿está envuelta en una transacción explícita (`BEGIN ... COMMIT / ROLLBACK`)?
  - ¿Se maneja el rollback automático ante cualquier excepción no controlada dentro del bloque transaccional?

- [ ] **3. Invariantes y Reglas Duras de Dominio**
  - ¿Las entidades o agregados impiden transiciones de estado ilegales (ej. pasar una orden de "Cancelada" a "Enviada")?
  - ¿Las validaciones de negocio dependen de la base de datos como fuente de verdad y no de suposiciones del cliente?

- [ ] **4. Principios SOLID y Mantenibilidad**
  - ¿Hay clases o funciones que superen las 150 líneas o que tengan más de 4 responsabilidades distintas?
  - ¿Se utiliza inyección o paso explícito de dependencias para facilitar pruebas unitarias sin acoplamiento a la base de datos real?
