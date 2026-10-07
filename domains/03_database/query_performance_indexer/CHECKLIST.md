# 📋 Checklist Forense — Auditor de Consultas y Rendimiento de BD

- [ ] **1. Detección de N+1 Queries**
  - ¿Hay iteraciones (`for`, `map`, `forEach`) en el backend que ejecuten consultas a base de datos dentro de su cuerpo?
  - ¿Los ORMs (Prisma, TypeORM, Hibernate) están configurados con `include` / `eager loading` adecuado para evitar subconsultas automáticas?

- [ ] **2. Cobertura de Índices y B-Trees**
  - ¿Todas las claves foráneas (`FOREIGN KEY`) tienen un índice explícito en la tabla hija?
  - ¿Las consultas filtradas por múltiples campos (ej. `empresa_id` + `estado`) cuentan con un índice compuesto B-Tree ordenado de mayor a menor selectividad?
  - ¿Hay índices redundantes o duplicados ocupando espacio innecesario en disco?

- [ ] **3. Consultas SARGables y Expresiones**
  - ¿Se evitan funciones directas sobre columnas filtradas (ej. `DATE(created_at)`) o se crearon índices basados en expresiones (`CREATE INDEX ... ON (DATE(created_at))`)?
  - ¿Las búsquedas de texto usan índices adecuados (`GIN`, `pg_trgm`) en lugar de escaneos completos con `LIKE '%text%'`?

- [ ] **4. Paginación y Límites de Memoria**
  - ¿Todas las consultas que listan datos tienen cláusula `LIMIT` obligatoria?
  - ¿En tablas de más de 100,000 registros se utiliza paginación por cursor (`keyset pagination`) en lugar de `OFFSET` profundo de alto costo?
