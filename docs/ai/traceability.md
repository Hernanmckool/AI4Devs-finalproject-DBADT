# Trazabilidad entre prompts y documentación

> **Alcance:** relación entre los 16 prompts de [`prompts.md`](../../prompts.md) y los documentos de `docs/`, y validaciones **realmente ejecutadas** durante la ejecución documental del 2026-10-19.
> **Estado:** registro factual de esta ejecución. El contenido generado está pendiente de revisión humana.

## 1. Distinción temporal

| Momento | Qué ocurrió | Evidencia |
|---|---|---|
| Planificación del proyecto (antes de 2026-10-19) | Se elaboraron el README y los 16 prompts. Según el README §0 del repositorio de respaldo `AI4Devs-finalproject-DBADT-backup` (rama `main`), los prompts son instrucciones estructuradas y aprobadas; **parte se formalizó con el diseño ya avanzado** y no son una transcripción de ejecuciones previas | README §0 del repositorio de respaldo `AI4Devs-finalproject-DBADT-backup`, rama `main` (alcance de la entrega 1) |
| 2026-10-19, 03:10 UTC | Primer commit con `README.md` y `prompts.md` (`d8cc30f`) | Historial de Git del repositorio anterior; el commit fue reemplazado por `--amend` (fila siguiente) |
| 2026-10-19 | Corrección de los encabezados del README sin emojis, con `--amend` (`8d4435f`, único commit de `main` en el repositorio anterior) | Rama `main` del repositorio de respaldo `AI4Devs-finalproject-DBADT-backup` |
| **2026-10-19 (esta ejecución)** | Los 16 prompts se ejecutaron **por primera vez como actividades documentales** para generar `docs/`, con el README como fuente de decisiones aprobadas | Este documento y los 31 archivos de `docs/` |
| **2026-10-19 (cierre documental)** | Correcciones CC-1 a CC-7 autorizadas por el responsable, aplicadas a `docs/` y al README, y nueva validación | [`docs/README.md`](../README.md#correcciones-del-cierre-documental) y §4 |

**Lo que este registro no afirma:**
- Que los prompts se ejecutaran antes de redactar el README.
- Que existan respuestas anteriores de un asistente de IA.
- Que el contenido de `docs/` haya sido aprobado.

No se reconstruye ninguna cronología anterior.

### 1.1. Desarrollo de esta ejecución

| Paso | Descripción | Intervención humana |
|---|---|---|
| 1 | Lectura completa de `README.md` (2.117 líneas) y `prompts.md` (16 prompts) | — |
| 2 | Plan: matriz de prompts, árbol de 30 archivos, conflictos C1–C8 y ambigüedades A1–A10 | — |
| 3 | El responsable del proyecto aprobó el plan con resoluciones para C1–C8 (con ADR-D04, el total pasa a 31 archivos) y autorizó `@redocly/cli` y `@mermaid-js/mermaid-cli` de forma temporal | Aprobación del plan |
| 4 | Generación de los documentos siguiendo el orden lógico de los prompts | — |
| 5 | Validaciones de la generación | — |
| 6 | El responsable revisó el informe de generación y autorizó las correcciones de cierre CC-1 a CC-7, sin nuevas aprobaciones intermedias | Revisión del informe y autorización |
| 7 | Correcciones aplicadas a los documentos existentes (sin recrearlos) y al README; `prompts.md` sin cambios | — |
| 8 | Validación final (§4) | — |
| 9 | Aprobación del contenido final, creación de la rama `feature/entrega1-HPPY`, commit, push y PR001 | **Pendiente** |

**Herramienta utilizada:** Claude Code con el modelo Claude Opus 5.5 (`claude-opus-5-5`), sin harness, skills, hooks ni subagentes del proyecto configurados.

## 2. Matriz de los 16 prompts

| N.º | Prompt | Documento generado | Requisitos relacionados | Validación | Observaciones |
|---|---|---|---|---|---|
| 1 | §1 P1 — Product Discovery | [`product/prd.md`](../product/prd.md) | F01–F07; perfiles Visitante, `TOURIST`, `ADMIN`, prestadores | Enlaces y anclas; checklist de calidad del prompt (prd §11) | La priorización se presenta como alternativas, sin decidir (A9); PQ-06 es una observación nueva |
| 2 | §1 P2 — MVP y flujos de negocio | [`product/business-flows.md`](../product/business-flows.md) | F01–F07; RN-01–RN-46; estados `PENDING`/`CONFIRMED`/`REJECTED` | 3 diagramas Mermaid válidos; enlaces | Documento principal de reglas; detecta A11–A13, A18 y A19 |
| 3 | §1 P3 — UX | [`product/ux-design.md`](../product/ux-design.md) | V-01–V-15; F01–F07 | 1 diagrama Mermaid válido; enlaces | Alternativas de mapa y de reordenamiento con ventajas y limitaciones; sin biblioteca seleccionada |
| 4 | §2.1 P1 — Arquitectura | [`architecture/architecture.md`](../architecture/architecture.md) | Stack aprobado; 3 endpoints; F01–F07 | 4 diagramas Mermaid válidos (1 de arquitectura, 3 de secuencia) | Añade secuencias de consulta y gestión administrativa; §4.1 documenta las dos alternativas de exposición de la API sin elegir (A14, CC-2) |
| 5 | §2.1 P2 — ADR | [`architecture/decisions/`](../architecture/decisions/README.md): índice, ADR-D01, D02, D03, D04, P01 | Decisiones del README §2.1 y §2.3 | Enlaces | "Alternativas: no documentadas" (C1); ADR-D04 por C2; ninguna versión histórica simulada |
| 6 | §2.2 P1 — Componentes | [`architecture/components.md`](../architecture/components.md) | F01–F07; Controller → Service → Repository | 1 diagrama Mermaid válido; enlaces | Reglas exclusivas del backend (§5); sin rutas para las funcionalidades sin contrato |
| 7 | §2.3 P1 — Monorepo y harness | [`architecture/repository-structure.md`](../architecture/repository-structure.md), [`ai/sdd-harness.md`](sdd-harness.md) | Monorepo aprobado; AR-01–AR-10; GR-01–GR-13; HAP-01–HAP-06 | 1 diagrama Mermaid válido; enlaces | No se creó ningún archivo del harness, como exige el prompt |
| 8 | §2.4 P1 — Infraestructura | [`architecture/deployment.md`](../architecture/deployment.md) | VPS KVM 4, Coolify, Docker | 2 diagramas Mermaid válidos | Sin archivos de configuración; backups fuera del VPS principal como requisito aprobado, mecanismo pendiente (A15, CC-1) |
| 9 | §2.5 P1 — Seguridad | [`architecture/security.md`](../architecture/security.md) | Matriz de permisos; SR-01–SR-14 | Enlaces | Evalúa tres alternativas de autenticación sin seleccionar ninguna (ADR-P01) |
| 10 | §2.6 P1 — Testing SDD/TDD | [`architecture/testing-strategy.md`](../architecture/testing-strategy.md) | HU-001-R01 a HU-003-R10; meta del 80 % | 2 diagramas Mermaid válidos; enlaces | Ninguna prueba existe ni se ejecutó; OpenSpec no instalado |
| 11 | §3 P1 — Modelo de datos | [`data/data-model.md`](../data/data-model.md) | 15 tablas; DC-01–DC-18; IX-01–IX-14 | DER válido; 15 entidades contadas | IX-13 e IX-14 son nuevas propuestas; sin SQL de migraciones |
| 12 | §4 P1 — API | [`api/openapi.yaml`](../api/openapi.yaml), [`api/api-reference.md`](../api/api-reference.md) | 3 operaciones aprobadas | Redocly: válido; `oneOf`: 12/12; 3 rutas contadas; README §4 idéntico | Fuente canónica del contrato (CC-6); DF-01–DF-09 revisadas e incorporadas; A16 como requisito previo de HU-001 (CC-3) |
| 13 | §5 P1 — Historias | [`user-stories/HU001.md`](../user-stories/HU001.md), [`HU002.md`](../user-stories/HU002.md), [`HU003.md`](../user-stories/HU003.md) | 7 + 10 + 10 criterios del README | Recuento de criterios igual al README | IDs provisionales, no OpenSpec (C7) |
| 14 | §5 P2 — Validación de historias | [`user-stories/validation-report.md`](../user-stories/validation-report.md) | Las 6 validaciones obligatorias del prompt | Las 6 se cumplen (informe §1) | Escenarios adicionales como propuestas; OBS-01–OBS-08 |
| 15 | §6 P1 — Tickets | [`delivery/tickets/`](../delivery/tickets/README.md): índice y TICKET-001–003 | HU-001–HU-003; 15 tablas | 1 diagrama Mermaid válido; 3 tickets contados y marcados como representativos | Tickets representativos, no backlog del MVP; inventario de trabajo posterior sin generar tickets (CC-5); estimaciones pendientes (C6) |
| 16 | §7 P1 — Pull Requests | [`delivery/pull-requests/pr-process.md`](../delivery/pull-requests/pr-process.md), [`PR-001.md`](../delivery/pull-requests/PR-001.md) | GR-01–GR-13; PR001 | Enlaces | Sin ramas, commits ni PR creados; rama académica confirmada `feature/entrega1-HPPY` (C8, CC-7) |

**Documentos transversales:** [`docs/README.md`](../README.md) (índice, convenciones, resolución C1–C8 y registro de pendientes) y este archivo.

**Total:** 31 archivos (29 específicos de los prompts y 2 transversales).

## 3. Correspondencia con el README

Todos los documentos toman sus decisiones de la sección del README indicada en la "Correspondencia documental" de cada prompt. Durante la generación, el README y `prompts.md` no se modificaron. En el cierre documental, el README se actualizó con autorización expresa para aplicar CC-1 a CC-7: apartado 0.6 de documentación complementaria, líneas de ampliación por sección, contrato §4 sustituido por una copia exacta del canónico, tickets representativos y rama académica. No se cambió ninguna decisión funcional ni arquitectónica. **`prompts.md` no se modificó.**

## 4. Validaciones ejecutadas en esta ejecución

Todas las herramientas se ejecutaron de forma temporal fuera del repositorio (directorio temporal de la sesión y caché de npm). No se añadieron dependencias ni archivos de configuración al proyecto. Los resultados corresponden a la **validación final del cierre documental** (2026-10-19), después de aplicar CC-1 a CC-7. La validación de la generación inicial dio los mismos resultados en todos los controles comunes.

| N.º | Validación | Herramienta y método | Resultado |
|---|---|---|---|
| 1 | Presencia de los 31 archivos de `docs/` | Recuento de archivos | **31** (30 Markdown y 1 YAML) |
| 2 | Enlaces Markdown y referencias internas de `docs/` y `README.md` | Script Python temporal: rutas relativas y anclas con el algoritmo de GitHub, ignorando bloques de código | **269 enlaces y 75 anclas; 0 errores** |
| 3 | Validez de `docs/api/openapi.yaml` (OpenAPI 3.0.3) | `npx @redocly/cli@1.25.0 lint` | **Válido, 0 errores, 4 avisos** (`info-license` y `operation-operationId` ×3; los mismos que tenía el contrato inicial del README) |
| 3b | Exclusividad `accommodation_id`/`tour_id` | Script Python temporal con PyYAML 6.0.1 y `jsonschema` 4.10.3 | **12/12 casos** con el resultado esperado |
| 3c | README §4 equivalente al contrato canónico | Comparación exacta del bloque YAML del README con el archivo | **Idéntico**; el README contiene un único bloque YAML |
| 4 | Solo los tres endpoints aprobados | Recuento de `paths` y operaciones; búsqueda de rutas `/api/v1` en `docs/` | **3 rutas, 3 operaciones**; ninguna otra ruta mencionada |
| 5 | Diagramas Mermaid | `mermaid.parse()` de mermaid 11.17.2 (incluido en `@mermaid-js/mermaid-cli@11.4.0`), en Node, con DOMPurify sustituido por funciones neutras | **Sintaxis válida en 21/21 diagramas** (16 de `docs/` y 5 del README). Control negativo: 3/3 diagramas rotos rechazados. **El render visual no se verificó**: `mmdc` no puede lanzar Chromium (falta `libnss3.so` y su instalación no estaba autorizada) |
| 6 | Contradicciones entre README y `docs/` | Búsqueda automática de restos superados: patrón de rama antiguo, backups de A15 descritos aún como contradicción, conjunción de filtros como aprobada, promesa de contacto al visitante; revisión cruzada de CC-1 a CC-7 | **0 restos.** La revisión cruzada la hizo el asistente; **requiere revisión humana** |
| 7 | Ninguna propuesta pendiente presentada como aprobada | Búsqueda de códigos A en filas con estado "Aprobado"; búsqueda de términos de ejecución sin negación ni condición | 1 fila revisada (`booking_requests.id`: campo aprobado, formato de referencia pendiente; correcto). Las coincidencias de términos son criterios de aceptación futuros o columnas de "control propuesto" del README |
| 8 | Tres tickets identificados como representativos | Recuento y búsqueda en cada ticket | 3 tickets; los 3 incluyen la aclaración; también README §6 e índice de tickets |
| 9 | Emojis en títulos | Búsqueda de pictogramas en encabezados de `docs/` y del README | **0** |
| 10 | `prompts.md` sin modificar | `git diff --quiet HEAD -- prompts.md`; SHA-256 | **Sin cambios** respecto de la versión inicial del repositorio anterior (SHA-256 `ddf8c98a…5da29`, igual al inicial) |
| — | 15 entidades y criterios de las historias | Recuento en el DER y en los archivos HU | 15 entidades; HU-001: 7, HU-002: 10, HU-003: 10 criterios (igual que el README) |

### 4.1. Validaciones no disponibles

| Validación | Motivo |
|---|---|
| Render visual de Mermaid | Faltan bibliotecas del sistema para Chromium; instalarlas no estaba autorizado |
| Lint de estilo Markdown (por ejemplo, markdownlint) | Herramienta no autorizada en esta ejecución |
| Revisión humana del contenido final | Pendiente del responsable del proyecto |
| Pruebas de aplicación, CI, OpenSpec | No existen código, CI ni specs |

## 5. Documentación repetida: análisis

| Contenido repetido | Dónde | Justificación |
|---|---|---|
| DER de las 15 tablas | README §3.1 y `data-model.md` | El documento de datos debe poder leerse solo; el diagrama se copia sin cambios |
| Criterios de aceptación de los tickets | README §6 y `TICKET-00x.md` | Cada ticket debe ser autocontenido para quien lo ejecute |
| Escenarios Gherkin del README | README §5 y `HU00x.md` | Se completan con el resto de criterios aprobados |
| Contrato OpenAPI | README §4 y `openapi.yaml` | El YAML es el artefacto versionable; las diferencias se registran (DF-01–DF-09) |
| Árbol del monorepo | README §2.3 y `repository-structure.md` | Se amplía con el estado actual y el propósito de cada directorio |

Para el resto de temas compartidos se usa un documento principal y enlaces ([`docs/README.md`](../README.md#documento-principal-de-cada-tema-compartido)). No se identificaron documentos innecesarios.

## 6. Lo que no se hizo en esta ejecución

- No se modificó `prompts.md`. `README.md` solo se modificó en el cierre documental, con autorización expresa (CC-1 a CC-7).
- No se generó código de aplicación, migraciones, configuraciones ni archivos del harness.
- No se instalaron dependencias en el proyecto ni herramientas permanentes en el sistema.
- No se crearon ramas, commits ni Pull Requests, y no se hizo push.
- No se ejecutaron despliegues ni se modificaron bases de datos.
- No se usó el ZIP de documentación generado anteriormente.
