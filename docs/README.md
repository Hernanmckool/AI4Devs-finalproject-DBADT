# Documentación ampliada — Descubre Barquisimeto

Esta carpeta contiene la documentación técnica y funcional generada el **2026-10-19**, al ejecutar como actividades documentales los 16 prompts de [`prompts.md`](../prompts.md).

- El [`README.md`](../README.md) principal sigue siendo el documento de presentación del proyecto y la **fuente de las decisiones aprobadas**.
- `docs/` desarrolla los entregables que pide cada prompt, sin modificar esas decisiones.
- La correspondencia entre prompts y documentos está en [`ai/traceability.md`](ai/traceability.md).

**Estado del proyecto:** primera entrega exclusivamente documental. No existe código de aplicación, pruebas, CI, OpenSpec, harness configurado ni despliegue.

## Convenciones de estado

Criterio de estado documental aplicado en el README y en `docs/`. Esta tabla es su referencia vigente:

| Etiqueta | Significado |
|---|---|
| **Aprobado** / **Confirmado** | Decisión de alcance o diseño registrada en el README |
| **Propuesto** / **Previsto** | Técnica, mecanismo o análisis que requiere concretarse o aprobarse |
| **Pendiente** | Decisión abierta; no se resuelve en la documentación |
| **Nueva propuesta de esta ejecución** | Recomendación elaborada el 2026-10-19 que no figura en el README; requiere aprobación |
| **Implementado** / **Verificado** | Solo con evidencia real en el repositorio o en una ejecución. No se usa para ningún componente del producto |

Los identificadores documentales (`RN-xx`, `HU-00x-Rxx`, `HU-00x-Sxx`, `GR-xx`, `DC-xx`, `IX-xx`, `DF-xx`, `OBS-xx`) se crearon en esta ejecución para trazar el contenido. **No son specs OpenSpec ni artefactos ejecutados.**

## Mapa de lectura

| Área | Documento | Prompt de origen |
|---|---|---|
| Producto | [`product/prd.md`](product/prd.md) | §1, Prompt 1 |
| Producto | [`product/business-flows.md`](product/business-flows.md) | §1, Prompt 2 |
| Producto | [`product/ux-design.md`](product/ux-design.md) | §1, Prompt 3 |
| Arquitectura | [`architecture/architecture.md`](architecture/architecture.md) | §2.1, Prompt 1 |
| Arquitectura | [`architecture/decisions/`](architecture/decisions/README.md) (ADR-D01–D04, ADR-P01) | §2.1, Prompt 2 |
| Arquitectura | [`architecture/components.md`](architecture/components.md) | §2.2 |
| Arquitectura | [`architecture/repository-structure.md`](architecture/repository-structure.md) | §2.3 |
| Arquitectura | [`architecture/deployment.md`](architecture/deployment.md) | §2.4 |
| Arquitectura | [`architecture/security.md`](architecture/security.md) | §2.5 |
| Arquitectura | [`architecture/testing-strategy.md`](architecture/testing-strategy.md) | §2.6 |
| Datos | [`data/data-model.md`](data/data-model.md) | §3 |
| API | [`api/openapi.yaml`](api/openapi.yaml), [`api/api-reference.md`](api/api-reference.md) | §4 |
| Historias | [`user-stories/HU001.md`](user-stories/HU001.md), [`HU002.md`](user-stories/HU002.md), [`HU003.md`](user-stories/HU003.md) | §5, Prompt 1 |
| Historias | [`user-stories/validation-report.md`](user-stories/validation-report.md) | §5, Prompt 2 |
| Entrega | [`delivery/tickets/`](delivery/tickets/README.md) (TICKET-001–003) | §6 |
| Entrega | [`delivery/pull-requests/pr-process.md`](delivery/pull-requests/pr-process.md), [`PR-001.md`](delivery/pull-requests/PR-001.md) | §7 |
| IA | [`ai/sdd-harness.md`](ai/sdd-harness.md) | §2.3 (harness) |
| IA | [`ai/traceability.md`](ai/traceability.md) | Transversal |

## Documento principal de cada tema compartido

Para evitar duplicaciones, cada tema tiene un único documento principal; los demás lo enlazan.

