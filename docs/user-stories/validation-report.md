# Validación de historias de usuario y criterios de aceptación

> **Prompt de origen:** §5, Prompt 2 — Validación de historias de usuario y criterios de aceptación, en [`prompts.md`](../../prompts.md).
> **Objeto de la auditoría:** [HU-001](HU001.md), [HU-002](HU002.md) y [HU-003](HU003.md), frente a F01–F07, el [modelo de datos](../data/data-model.md) y el [contrato API](../api/openapi.yaml).
> **Estado del documento:** auditoría documental. Todas las mejoras son **propuestas** pendientes de aprobación del Product Owner. No se crean historias, endpoints ni reglas de negocio.

## 1. Validaciones obligatorias

| Validación exigida por el prompt | Resultado | Evidencia |
|---|---|---|
| HU-001 contempla filtros y paginación | Cumple | HU-001-R04, HU-001-R06; parámetros `category`, `page` y `limit` |
| HU-002 permite solicitudes públicas sin registro | Cumple | HU-002-R01; `security: []` en el `POST` |
| Toda solicitud nueva comienza en `PENDING` | Cumple | HU-002-R08; `BookingCreated.status` con `enum: [PENDING]`; DC-13 |
| HU-003 requiere autorización administrativa | Cumple | HU-003-R01, HU-003-R02; `401` y `403` en el `PATCH` |
| Solo `PENDING → CONFIRMED` y `PENDING → REJECTED` | Cumple | HU-003-R07, HU-003-R08; `BookingStatusUpdate` con `enum: [CONFIRMED, REJECTED]`; `409` |
| Sin pagos ni disponibilidad en tiempo real | Cumple | HU-002-R10; ninguna ruta ni campo de pago o disponibilidad |

## 2. Evaluación de calidad

| Criterio | HU-001 | HU-002 | HU-003 |
|---|---|---|---|
| Formato Como / Quiero / Para | Correcto | Correcto | Correcto |
| Valor de negocio explícito | Sí | Sí | Sí |
| Criterios medibles y convertibles en pruebas | Sí, salvo la semántica de búsqueda (A16) | Sí | R01, R02 y R06–R10 sí; R03–R05 sin contrato (A1) |
| Coherencia con la API | Total | Total | Parcial: la consulta y el filtrado no tienen endpoint |
| Coherencia con el modelo de datos | Total | Total | R03–R05 consultables en `booking_requests`; sin columnas de auditoría (A4) |
| Independencia | Alta | Depende de datos de F02 y F03 | Depende de HU-002 y de A5 |
| Tamaño | Adecuado | Adecuado | Grande: consulta, filtrado y resolución en una sola historia |

## 3. Escenarios faltantes y casos límite

Escenarios **propuestos** para completar el Gherkin. No modifican requisitos aprobados: los que dependen de una decisión pendiente se marcan así.

### 3.1. HU-001

```gherkin
  # Propuesta P-HU001-01 — combinación de búsqueda y filtro (TICKET-001)
  # El resultado esperado depende de A16 (comportamiento de los filtros combinados)
  Scenario: Búsqueda combinada con filtro de categoría
    Given que existen atractivos activos con "Plaza" en el nombre en varias categorías
    When el visitante busca "Plaza" y filtra por la categoría "Histórico"
    Then el resultado respeta el comportamiento de combinación que se apruebe en A16

  # Propuesta P-HU001-02 — parámetros fuera de rango
  Scenario: Tamaño de página inválido
    When se consulta el catálogo con limit igual a 0 o mayor que 100
    Then la API responde 400 con un error de validación

  # Propuesta P-HU001-03 — depende de A16
  Scenario: Página posterior a la última
    Given que el catálogo tiene 1 página de resultados
    When se consulta la página 5
    Then el comportamiento esperado queda pendiente de definir (A16)
```

**Otros casos límite:** atractivo sin imágenes (el ejemplo del contrato muestra `images: []`); atractivo con varias categorías que aparece una sola vez en el filtro; categoría inexistente (A16); resultados estables entre páginas (requiere un orden definido, A16).

### 3.2. HU-002

