# ADR-D04 — Organización en monorepo

| Campo | Valor |
|---|---|
| Estado | Aprobada |
| Fecha de la decisión | No registrada |
| Fecha de este registro | 2026-10-19 (ejecución documental de la entrega 1) |
| Origen del registro | Incorporado por decisión del responsable del proyecto (conflicto C2) para documentar una decisión ya aprobada |
| Fuente | [`README.md`](../../../README.md) §2.3 y §2.4; contexto de los prompts §2.1 y §2.4 en [`prompts.md`](../../../prompts.md) |

## Contexto y problema

El proyecto tiene frontend, backend, base de datos, pruebas E2E y documentación que evolucionan juntos: un cambio en el contrato API afecta a la vez al backend, al frontend, a las pruebas y a la documentación.

## Decisión

Un único repositorio GitHub (`AI4Devs-finalproject-DBADT`) con directorios separados: `frontend/`, `backend/`, `database/`, `tests/e2e/` y `docs/`. Cada componente mantiene sus propias dependencias y procesos de ejecución (README §2.3, patrón "Monorepo").

## Alternativas consideradas

No documentadas en el registro aprobado.

## Consecuencias positivas

- Un cambio de contrato y sus consecuencias se revisan en un mismo Pull Request.
- Trazabilidad única entre historias, specs, tests y código.
- Coolify puede construir cada componente desde su directorio (README §2.4).

## Consecuencias negativas

- Los controles de CI deben limitarse por ruta para no ejecutar todo en cada cambio.
- Conviven dos ecosistemas de dependencias (Go y Node.js).

## Riesgos y limitaciones

| Riesgo | Mitigación prevista | Estado |
|---|---|---|
| Acoplamiento accidental entre `frontend/` y `backend/` | Comunicación solo mediante el contrato REST | Aprobado como criterio |
| CI lento o ruidoso | Controles condicionados por ruta ([`pr-process.md`](../../delivery/pull-requests/pr-process.md#2-controles-ci-previstos-y-condiciones-de-bloqueo)) | Propuesto |

## Decisiones relacionadas pendientes

Ninguna específica. La extensión del harness (`AGENTS.md`, `.claude/`, `openspec/`, `.github/workflows/`) es una propuesta no implementada ([`sdd-harness.md`](../../ai/sdd-harness.md)).
