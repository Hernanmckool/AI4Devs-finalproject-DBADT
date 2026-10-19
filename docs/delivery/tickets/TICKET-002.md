# TICKET-002 — Implementación de solicitudes de reserva

> **Prompt de origen:** §6, Prompt 1, en [`prompts.md`](../../../prompts.md). **Fuente:** [`README.md`](../../../README.md) §6 (TICKET-002).
> **Estado:** aprobado; **no implementado**. Ticket **representativo** de la primera entrega académica; no forma parte de un backlog completo del MVP ([alcance](README.md#6-trabajo-que-requerirá-tickets-posteriores)).

| Campo | Valor |
|---|---|
| Tipo | Backend Development |
| Prioridad | Pendiente de definir |
| Estimación | Pendiente de definir (C6): no se asignan valores |
| Sprint | Pendiente de planificación |
| Historia | [HU-002](../../user-stories/HU002.md) |
| Funcionalidad | F04 — Solicitudes de reserva |
| API | `POST /api/v1/booking-requests` |
| Entidades | `booking_requests`, `accommodations`, `tours` |

## 1. Objetivo

Implementar en Go con Chi v5, por capas Controller → Service → Repository, el registro público de solicitudes de reserva de alojamientos y tours. El backend valida los datos, verifica que el servicio exista y esté activo, y persiste la solicitud en `PENDING`.

## 2. Alcance

**Incluye:** endpoint `POST`, validaciones, verificación del servicio, persistencia y manejo de errores.

**No incluye:** pagos, disponibilidad en tiempo real, notificaciones automáticas ni el `PATCH` administrativo (README §1.2 y §6).

## 3. Requisitos y escenarios relacionados

| Requisito | Escenario | Criterio del ticket (README) |
|---|---|---|
| HU-002-R01 | S01 | 1. Sin autenticación |
| HU-002-R02 | S04, P-HU002-05 | 10. Sin solicitudes para servicios inexistentes o desactivados |
| HU-002-R03 | S05 | 6. Nombre y correo válidos |
| HU-002-R04 | S06 | Teléfono y observaciones opcionales |
| HU-002-R05 | S03 | 8. Fechas válidas de alojamiento |
| HU-002-R06 | S02, P-HU002-03 | 9. Sin fecha de salida en tours |
| HU-002-R08 | S01, S02 | 2, 3. Registro en `PENDING` |
| HU-002-R09 | S01 | 11. `201`, identificador y `PENDING` |
| — | P-HU002-01, P-HU002-02 | 4, 5. Exclusividad del servicio |
| — | P-HU002-04 | 7. `people_count` > 0 |

## 4. Tareas verificables

| ID | Fase | Tarea | Responsable | Evidencia |
|---|---|---|---|---|
| T2-01 | Spec | Revisar HU-002, los escenarios y el YAML del `POST` | Agente de especificaciones + humano | HAP-01 |
| T2-02 | RED | Pruebas `httptest`: alojamiento y tour válidos, campos ausentes, ambos servicios o ninguno, fechas inválidas, tour con salida, `people_count` 0, sin autenticación | Agente de testing | Fallo esperado |
| T2-03 | RED | Pruebas unitarias del Service con repositorio doble: servicio inexistente o inactivo y reglas por tipo | Agente de testing | Fallo esperado |
| T2-04 | RED | Pruebas de integración con PostgreSQL aislado: persistencia en `PENDING`, `CHECK` de exclusividad y de fechas | Agente de testing | Fallo esperado |
| T2-05 | GREEN | Controller: decodificación, validación estructural y traducción de errores a HTTP | Agente implementador | Suite en verde |
| T2-06 | GREEN | Service: reglas RN-10 a RN-18 y verificación del servicio activo | Agente implementador | Suite en verde |
| T2-07 | GREEN | Repository: consulta del servicio e inserción parametrizada | Agente implementador | Suite en verde |
| T2-08 | REFACTOR | Errores de dominio unificados; sin lógica de negocio en el Controller | Agente implementador | Suite en verde |
| T2-09 | Verificación | Coherencia con OpenAPI; cobertura del Service; `govulncheck`; errores sin datos personales | CI / agente de testing | Resultados reales |
| T2-10 | Revisión | Revisión adversarial y aprobación | Revisor + humano | Hallazgos y decisión |

## 5. Criterios de aceptación (README §6)

1. El endpoint permite registrar solicitudes sin autenticación.
2. Una solicitud válida de alojamiento se registra en `PENDING`.
3. Una solicitud válida de tour se registra en `PENDING`.
4. No se permite enviar `accommodation_id` y `tour_id` a la vez.
5. No se permite una solicitud sin servicio.
6. Se rechazan solicitudes sin nombre o con un correo inválido.
7. Se rechaza `people_count` ≤ 0.
8. Se requieren fechas válidas de entrada y salida para alojamientos.
9. No se admite fecha de salida en tours.
10. No se admiten servicios inexistentes o desactivados.
11. Una solicitud válida devuelve `201 Created`, identificador y `PENDING`.
12. Los datos se almacenan correctamente en PostgreSQL.
13. Validación: `400`; servicio inexistente o inactivo: `404`.
14. Los errores internos no exponen información sensible.
15. Las pruebas unitarias y de integración de los escenarios principales finalizan satisfactoriamente.

## 6. Escenarios alternativos y casos límite

| Caso | Tratamiento |
|---|---|
| Salida igual a la entrada | `400` |
| `accommodation_id: null` junto con un `tour_id` válido | Válido como tour (DF-04 en [`api-reference.md`](../../api/api-reference.md#7-diferencias-respecto-del-contrato-del-readme-decisión-c4)) |
| JSON mal formado o tipos incorrectos | `400` |
| Servicio desactivado entre la verificación y la inserción | Pendiente ([`data-model.md`](../../data/data-model.md#71-solicitudes-de-reserva)) |
| Violación de una restricción de PostgreSQL no anticipada por el Service | Se informa como error controlado sin detalles de SQL; el código HTTP exacto está pendiente |
| Fechas pasadas, máximo de personas | Pendiente (A12) |

## 7. Guardrails del ticket

GR-01 a GR-06, GR-08 a GR-12 ([catálogo](../../ai/sdd-harness.md#7-catálogo-de-guardrails)). GR-05 verifica que solo existe la ruta `POST /api/v1/booking-requests` y que respeta el contrato.

## 8. Dependencias

- TICKET-003: tablas `booking_requests`, `accommodations` y `tours` con sus restricciones.
- Contrato OpenAPI aprobado del `POST`.
- Datos de prueba de alojamientos y tours activos e inactivos.

## 9. Riesgos

| Riesgo | Mitigación |
|---|---|
| Validaciones divergentes entre el Service y PostgreSQL | Pruebas de integración de ambas capas |
| Datos personales en logs | Revisión en T2-09; regla AR-07 |
| Abuso del endpoint público | Rate limiting previsto; parámetros y `429` pendientes (C5) |

## 10. Definición de terminado

Las solicitudes válidas se guardan con identificador único y en `PENDING`, las inválidas no se persisten, las pruebas y los controles relevantes pasan y existe aprobación humana. No se implementa cobro, disponibilidad en tiempo real ni rutas no aprobadas.
