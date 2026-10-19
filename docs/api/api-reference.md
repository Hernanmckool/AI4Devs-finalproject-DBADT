# Referencia de la API REST

> **Prompt de origen:** §4, Prompt 1 — Diseño y documentación del contrato REST API, en [`prompts.md`](../../prompts.md).
> **Fuente de decisiones aprobadas:** [`README.md`](../../README.md) §4; contrato en [`openapi.yaml`](openapi.yaml).
> **Estado del documento:** contrato **propuesto** de exactamente tres operaciones. Los endpoints no están implementados ni desplegados; los ejemplos son ilustrativos.

## 1. Convenciones generales

| Aspecto | Definición | Estado |
|---|---|---|
| Estilo | REST/JSON, prefijo `/api/v1` | Aprobado |
| Versión | `v1` | Aprobado |
| Especificación | OpenAPI 3.0.3 | Aprobado |
| Contrato canónico | [`docs/api/openapi.yaml`](openapi.yaml); README §4 contiene una copia exacta | Aprobado (CC-6) |
| URL base | Pendiente de despliegue y dominio | Pendiente (A8) |
| Autenticación | Endpoints públicos sin sesión; el `PATCH` exige `ADMIN`. `BearerAuth` provisional, **no equivale a JWT** | Pendiente (ADR-P01) |
| Errores | `{error, message, details?}` | Aprobado; catálogo de códigos pendiente (A17) |
| Pagos y disponibilidad | No existen | Aprobado |

## 2. Endpoints

| Método y ruta | Acceso | Historia | Funcionalidad | Éxito | Errores |
|---|---|---|---|---|---|
| `GET /api/v1/attractions` | Público | HU-001 | F01 | `200` | `400`, `500` |
| `POST /api/v1/booking-requests` | Público | HU-002 | F04 | `201` | `400`, `404`, `500` |
| `PATCH /api/v1/booking-requests/{id}/status` | Solo `ADMIN` | HU-003 | F05 | `200` | `400`, `401`, `403`, `404`, `409`, `500` |

No existen otras rutas. La consulta y el filtrado administrativos de HU-003 **no tienen contrato** (A1); antes de implementarlos debe formalizarse y autorizarse cualquier ruta adicional (README §4).

## 3. Parámetros y cuerpos

### 3.1. `GET /api/v1/attractions`

| Parámetro | Ubicación | Tipo | Regla | Por defecto |
|---|---|---|---|---|
| `q` | query | string | Búsqueda por nombre | — |
| `category` | query | string | Filtro por categoría | — |
| `page` | query | integer | ≥ 1 | 1 |
| `limit` | query | integer | 1–100 | 20 |

**Respuesta `200`:** `data` (array de `Attraction`) y `pagination` (`page`, `limit`, `total`, `total_pages`). Solo incluye atractivos activos.

**Criterios de paginación y filtrado.** Lo único aprobado es que existen `q`, `category`, `page` y `limit` con los tipos y rangos del contrato, que solo se devuelven atractivos activos y que búsqueda y filtros "pueden combinarse" (TICKET-001). Las siguientes definiciones son **decisiones técnicas pendientes (A16)** y **requisitos previos a la implementación de HU-001**. El contrato no se modifica.

| Decisión pendiente | Qué hay que definir | Estado |
|---|---|---|
| Semántica exacta de `q` | Coincidencia parcial o exacta; distinción de mayúsculas, minúsculas y acentos; campos sobre los que busca | Pendiente (A16) |
| Identificación de categorías | Si `category` recibe el `slug` o el `id`; el contrato solo declara `string`, y el ejemplo de respuesta muestra `slug` | Pendiente (A16) |
| Ordenación estable | Criterio de orden que permita paginar sin duplicar ni omitir resultados (criterio 7 de TICKET-001) | Pendiente (A16) |
| Filtros combinados | Cómo se combinan `q` y `category` (por ejemplo, si deben cumplirse ambos) | Pendiente (A16). La posibilidad de combinarlos está aprobada; su comportamiento exacto no |
| `page` mayor que `total_pages` | Respuesta esperada | Pendiente (A16) |
| Categoría inexistente | Respuesta esperada | Pendiente (A16) |

### 3.2. `POST /api/v1/booking-requests`

El cuerpo es `BookingRequestCreate`, que es **exactamente uno** de estos dos esquemas (`oneOf`):

| Campo | Alojamiento (`AccommodationBookingRequest`) | Tour (`TourBookingRequest`) |
|---|---|---|
| `accommodation_id` | Obligatorio (UUID) | Omitido o `null` |
| `tour_id` | Omitido o `null` | Obligatorio (UUID) |
| `contact_name` | Obligatorio, mínimo 1 carácter | Obligatorio, mínimo 1 carácter |
| `contact_email` | Obligatorio, formato email | Obligatorio, formato email |
| `contact_phone` | Opcional | Opcional |
| `start_date` | Obligatoria (date) | Obligatoria (date) |
| `end_date` | Obligatoria (date), posterior a `start_date` | Omitida o `null` |
| `people_count` | Obligatorio, ≥ 1 | Obligatorio, ≥ 1 |
| `observations` | Opcional | Opcional |

