# Registro de decisiones arquitectónicas (ADR)

> **Prompt de origen:** §2.1, Prompt 2 — Evaluación y registro de decisiones arquitectónicas (ADR), en [`prompts.md`](../../../prompts.md).
> **Fuente de decisiones aprobadas:** [`README.md`](../../../README.md) §2.1 (tabla "Registro resumido de decisiones") y §2.3 (monorepo).

## Naturaleza de estos registros

Estos archivos se crearon el **2026-10-19**, durante la ejecución documental de la entrega 1. Formalizan decisiones que ya figuraban como aprobadas o pendientes en el README. **No son versiones anteriores ni actas de deliberaciones históricas**, y no reconstruyen comparaciones de alternativas que no se documentaron en su momento.

Para cada ADR:

- **Alternativas consideradas** solo recoge lo que el README documenta, incluidas las exclusiones explícitas. Si no hay registro, se indica "No documentadas en el registro aprobado".
- **Fecha de la decisión** se indica como "No registrada": el README no la recoge.

## Índice

| ID | Título | Estado | Archivo |
|---|---|---|---|
| ADR-D01 | Stack: Next.js + TypeScript y Go + Chi v5 con REST/JSON | Aprobada | [`ADR-D01-stack.md`](ADR-D01-stack.md) |
| ADR-D02 | Backend por capas Controller → Service → Repository con PostgreSQL | Aprobada | [`ADR-D02-backend-layers.md`](ADR-D02-backend-layers.md) |
| ADR-D03 | Infraestructura Docker + Coolify en VPS KVM 4 propio | Aprobada; no desplegada | [`ADR-D03-infrastructure.md`](ADR-D03-infrastructure.md) |
| ADR-D04 | Organización en monorepo | Aprobada | [`ADR-D04-monorepo.md`](ADR-D04-monorepo.md) |
| ADR-P01 | Mecanismo de autenticación | Pendiente | [`ADR-P01-authentication.md`](ADR-P01-authentication.md) |

ADR-D04 se incorporó por decisión del responsable del proyecto durante la planificación de esta ejecución (conflicto C2). Documenta una decisión que ya estaba aprobada en README §2.3; no es una decisión nueva.

## Plantilla utilizada

Contexto y problema · Decisión · Alternativas consideradas · Consecuencias positivas · Consecuencias negativas · Riesgos y limitaciones · Decisiones relacionadas pendientes · Fuente.