| Tema | Documento principal |
|---|---|
| Actores, reglas funcionales y estados de la solicitud | [`business-flows.md`](product/business-flows.md) |
| Matriz de permisos | [`security.md`](architecture/security.md#3-matriz-de-permisos-por-perfil) |
| Restricciones físicas, índices y migraciones | [`data-model.md`](data/data-model.md) |
| Validaciones HTTP y códigos de respuesta | [`api-reference.md`](api/api-reference.md) |
| Catálogo de guardrails | [`sdd-harness.md`](ai/sdd-harness.md#7-catálogo-de-guardrails) |
| Criterios Gherkin aprobados y propuestos | `HU00x.md` / [`validation-report.md`](user-stories/validation-report.md) |

## Resolución de conflictos de la planificación

Decisiones del responsable del proyecto, tomadas al aprobar el plan de esta ejecución.

| ID | Conflicto | Resolución |
|---|---|---|
| C1 | Los ADR piden alternativas, pero no hay comparación histórica | "No documentadas en el registro aprobado"; sin inventar alternativas |
| C2 | El monorepo no tenía ADR | Se incorpora [ADR-D04](architecture/decisions/ADR-D04-monorepo.md) como registro de una decisión ya aprobada |
| C3 | `HU-001` frente a `HU001` | IDs del README en el contenido; nombres de archivo propuestos |
| C4 | Huecos del contrato OpenAPI | Esquemas de error completos y exclusividad formal; diferencias en [`api-reference.md`](api/api-reference.md#7-diferencias-respecto-del-contrato-del-readme-decisión-c4) |
| C5 | Rate limiting sin `429` | `429` pendiente de definición; no se añade |
| C6 | Estimación de tickets | Pendiente; sin valores inventados |
| C7 | Tickets ligados a specs inexistentes | IDs documentales provisionales, no OpenSpec |
| C8 | PR001 y rama | Rama de referencia `feature/entrega1-HPPY`; no se crean ramas ni PR ([`PR-001.md`](delivery/pull-requests/PR-001.md)) |

## Correcciones del cierre documental

Tras revisar el informe de generación, el responsable del proyecto autorizó estas correcciones. Se numeran CC-1 a CC-7 para distinguirlas de los conflictos C1–C8 de la planificación.

| ID | Corrección | Aplicación |
|---|---|---|
| CC-1 | Backups fuera del VPS principal como requisito aprobado; mecanismo, proveedor, frecuencia, retención y recuperación pendientes | `deployment.md`, ADR-D03, README §2.4; A15 redefinido |
| CC-2 | Dos alternativas de exposición de la API documentadas sin elegir ninguna | `architecture.md` §4.1, `deployment.md`, `security.md`, README §2.1 y §2.4 |
| CC-3 | Semántica de `q`, `id` o `slug` en `category`, orden estable y filtros combinados como pendientes y requisitos previos de HU-001 | `api-reference.md`, HU001, TICKET-001, `business-flows.md`, `validation-report.md`, README §4 y §5 |
| CC-4 | Reglas de reserva mantenidas; referencia, fechas pasadas y comunicación posterior pendientes, sin asumir notificaciones | `ux-design.md`, `prd.md`, `business-flows.md`, HU002, README §1.2 y §5 |
| CC-5 | Los tres tickets son representativos de la entrega académica, no el backlog del MVP | `tickets/README.md` (§6, inventario de trabajo posterior), TICKET-001 a 003, README §6 |
| CC-6 | `docs/api/openapi.yaml` como fuente canónica; README §4 con una copia exacta; DF-01 a DF-09 revisadas e incorporadas | `openapi.yaml`, `api-reference.md`, README §4 |
| CC-7 | Rama académica `feature/entrega1-HPPY` | README §7, `PR-001.md` |

`README.md` se modificó en este cierre (correcciones anteriores y apartado 0.6 de documentación complementaria). `prompts.md` no se modificó.

## Registro de pendientes

A1–A10 se identificaron en la planificación. A11–A20 se detectaron durante esta ejecución. Ninguno se resuelve en la documentación.

| ID | Pendiente | Documentos afectados |
|---|---|---|
| A1 | Contrato de consulta y filtrado administrativo de HU-003 (no está entre los tres endpoints) | HU003, api-reference, architecture, validation-report |
| A2 | Filtro por "ubicación" en F02 y F03 sin campo estructurado | business-flows, ux-design, data-model |
| A3 | Significado de "intereses" en F01 | business-flows, HU001 |
| A4 | Mecanismo y persistencia de la auditoría de cambios de estado | security, data-model, HU003 |
| A5 | Mecanismo de autenticación (ADR-P01) | security, ADR-P01, components, HU003 |
| A6 | Tamaños de `VARCHAR`, precisión de `DECIMAL`, zona horaria de `TIMESTAMP`, valores por defecto | data-model, TICKET-003, security |
| A7 | Funciones de `ADMIN` sobre los recorridos | business-flows, security |
| A8 | Ambientes, dominios, backups (frecuencia y retención), RTO/RPO, rollback | deployment, ADR-D03 |
| A9 | Priorización MoSCoW y secuencia de F01–F07 | prd |
| A10 | Pruebas y contratos de F02, F03, F06 y F07 | testing-strategy, components, architecture |
| A11 | Formato del número de referencia de la solicitud | business-flows, HU002, api-reference |
| A12 | Fechas pasadas, antelación, máximo de personas, solicitudes duplicadas | business-flows, HU002, api-reference |
| A13 | Uso del planificador sin cuenta (borrador no guardado) | business-flows, ux-design, prd |
| A14 | Exposición de la API: accesible desde el navegador mediante HTTPS, o privada y consumida a través del servidor Next.js; estrategia de renderizado (CC-2) | architecture §4.1, deployment, security |
| A15 | Mecanismo y proveedor del almacenamiento de backups fuera del VPS principal. El requisito de almacenarlos fuera está aprobado (CC-1) | deployment, ADR-D03 |
| A16 | Semántica de `q`, `id` o `slug` en `category`, ordenación estable, filtros combinados, página o categoría fuera de rango. Requisitos previos de HU-001 (CC-3) | api-reference, HU001, TICKET-001, data-model |
| A17 | Catálogo de códigos `error`; `operationId` y `license` en OpenAPI | api-reference, openapi.yaml |
| A18 | Motivo de rechazo y comunicación del resultado al visitante | business-flows, HU003, prd |
| A19 | Estrategia de reordenamiento frente a la unicidad de posiciones | data-model, business-flows |
| A20 | Borrado físico y acciones referenciales de las FK | data-model |
| C5 | Parámetros de rate limiting y código `429` | security, api-reference |
| C6 | Prioridad, estimación y sprint de los tickets | delivery/tickets |
| C8 | Creación de la rama `feature/entrega1-HPPY`, commit, publicación y apertura de PR001 (requieren autorización expresa) | PR-001 |