"`end_date` posterior a `start_date`" no se puede expresar en JSON Schema: lo valida el backend (y el `CHECK` de PostgreSQL).

**Respuesta `201`:** `id`, `status: PENDING`, `message`, `created_at`.

### 3.3. `PATCH /api/v1/booking-requests/{id}/status`

| Elemento | Regla |
|---|---|
| `id` (path) | UUID obligatorio |
| Cuerpo | `{ "status": "CONFIRMED" \| "REJECTED" }`; no admite propiedades adicionales |
| Seguridad | `BearerAuth` provisional; rol `ADMIN` |

**Respuesta `200`:** `id`, `status`, `message`.

## 4. Reglas de validación

| Endpoint | Validación | Capa | Código si falla |
|---|---|---|---|
| `GET` | Tipos y rangos de `page` y `limit` | Controller | `400` |
| `POST` | JSON bien formado, tipos y campos requeridos | Controller | `400` |
| `POST` | Exactamente un servicio | Controller (esquema) y Service | `400` |
| `POST` | Formato de correo | Controller | `400` |
| `POST` | `people_count` ≥ 1 | Controller | `400` |
| `POST` | Alojamiento: `end_date` > `start_date`; tour: sin `end_date` | Service | `400` |
| `POST` | Servicio existente y activo | Service | `404` |
| `PATCH` | UUID válido y `status` permitido | Controller | `400` |
| `PATCH` | Credenciales presentes y válidas | Middleware | `401` |
| `PATCH` | Rol `ADMIN` | Service | `403` |
| `PATCH` | Solicitud existente | Service y Repository | `404` |
| `PATCH` | Estado actual `PENDING`; ninguna resolución concurrente previa | Repository (actualización condicionada) | `409` |
| Todos | Error inesperado | — | `500`, sin detalles internos |

**Validaciones pendientes:** fechas pasadas, antelación y máximo de personas (A12); longitudes máximas (A6); límite de tasa con `429` (C5, pendiente de definición y **no incluido** en el contrato).

## 5. Manejo de errores

| Código HTTP | Significado | `error` de ejemplo (ilustrativo) | Origen del ejemplo |
|---|---|---|---|
| `400` | Validación | `VALIDATION_ERROR` | README §4 |
| `401` | No autenticado | `AUTHENTICATION_REQUIRED` | Esta ejecución |
| `403` | Sin permisos | `FORBIDDEN` | Esta ejecución |
| `404` | Recurso inexistente; servicio inactivo en `POST` | `NOT_FOUND`, `SERVICE_NOT_AVAILABLE` | Esta ejecución |
| `409` | Transición inválida o carrera perdida | `INVALID_STATUS_TRANSITION` | README §4 |
| `500` | Error interno | `INTERNAL_ERROR` | Esta ejecución |

