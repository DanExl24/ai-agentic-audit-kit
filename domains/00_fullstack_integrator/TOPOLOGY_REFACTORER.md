# 🏗️ Guía de Diagnóstico y Refactorización de Topología de Carpetas

Esta guía enseña al **Agente Integrador Fullstack** a analizar la estructura de archivos de un proyecto y proponer reorganizaciones limpias, desacopladas y mantenibles.

---

## 1. Síntomas de una Topología Enferma (Codebase Smells)

1. **La "Bolsa de Gatos" (`utils/` o `helpers/` gigante):**
   * Decenas de archivos con funciones no relacionadas que todo el mundo importa desde todas partes.
2. **Componentes con Dependencias Circulares o Ilegítimas:**
   * Archivos de la interfaz gráfica importando modelos de base de datos, ORMs o secretos de entorno del backend.
3. **Falta de Capas de Abstracción (Monolito sin Límites):**
   * Controladores de Express/FastAPI que hacen consultas SQL directamente, mezclados con lógica de negocio y validación de strings en un solo archivo de 1,200 líneas.
4. **Tipos Duplicados en Espejo:**
   * Definiciones manuales de interfaces de usuario en el frontend y schemas idénticos repetidos en el backend, que inevitablemente divergen con el tiempo.
5. **Mezcla de Responsabilidades en Vistas:**
   * Vistas de React/Vue que ejecutan lógica de autenticación, peticiones HTTP, manipulación de query params y renderizado de tablas en un solo archivo.

---

## 2. Los 3 Arquetipos de Arquitectura Recomendados

Según la escala y naturaleza del proyecto, el integrador debe proponer uno de los siguientes arquetipos:

### Arquetipo A: Monolito Modular Desacoplado (Recomendado para la mayoría de apps)
```text
/
├── shared/                     # Contratos Zod / DTOs / Constantes de negocio
├── backend/
│   ├── core/                   # Middlewares, DB pool, auth, config
│   └── modules/                # Módulos verticales por feature (routes -> controller -> service -> repo)
└── frontend/
    ├── core/                   # ApiClient, Router, Layouts, Design System Base
    └── modules/                # Vistas, stores locales y componentes de dominio
```

### Arquetipo B: Monorepo con Workspaces (Turborepo / Nx / pnpm)
Recomendado cuando el frontend y el backend son proyectos de despliegue independiente pero comparten librerías.
```text
/
├── packages/
│   ├── contracts/              # Paquete @org/contracts tipado y publicado internamente
│   ├── ui-kit/                 # Librería de componentes visuales compartida
│   └── config/                 # ESLint, TypeScript, Tailwind compartidos
└── apps/
    ├── web/                    # SPA / SSR
    └── api/                    # Servidor REST / GraphQL
```

### Arquetipo C: Clean Architecture / Hexagonal (Para alta complejidad de dominio)
Recomendado para sistemas bancarios, fintech o ERPs con reglas estrictas independientes de la base de datos o el framework web.

---

## 3. Protocolo de Migración No Disruptiva (Strangler Fig Pattern)

Nunca propongas reescribir un proyecto de golpe. El Integrador Fullstack siempre debe plantear un plan gradual:
1. **Fase 1 (Aislamiento de Contratos):** Crear la carpeta `shared/contracts` sin mover código funcional.
2. **Fase 2 (Encapsulamiento del Backend):** Mover controladores y servicios módulo por módulo sin cambiar endpoints.
3. **Fase 3 (Modularización del Frontend):** Reorganizar vistas en módulos de dominio vinculándolos al nuevo cliente de API.
4. **Fase 4 (Limpieza de Archivos Huérfanos):** Depurar carpetas `utils/` obsoletas una vez que todo importe desde sus módulos correspondientes.