```gherkin
  # Propuesta P-HU002-01 — exclusividad del servicio
  Scenario: Solicitud con alojamiento y tour a la vez
    When el visitante envía accommodation_id y tour_id en la misma solicitud
    Then la API responde 400
    And no se crea ningún registro

  # Propuesta P-HU002-02 — sin servicio
  Scenario: Solicitud sin servicio identificado
    When se envía una solicitud sin accommodation_id ni tour_id
    Then la API responde 400

  # Propuesta P-HU002-03 — tour con salida
  Scenario: Tour con fecha de salida
    When se envía una solicitud de tour con end_date
    Then la API responde 400

  # Propuesta P-HU002-04 — cantidad de personas
  Scenario: Cantidad de personas igual a cero
    When se envía people_count igual a 0
    Then la API responde 400

  # Propuesta P-HU002-05 — servicio inexistente
  Scenario: Servicio inexistente
    When se envía un accommodation_id que no existe
    Then la API responde 404
    And no se crea ningún registro
```

**Otros casos límite:** salida igual a la entrada (cubierto por S03: "anterior o igual"); correo repetido en varias solicitudes (permitido, sin unicidad); servicio desactivado mientras se completa el formulario; fechas pasadas (A12); envíos duplicados por doble clic (la interfaz deshabilita el botón, pero el backend no deduplica, A12).

### 3.3. HU-003

```gherkin
  # Propuesta P-HU003-01 — estado no permitido
  Scenario: Estado solicitado inválido
    Given que un ADMIN autenticado gestiona una solicitud PENDING
    When solicita el estado "PENDING" o un valor desconocido
    Then la API responde 400
    And la solicitud no cambia

  # Propuesta P-HU003-02 — solicitud inexistente
  Scenario: Solicitud inexistente
    Given que un ADMIN autenticado
    When intenta resolver una solicitud con un identificador que no existe
    Then la API responde 404
```

**Otros casos límite:** credenciales expiradas (depende de A5); `id` con formato no UUID (`400`); propiedades adicionales en el cuerpo (`400`, por `additionalProperties: false`); confirmar una solicitud cuyo servicio fue desactivado después de enviarla (no definido; se registra como observación OBS-06).

## 4. Matriz de trazabilidad funcional

| Historia | Requisitos | Funcionalidad | API | Datos | Ticket | Pruebas ([`testing-strategy.md`](../architecture/testing-strategy.md#6-matriz-de-trazabilidad-requisito--prueba)) |
|---|---|---|---|---|---|---|
| HU-001 | R01–R07 | F01 | `GET /api/v1/attractions` | `attractions`, `categories`, `attraction_categories`, `attraction_images` | TICKET-001 (frontend); TICKET-003 (datos) | Contrato, Service, integración, Vitest/RTL, E2E |
| HU-002 | R01–R10 | F04 (F02, F03) | `POST /api/v1/booking-requests` | `booking_requests`, `accommodations`, `tours` | TICKET-002 (backend); TICKET-003 (datos) | Contrato, Service, integración, E2E |
| HU-003 | R01–R10 | F05 | `PATCH /api/v1/booking-requests/{id}/status` (R03–R05 sin contrato) | `booking_requests` | Sin ticket específico; TICKET-003 (datos) | Service, integración, contrato |

## 5. Observaciones pendientes de aprobación

| ID | Observación | Propuesta | Referencia |
|---|---|---|---|
| OBS-01 | HU-003-R03 a R05 no tienen contrato API | Mantener la brecha documentada; no inventar rutas; decidir antes de implementar | A1 |
| OBS-02 | No existe ticket para HU-003 entre los tres aprobados | Mantener los tres tickets; registrar la ausencia para la planificación | README §6 |
| OBS-03 | La combinación de búsqueda y filtro está en TICKET-001, pero no en los criterios de HU-001 | Incorporar P-HU001-01 como escenario, si el Product Owner lo aprueba | — |
| OBS-04 | La semántica de búsqueda condiciona HU-001-S03 | Definir A16 | A16 |
| OBS-05 | "Número de referencia" de HU-002-R09 | Definir si es el `id` | A11 |
| OBS-06 | Confirmar una solicitud cuyo servicio se desactivó después | Definir si se permite | Nueva; sin código A |
| OBS-07 | HU-003 agrupa consulta, filtrado y resolución | Valorar dividirla en el refinamiento, sin crear historias nuevas ahora | — |
| OBS-08 | La comunicación del resultado al visitante no está en ninguna historia | Definir el canal y el motivo de rechazo | A18 |

Ninguna observación se ha aplicado a los archivos de historia: las historias conservan los criterios aprobados.