Los valores de `error` que no vienen del README son ejemplos para completar los esquemas (C4); el catálogo definitivo está pendiente (A17). `details` nunca contiene trazas, SQL ni datos de otros registros ([`security.md`](../architecture/security.md#6-validación-de-entradas-ataques-comunes-y-manejo-de-errores)).

## 6. Ejemplos JSON

**`GET /api/v1/attractions?category=historico&page=1&limit=20` → `200`**

```json
{
  "data": [
    {
      "id": "7d2e8aa0-4a73-4de1-92c5-b12e097a4121",
      "name": "Obelisco de Barquisimeto",
      "description": "Monumento emblemático de la ciudad.",
      "location": "Barquisimeto, Lara, Venezuela",
      "latitude": 10.062,
      "longitude": -69.341,
      "categories": [{ "name": "Histórico", "slug": "historico" }],
      "images": []
    }
  ],
  "pagination": { "page": 1, "limit": 20, "total": 1, "total_pages": 1 }
}
```

**`POST /api/v1/booking-requests` (alojamiento) → `201`**

```json
{
  "accommodation_id": "8f7a2e41-1c99-4fd0-9b2c-87d9b10a6e13",
  "contact_name": "María González",
  "contact_email": "maria@example.com",
  "start_date": "2026-12-15",
  "end_date": "2026-12-18",
  "people_count": 2
}
```

```json
{
  "id": "b49ecb72-8a34-4cb2-82a9-bd2c2a9c0f31",
  "status": "PENDING",
  "message": "Tu solicitud fue recibida correctamente.",
  "created_at": "2026-12-10T14:30:00Z"
}
```

**`POST /api/v1/booking-requests` con ambos servicios → `400`**

```json
{
  "error": "VALIDATION_ERROR",
  "message": "La solicitud debe referirse a un alojamiento o a un tour, no a ambos.",
  "details": {
    "accommodation_id": "Excluyente con tour_id.",
    "tour_id": "Excluyente con accommodation_id."
  }
}
```

**`PATCH /api/v1/booking-requests/{id}/status` sobre una solicitud ya resuelta → `409`**

```json
{
  "error": "INVALID_STATUS_TRANSITION",
  "message": "La solicitud ya fue resuelta.",
  "details": { "current_status": "CONFIRMED", "requested_status": "REJECTED" }
}
```

## 7. Diferencias respecto del contrato del README (decisión C4)

Base de comparación: bloque YAML **inicial** de README §4 (versión inicial del repositorio anterior). No cambian rutas, métodos, códigos HTTP declarados ni reglas de negocio.

**Estado tras el cierre documental (CC-6):** `docs/api/openapi.yaml` es la **fuente canónica** del contrato. Se revisaron las nueve diferencias frente al comportamiento aprobado y ninguna lo modifica, por lo que todas están incorporadas. README §4 se sustituyó por una copia exacta del archivo canónico, para no mantener dos contratos que puedan divergir.

| ID | Elemento | README §4 inicial | Contrato canónico | Motivo | Revisión CC-6 |
|---|---|---|---|---|---|
| DF-01 | `BookingRequestCreate` | Un objeto con `accommodation_id` y `tour_id` anulables; exclusividad descrita solo en texto | `oneOf` entre `AccommodationBookingRequest` y `TourBookingRequest`, con campos comunes en `BookingRequestBase` (`allOf`); se conserva la descripción original | Exclusividad formal | Incorporada: expresa RN-10 (README §3.2) |
| DF-02 | `end_date` en alojamiento | Opcional y anulable; obligatoriedad solo en texto | Obligatoria en `AccommodationBookingRequest` | Formaliza RN-14 | Incorporada: regla ya aprobada |
| DF-03 | `end_date` en tour | Anulable; "debe omitirse o ser null" en texto | Solo admite omisión o `null` (`enum: [null]`) | Formaliza RN-15 | Incorporada: regla ya aprobada |
| DF-04 | Referencia del otro servicio | Anulable | Solo admite omisión o `null` en cada variante | Mantiene la semántica `nullable` original | Incorporada: sin cambio de comportamiento |
| DF-05 | `401`, `403`, `404` y `500` | Solo descripción, sin cuerpo | Cuerpo `Error` con ejemplo | Esquemas de error consistentes | Incorporada: los códigos no cambian |
| DF-06 | `400` y `409` | Esquema `Error`; ejemplo solo en `409` | Ejemplos añadidos en todos los `400` | Ejemplos coherentes con el comportamiento | Incorporada |
| DF-07 | `Error` y `BearerAuth` | Sin descripción del alcance de los ejemplos; `BearerAuth` "provisional" | Descripciones que remiten a A17 y ADR-P01 | Trazabilidad de pendientes | Incorporada: la autenticación sigue pendiente |
| DF-08 | `info.description` | "API REST para catálogo turístico y gestión de reservas." | Se añade que documenta solo las tres operaciones y que no incluye pagos ni disponibilidad | Aclarar el alcance | Incorporada |
| DF-09 | Comentarios de cabecera | — | Fuente canónica, origen y estado del contrato | Trazabilidad | Incorporada |

**Sin cambios:** `servers`, los tres `paths`, los métodos, los parámetros, los códigos de respuesta, `Attraction`, `Category`, `AttractionImage`, `BookingCreated`, `BookingStatusUpdate` y `BookingStatusResponse`.

## 8. Validación del contrato en esta ejecución

| Validación | Herramienta | Resultado |
|---|---|---|
| Lint del contrato inicial del README (extraído a un archivo temporal, durante la generación) | `npx @redocly/cli@1.25.0 lint` | Válido; 0 errores; 4 avisos (`info-license` y `operation-operationId` ×3) |
| Lint del contrato canónico `docs/api/openapi.yaml` (validación final del cierre) | `npx @redocly/cli@1.25.0 lint` | Válido; 0 errores; los mismos 4 avisos |
| Equivalencia de README §4 con el canónico | Comparación exacta del bloque YAML | Idéntico |
| Comportamiento de `oneOf` | Script Python temporal con `jsonschema` 4.10.3, convirtiendo `nullable` de OAS 3.0 | 12 de 12 casos con el resultado esperado (válidos: alojamiento, tour y variantes con `null`; inválidos: ambos servicios, ninguno, ambos `null`, alojamiento sin `end_date`, tour con `end_date`, `people_count` 0, sin correo) |

Los avisos no se corrigieron: añadir `license` u `operationId` no estaba autorizado (C4 se limita a esquemas de error y exclusividad). Se registran como pendientes (A17).

## 9. Decisiones pendientes

| Código | Decisión |
|---|---|
| A1 | Contrato de consulta y filtrado administrativo (HU-003) |
| A5 | Esquema de seguridad definitivo |
| A11 | Formato de la referencia devuelta |
| A12 | Validaciones de fechas pasadas, antelación y máximo de personas |
| A16 | Semántica de `q` y `category`, orden y comportamiento fuera de rango |
| A17 | Catálogo de códigos `error`; `operationId` y `license` |
| C5 | Rate limiting y `429` |
