# TICKET-001 — Implementación del catálogo turístico

> **Prompt de origen:** §6, Prompt 1, en [`prompts.md`](../../../prompts.md). **Fuente:** [`README.md`](../../../README.md) §6 (TICKET-001).
> **Estado:** aprobado; **no implementado**. Ticket **representativo** de la primera entrega académica; no forma parte de un backlog completo del MVP ([alcance](README.md#6-trabajo-que-requerirá-tickets-posteriores)).

| Campo | Valor |
|---|---|
| Tipo | Frontend Development |
| Prioridad | Pendiente de definir |
| Estimación | Pendiente de definir (C6): no se asignan valores |
| Sprint | Pendiente de planificación |
| Historia | [HU-001](../../user-stories/HU001.md) |
| Funcionalidad | F01 — Exploración de atractivos turísticos |
| API | `GET /api/v1/attractions` |
| Entidades | `attractions`, `categories`, `attraction_categories`, `attraction_images` |

## 1. Objetivo

Desarrollar en Next.js con TypeScript la interfaz del catálogo de atractivos: explorar, buscar, filtrar y paginar atractivos activos, con estados de carga, vacío y error, y un diseño responsive.

## 2. Alcance

**Incluye:** vistas y componentes del catálogo, consumo del endpoint, estados de interfaz, responsive y accesibilidad de navegación.

**No incluye:** implementar la API, cambiar el esquema de PostgreSQL ni desarrollar otras funcionalidades (README §6).

## 3. Requisitos y escenarios relacionados

| Requisito | Escenario | Requisito funcional del ticket (README) |
|---|---|---|
| HU-001-R01 | S01 | Exploración sin registro |
| HU-001-R02 | S01 | Solo atractivos activos devueltos por la API |
| HU-001-R03 | S03 | Búsqueda por nombre |
| HU-001-R04 | S02 | Filtro por categoría |
| HU-001-R05 | S01 | Nombre, descripción, ubicación y fotografías en el orden de `display_order` |
| HU-001-R06 | S05 | Paginación sin duplicar resultados |
| HU-001-R07 | S04 | Estado vacío informativo |
| — | P-HU001-01 (propuesta) | Combinar búsqueda y filtros |

## 4. Tareas verificables

| ID | Fase | Tarea | Responsable | Evidencia |
|---|---|---|---|---|
| T1-01 | Spec | Revisar HU-001 y el contrato; confirmar los escenarios de activos, filtros, paginación y vacío | Agente de especificaciones + humano | Escenarios aprobados (HAP-01) |
| T1-02 | RED | Pruebas Vitest/RTL de los estados `loading`, `empty` y `error`, de la lista y de la tarjeta | Agente de testing | Salida del fallo esperado |
| T1-03 | RED | Pruebas de búsqueda, filtro, combinación y paginación con respuestas simuladas del contrato | Agente de testing | Salida del fallo esperado |
| T1-04 | GREEN | Componentes reutilizables (tarjeta, búsqueda, filtros, paginación, galería) | Agente implementador | Suite en verde |
| T1-05 | GREEN | Cliente de API y tipos alineados con `openapi.yaml`; el filtrado definitivo queda en el backend | Agente implementador | Suite en verde |
| T1-06 | REFACTOR | Eliminar duplicaciones y revisar la accesibilidad de la navegación | Agente implementador | Suite en verde |
| T1-07 | Verificación | Recorrido Playwright de exploración y filtro, cuando existan API y datos reales | Agente de testing | Resultado real o "no aplicable", con su motivo |
| T1-08 | Verificación | Responsive en móvil y escritorio; teclado y foco visible | Agente de testing + humano | Evidencia de la revisión |
| T1-09 | Revisión | Revisión adversarial y aprobación | Revisor + humano | Hallazgos y decisión |

## 5. Criterios de aceptación (README §6)

1. El visitante puede acceder al catálogo sin iniciar sesión.
2. Solo se muestran atractivos activos devueltos por la API.
3. La búsqueda por nombre encuentra atractivos relacionados con el término.
4. El filtro por categoría devuelve los atractivos correspondientes.
5. La búsqueda y los filtros pueden combinarse.
6. Cada resultado muestra su información turística y las fotografías disponibles.
7. La paginación permite consultar páginas adicionales sin duplicar resultados.
8. Sin coincidencias se muestra un estado vacío informativo.
9. Los errores de la API se presentan con mensajes comprensibles, sin detalles técnicos.
10. La interfaz funciona en resoluciones móviles y de escritorio.
11. Las pruebas automatizadas de los escenarios principales finalizan satisfactoriamente.

## 6. Escenarios alternativos y casos límite

| Caso | Comportamiento esperado |
|---|---|
| Atractivo sin imágenes | La tarjeta se muestra sin galería y sin error |
| Varias imágenes, una principal | La principal se muestra primero y el resto según `display_order` |
| API responde `400` | Mensaje comprensible; filtros recuperables |
| API no disponible | Estado `error` con opción de reintentar |
| Página fuera de rango | Pendiente (A16) |
| Cambio de filtro en una página distinta de la primera | Volver a la primera página (propuesta UX) |

## 7. Guardrails del ticket

GR-01, GR-02, GR-03, GR-05 (consumo coherente con el contrato), GR-06, GR-08, GR-11 y GR-12 ([catálogo](../../ai/sdd-harness.md#7-catálogo-de-guardrails)). Sin cambios en endpoints ni esquema.

## 8. Dependencias

- Contrato aprobado de `GET /api/v1/attractions`.
- Backend disponible para la integración final. No existe ticket de backend para este endpoint ([brecha](README.md#5-brechas-registradas)).
- Datos de prueba para búsquedas, filtros y paginación (TICKET-003, seeds).
- **Requisitos previos:** decisiones A16 (semántica de `q`, `id` o `slug` en `category`, ordenación estable y filtros combinados; ver [HU-001](../../user-stories/HU001.md#requisitos-previos-a-la-implementación)) y A14 (exposición de la API y renderizado).

## 9. Riesgos

| Riesgo | Mitigación |
|---|---|
| El contrato cambia durante el desarrollo con mocks | Tipos derivados del contrato versionado; GR-05 |
| Duplicar el filtrado en el cliente | El filtrado definitivo queda en el backend (README §2.2) |
| Accesibilidad insuficiente | Revisión de teclado y foco en T1-08 |

## 10. Definición de terminado

Los criterios de HU-001 están cubiertos por pruebas relevantes, el contrato no se rompe, los estados `loading`, `empty` y `error` están presentes y la revisión humana acepta la evidencia.
