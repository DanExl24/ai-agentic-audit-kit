# 📋 Checklist Forense — Causa Raíz y Deuda de Procesos (Root Cause & Kaizen Specialist)

- [ ] **1. Detección de Hotspots y Regresiones en Historial**
  - ¿Se identificaron los 3 archivos o módulos con mayor frecuencia de commits de corrección (`git log --format=format: --name-only --grep="fix"`)?
  - ¿El incidente analizado es una regresión directa de un bug supuestamente resuelto en semanas o sprints anteriores?
  - ¿Existen pruebas automatizadas asociadas a los bugs corregidos que impidan su reaparición?

- [ ] **2. Exhaustividad de las 5 Ramas de Ishikawa**
  - **Métodos:** ¿Se definió y cumplió la Definición de Terminado (*Definition of Done*) y la revisión de código por pares?
  - **Personas:** ¿El equipo contaba con la especificación completa del requerimiento o se asumieron reglas de negocio sin confirmar?
  - **Herramientas:** ¿La suite de CI/CD ejecutó las pruebas de forma bloqueante antes del merge o se permitió el bypass manual?
  - **Entorno:** ¿El fallo se reproduce en local o dependió exclusivamente de factores del entorno de despliegue?
  - **Código:** ¿La estructura del código fomenta el error (acoplamiento alto, efectos secundarios, ausencia de tipado)?

- [ ] **3. Aislamiento Pareto 80/20**
  - ¿Se cuantificaron las incidencias pasadas por categoría (ej. 60% por falta de validación de entradas, 25% por inconsistencias en la base de datos, 15% misceláneos)?
  - ¿Se priorizó el ataque a la causa raíz de mayor impacto en lugar de dispersar esfuerzo en síntomas superficiales?

- [ ] **4. Realismo de la Matriz Kaizen y Quick Wins**
  - ¿Se definieron acciones inmediatas (*Quick Wins*) ejecutables en menos de 48 horas (ej. agregar un validador Zod, activar una regla de ESLint, agregar un índice)?
  - ¿Las soluciones estructurales tienen asignado un nivel de dificultad, plazo e impacto verificable?
  - ¿Se establecen métricas de éxito (KPIs) para comprobar que la causa raíz fue erradicada definitivamente?
