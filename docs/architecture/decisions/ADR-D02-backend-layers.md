# ADR-D02 — Backend por capas Controller → Service → Repository con PostgreSQL

| Campo | Valor |
|---|---|
| Estado | Aprobada |
| Fecha de la decisión | No registrada |
| Fecha de este registro | 2026-10-19 (ejecución documental de la entrega 1) |
| Fuente | [`README.md`](../../../README.md) §2.1, §2.2, §2.3 y §3 |

## Contexto y problema

Las reglas centrales del producto (solicitud con un solo servicio, validación de fechas por tipo, transiciones `PENDING → CONFIRMED | REJECTED`, concurrencia entre administradores y propiedad de los recorridos) tienen que ser verificables y quedar aisladas de los detalles de HTTP y SQL. Los datos son relacionales y requieren integridad referencial.

## Decisión

- Backend organizado en tres capas:
  - **Controller:** contrato HTTP, lectura y validación inicial, respuestas.
  - **Service:** reglas de negocio y autorización.
  - **Repository:** acceso a datos y transacciones.
- Persistencia en **PostgreSQL**, con claves foráneas, `CHECK`, `UNIQUE` e índices.

## Alternativas consideradas

No documentadas en el registro aprobado. El README deja constancia de exclusiones explícitas, sin una evaluación comparativa:

- Microservicios: "no forman parte del diseño adoptado" (README §2.1).
- Arquitectura hexagonal: "sin introducir microservicios ni arquitecturas hexagonales que no hayan sido definidas para el proyecto" (README §2.2).

## Consecuencias positivas

- Los servicios de negocio pueden probarse de forma aislada; sobre ellos aplica la meta del 80 % de cobertura (README §2.6).
- Las restricciones de PostgreSQL complementan las reglas del servicio (columna "Responsable" de [`data-model.md` §5](../../data/data-model.md#5-restricciones-de-integridad)).
- La API depende de capas con responsabilidades claras.

## Consecuencias negativas

- Más archivos y capas que un enfoque sin separación.
- Riesgo de sobrefragmentar servicios si se aplican capas sin criterio (README §2.1).

## Riesgos y limitaciones

| Riesgo | Mitigación prevista | Estado |
|---|---|---|
| Reglas duplicadas entre Service y PostgreSQL con resultados distintos | Responsable de cada restricción en [`data-model.md` §5](../../data/data-model.md#5-restricciones-de-integridad) y pruebas de integración | Propuesto |
| Lógica de negocio filtrada al Controller | Revisión adversarial y criterios de PR ([`pr-process.md`](../../delivery/pull-requests/pr-process.md)) | Propuesto |
| Condiciones de carrera en las transiciones | Actualización condicionada y atómica en el Repository | Aprobado como requisito; diseño en [`data-model.md`](../../data/data-model.md#71-solicitudes-de-reserva) |

## Decisiones relacionadas pendientes

- Biblioteca de acceso a PostgreSQL y de migraciones: no seleccionadas. Cualquier incorporación requiere aprobación.
