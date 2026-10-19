# TICKET-003 — Implementación del modelo de datos PostgreSQL

> **Prompt de origen:** §6, Prompt 1, en [`prompts.md`](../../../prompts.md). **Fuente:** [`README.md`](../../../README.md) §6 (TICKET-003) y §3.
> **Estado:** aprobado; **no implementado**. Ticket **representativo** de la primera entrega académica; no forma parte de un backlog completo del MVP ([alcance](README.md#6-trabajo-que-requerirá-tickets-posteriores)). No existen migraciones ni esquema físico.

| Campo | Valor |
|---|---|
| Tipo | Database Development |
| Prioridad | Pendiente de definir |
| Estimación | Pendiente de definir (C6): no se asignan valores |
| Sprint | Pendiente de planificación |
| Historias | Soporte de datos para HU-001, HU-002 y HU-003 |
| Funcionalidades | F01–F07 |
| Referencia de diseño | [`data-model.md`](../../data/data-model.md) |

## 1. Objetivo

Implementar el modelo de datos en PostgreSQL con **migraciones versionadas** que creen las **15 tablas** aprobadas, con integridad referencial, restricciones, índices y pruebas de integridad.

## 2. Alcance

**Incluye:** esquema, migraciones en `database/migrations/`, datos sintéticos en `database/seeds/`, restricciones, relaciones, índices y pruebas de integridad.

**No incluye:** endpoints Go ni interfaces Next.js. La estrategia de backups pertenece a [`deployment.md`](../../architecture/deployment.md).

## 3. Entidades a implementar (15)

| Grupo | Tablas |
|---|---|
| Usuarios | `users` |
| Categorías | `categories`, `attraction_categories`, `tour_categories` |
| Atractivos | `attractions`, `attraction_images` |
| Alojamientos | `accommodations`, `amenities`, `accommodation_amenities`, `accommodation_images` |
| Tours | `tours`, `tour_images` |
| Reservas | `booking_requests` |
| Planificador | `travel_plans`, `travel_plan_items` |

## 4. Requisitos y restricciones relacionados

| Origen | Restricciones del modelo |
|---|---|
| HU-001-R02, R04 | `is_active`; relaciones N:M de categorías (DC-06); IX-04 |
| HU-002-R05, R08 | DC-10 (exclusividad), DC-11, DC-12 (fechas), DC-13 (`PENDING` por defecto) |
| HU-003-R07, R08 | DC-13 (valores de estado). Las transiciones se aplican en el backend (DC-14) |
| F07 | DC-15 a DC-17 |
| Catálogo | DC-01 a DC-09 |

Detalle de cada restricción e índice en [`data-model.md`](../../data/data-model.md#5-restricciones-de-integridad).

## 5. Tareas verificables

| ID | Fase | Tarea | Responsable | Evidencia |
|---|---|---|---|---|
| T3-01 | Spec | Revisar el DER, el diccionario, DC-01 a DC-18 e IX-01 a IX-12; confirmar o resolver A6, A19 y A20 antes de escribir las migraciones | Agente de especificaciones + humano | HAP-01 y decisiones registradas |
| T3-02 | RED | Pruebas de integridad: exclusividad de la reserva, fechas, unicidad, imagen principal única, posiciones únicas con atractivos repetibles, valor por defecto `PENDING`, conservación histórica | Agente de testing | Fallo esperado sobre una base sin esquema |
| T3-03 | GREEN | Migraciones ordenadas por dependencia (niveles 0, 1 y 2 de [`data-model.md`](../../data/data-model.md#8-estrategia-de-migraciones-y-evolución-del-esquema)) | Agente implementador | Pruebas en verde en la base aislada |
| T3-04 | GREEN | Reversión de cada migración cuando sea segura | Agente implementador | Ejecución de ida y vuelta en la base de prueba |
| T3-05 | GREEN | Seeds sintéticos: activos e inactivos, categorías y servicios | Agente implementador | Carga en la base de prueba |
| T3-06 | REFACTOR | Revisar nombres, índices y orden | Agente implementador | Pruebas en verde |
| T3-07 | Verificación | Contrastar el esquema real con el DER: exactamente 15 tablas, sin entidades adicionales | CI / agente de testing | GR-07 |
| T3-08 | Revisión | Revisión adversarial y aprobación; cualquier desviación se documenta antes | Revisor + humano | Hallazgos y decisión |

IX-13 e IX-14 son propuestas nuevas de esta ejecución: requieren aprobación antes de incluirse.

## 6. Criterios de aceptación (README §6)

1. Se crean correctamente las 15 tablas aprobadas.
2. Se definen claves primarias y foráneas.
3. Las relaciones N:M utilizan tablas intermedias.
4. Se impiden asociaciones duplicadas.
5. Se restringen los tipos de alojamiento y los roles permitidos.
6. No puede haber dos fotos principales en una misma galería.
7. Una reserva no puede asociarse a la vez a un alojamiento y a un tour.
8. Se aplican las restricciones de fecha y de cantidad de personas.
9. Una solicitud nueva recibe `PENDING` por defecto cuando no se informa el estado.
10. La desactivación lógica conserva reservas y referencias históricas.
11. Los recorridos admiten atractivos repetidos, pero no posiciones duplicadas.
12. Se crean los índices definidos.
13. Las migraciones se ejecutan sin errores sobre una base nueva.
14. Las pruebas de integración verifican las restricciones de integridad.
15. El esquema implementado corresponde al diagrama aprobado.

## 7. Escenarios alternativos y casos límite

| Caso | Tratamiento |
|---|---|
| Reordenar posiciones dentro de un día | Depende de A19 (restricción diferible u otra estrategia) |
| Borrado físico de un alojamiento con solicitudes | Depende de A20; la regla aprobada es la desactivación lógica |
| Coordenadas en los límites (±90, ±180) | Aceptadas |
| `display_order` igual a 0 | Aceptado ("no negativo") |
| Tour con `duration_minutes` nulo | Aceptado ("cuando se informe") |

## 8. Guardrails del ticket

GR-01, GR-02, GR-03, GR-06, GR-07, GR-11 y GR-12 ([catálogo](../../ai/sdd-harness.md#7-catálogo-de-guardrails)). Toda migración destructiva requiere HAP-06.

## 9. Dependencias

- DER y restricciones aprobados (README §3).
- PostgreSQL disponible para migraciones y pruebas en un entorno aislado.
- Selección de la herramienta de migraciones (pendiente; requiere aprobación).
- Decisiones A6, A19 y A20.

## 10. Riesgos

| Riesgo | Mitigación |
|---|---|
| Decisiones físicas no definidas (tamaños, zona horaria) | Resolver A6 en T3-01 |
| Desviación respecto del DER | GR-07 y T3-07 |
| Migración irreversible aplicada por error | Aplicar solo en una base aislada; HAP-06 |

## 11. Definición de terminado

Las 15 tablas y restricciones aprobadas existen en el entorno de prueba, las migraciones son reproducibles, las pruebas de integridad están en verde y existe revisión humana. **No** se declara creado el esquema físico de producción.
