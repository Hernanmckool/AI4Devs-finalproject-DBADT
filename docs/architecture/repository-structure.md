# Estructura del monorepo

> **Prompt de origen:** §2.3, Prompt 1 — Estructura del monorepo y harness de desarrollo con IA, en [`prompts.md`](../../prompts.md). La parte del harness se desarrolla en [`docs/ai/sdd-harness.md`](../ai/sdd-harness.md).
> **Fuente de decisiones aprobadas:** [`README.md`](../../README.md) §2.3; [ADR-D04](decisions/ADR-D04-monorepo.md).
> **Estado del documento:** estructura **planificada**. En el repositorio solo existen `README.md`, `prompts.md` y, desde esta ejecución, `docs/`.

## 1. Árbol aprobado del monorepo

```text
AI4Devs-finalproject-DBADT/
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── app/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── lib/
│   │   ├── services/
│   │   └── types/
│   └── package.json
├── backend/
│   ├── cmd/api/
│   ├── internal/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── repositories/
│   │   ├── models/
│   │   ├── middleware/
│   │   ├── config/
│   │   └── dto/
│   ├── tests/integration/
│   └── go.mod
├── database/
│   ├── migrations/
│   └── seeds/
├── tests/e2e/
├── docs/
├── README.md
└── prompts.md
```

## 2. Estado actual frente a lo planificado

| Ruta | Estado en el repositorio a 2026-10-19 |
|---|---|
| `README.md` | Existe en `main` y en la rama `feature/entrega1-HPPY`. **Pull Request no creado** |
| `prompts.md` | Existe; publicado en `main`; sin cambios e idéntico en ambas ramas |
| `docs/` | Creado en la ejecución documental del 2026-10-19; publicado en `main` y en `feature/entrega1-HPPY` |
| `frontend/`, `backend/`, `database/`, `tests/e2e/` | No existen |

## 3. Propósito de cada directorio

| Directorio | Contenido previsto | Componentes relacionados |
|---|---|---|
| `frontend/src/app/` | Rutas y vistas de Next.js | Vistas ([`components.md`](components.md#1-componentes-del-frontend-nextjs--typescript)) |
| `frontend/src/components/` | Componentes de interfaz reutilizables | [`ux-design.md`](../product/ux-design.md#8-componentes-visuales-reutilizables) |
| `frontend/src/hooks/` | Estado de interfaz y consumo de datos | — |
| `frontend/src/services/` | Cliente de API | — |
| `frontend/src/types/` | Tipos del contrato | [`openapi.yaml`](../api/openapi.yaml) |
| `frontend/src/lib/` | Utilidades | — |
| `backend/cmd/api/` | Punto de entrada | — |
| `backend/internal/*` | Capas y paquetes transversales | [`components.md`](components.md#2-componentes-del-backend-go--chi-v5) |
| `backend/tests/integration/` | Integración con PostgreSQL | [`testing-strategy.md`](testing-strategy.md) |
| `database/migrations/` | Migraciones SQL versionadas | TICKET-003 |
| `database/seeds/` | Datos sintéticos de prueba | TICKET-003 |
| `tests/e2e/` | Pruebas Playwright | [`testing-strategy.md`](testing-strategy.md) |
| `docs/` | Documentación ampliada de esta ejecución | [`docs/README.md`](../README.md) |

## 4. Convenciones de pruebas (README §2.3)

- Pruebas unitarias de Go en archivos `*_test.go`, junto al código.
- Integración de backend con PostgreSQL en `backend/tests/integration/`.
- Pruebas E2E en `tests/e2e/`.
- Pruebas funcionales HTTP para validar contratos y respuestas.
- La ubicación de las pruebas de Vitest y React Testing Library dentro de `frontend/` no está definida (pendiente).

## 5. Patrones arquitectónicos

| Patrón | Aplicación |
|---|---|
| Layered Architecture | Capas Controller, Service y Repository en `backend/internal/` |
| Service Layer | Lógica de negocio fuera de los controladores |
| Repository | Acceso a PostgreSQL encapsulado |
| Monorepo | Componentes en un repositorio con dependencias separadas |

## 6. Extensión propuesta para el harness

La extensión `AGENTS.md` o `CLAUDE.md`, `.claude/`, `openspec/` y `.github/workflows/` es una **propuesta no implementada**. Su diseño, responsabilidades, límites y justificación están en [`docs/ai/sdd-harness.md`](../ai/sdd-harness.md). En esta ejecución no se ha creado ninguno de esos archivos o directorios.
