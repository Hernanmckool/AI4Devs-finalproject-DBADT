# ADR-D01 — Stack: Next.js + TypeScript y Go + Chi v5 con REST/JSON

| Campo | Valor |
|---|---|
| Estado | Aprobada |
| Fecha de la decisión | No registrada |
| Fecha de este registro | 2026-10-19 (ejecución documental de la entrega 1) |
| Fuente | [`README.md`](../../../README.md) §0.3, §2.1 y §2.2 |

## Contexto y problema

La plataforma necesita una interfaz web adaptable a móviles, tablets y computadoras, con vistas públicas y vistas autenticadas para turistas y administradores. También necesita una API que concentre las reglas de negocio (solicitudes, estados, permisos y recorridos) y que el frontend consuma mediante un contrato explícito.

## Decisión

- Frontend: **Next.js con TypeScript**.
- Backend: **Go con el router Chi v5**.
- Comunicación: **REST/JSON** con prefijo `/api/v1`, documentada con OpenAPI 3.0.3.

## Alternativas consideradas

No documentadas en el registro aprobado. El README indica expresamente que "no se reconstruye una comparación histórica formal de alternativas".

## Consecuencias positivas

- Frontend y backend separados, con ciclos de prueba independientes.
- El tipado de TypeScript y de Go ayuda a mantener la coherencia con el contrato.
- La API independiente permite verificar las reglas de negocio sin depender de la interfaz.

## Consecuencias negativas

- Dos ciclos de compilación, ejecución y despliegue que hay que coordinar (README §2.1).
- El contrato API debe mantenerse sincronizado entre ambos lados.

## Riesgos y limitaciones

| Riesgo | Mitigación prevista | Estado |
|---|---|---|
| Desincronización entre frontend y contrato | Contrato OpenAPI versionado y control GR-05 ([`sdd-harness.md`](../../ai/sdd-harness.md#7-catálogo-de-guardrails)) | Propuesto |
| Duplicación de reglas entre frontend y backend | Reglas autoritativas solo en el backend ([`components.md`](../components.md#5-reglas-que-se-ejecutan-exclusivamente-en-el-backend)) | Aprobado como criterio |

## Decisiones relacionadas pendientes

- Estrategia de renderizado de Next.js y exposición de la API (A14).
- Mecanismo de autenticación ([ADR-P01](ADR-P01-authentication.md)).
