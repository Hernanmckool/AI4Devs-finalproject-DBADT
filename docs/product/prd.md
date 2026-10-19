# PRD — Descubre Barquisimeto

> **Prompt de origen:** §1, Prompt 1 — Definición estratégica del producto (Product Discovery), en [`prompts.md`](../../prompts.md).
> **Fuente de decisiones aprobadas:** [`README.md`](../../README.md) §0, §1.1 y §1.2.
> **Estado del documento:** desarrollo documental de la entrega 1, pendiente de revisión humana. Ninguna capacidad descrita está implementada.
> **Convenciones de estado:** ver [`docs/README.md`](../README.md#convenciones-de-estado).

## 1. Visión del producto

Descubre Barquisimeto será la plataforma web de una agencia digital de turismo que reúne, en un único lugar, la información que necesita un visitante para conocer Barquisimeto y sus alrededores (estado Lara, Venezuela) y planificar su estadía: atractivos, alojamientos, tours, ubicación geográfica, solicitudes de reserva y recorridos personalizados.

| Elemento | Definición | Estado |
|---|---|---|
| Visión | Ser el punto de entrada digital para descubrir y organizar una visita a Barquisimeto y sus alrededores. | Aprobado (README §0.3, §1.1) |
| Problema principal | La información turística está dispersa; el visitante consulta múltiples fuentes para conocer destinos, alojamientos y actividades. | Aprobado (README §1.1) |
| Problema secundario | Planificar la visita y expresar interés en una reserva exige contactar por separado a cada prestador. | Aprobado (README §1.1) |
| Problema operativo | La agencia necesita recibir y resolver solicitudes de forma ordenada y con control de acceso. | Aprobado (README §1.2, F05) |

## 2. Análisis de necesidades

### 2.1. Problemas del visitante al descubrir y organizar actividades

| Código | Problema identificado | Capacidad que lo atiende |
|---|---|---|
| NV-01 | No sabe qué lugares visitar ni cómo se clasifican por interés. | F01 |
| NV-02 | No encuentra en un mismo sitio opciones de hospedaje comparables. | F02 |
| NV-03 | Desconoce qué experiencias guiadas existen, su duración y punto de encuentro. | F03 |
| NV-04 | Para manifestar interés en un alojamiento o tour debe buscar el contacto de cada prestador. | F04 |
| NV-05 | No comprende dónde se encuentra cada lugar ni su cercanía relativa. | F06 |
| NV-06 | No puede organizar por días los lugares que quiere visitar ni recuperar esa organización después. | F07 |

### 2.2. Necesidades operativas de la agencia

| Código | Necesidad operativa | Capacidad que la atiende |
|---|---|---|
| NA-01 | Recibir solicitudes con datos suficientes para contactar al visitante. | F04 |
| NA-02 | Consultar, filtrar y resolver solicitudes pendientes. | F05 |
| NA-03 | Evitar que dos miembros del personal resuelvan la misma solicitud de forma contradictoria. | F05 |
| NA-04 | Restringir el acceso administrativo al personal autorizado. | F05 |
| NA-05 | Mantener actualizada la información publicada del catálogo. | F01–F03 (curación editorial; frecuencia pendiente) |

La diferencia entre ambos grupos es la base de los perfiles de acceso: el visitante consume información pública y emite solicitudes; la agencia opera sobre datos personales y estados, por lo que requiere autenticación y autorización.

## 3. Objetivos de negocio y propuesta de valor

**Objetivos cualitativos (aprobados, README §1.1):**

1. Reunir información turística dispersa en una plataforma única.
2. Reducir los pasos necesarios para conocer y solicitar experiencias.
3. Facilitar la gestión interna de las solicitudes por la agencia.
4. Dar visibilidad indirecta a los prestadores turísticos de la región.

**Indicadores:** no existe línea base de visitantes, conversión ni reservas. No se definen métricas cuantitativas ni se citan estadísticas de mercado; los indicadores se fijarán cuando existan datos medibles (README §1.1).

**Propuesta de valor diferencial:**

| Para | Valor | Diferencia frente a consultar fuentes dispersas |
|---|---|---|
| Visitante | Descubrir, ubicar y solicitar en un mismo recorrido de navegación | Un solo punto de consulta y un formulario uniforme de solicitud |
| Turista registrado | Guardar y recuperar recorridos organizados por días | La planificación persiste entre accesos |
| Agencia | Bandeja ordenada de solicitudes con estados controlados | Evita resoluciones contradictorias y centraliza el contacto |
| Prestadores (indirecto) | Visibilidad mediante la agencia | Sin portal propio en el MVP |

## 4. Público objetivo y perfiles de usuario

| Perfil | Objetivo principal | Necesidades | Acceso | Estado |
|---|---|---|---|---|
| Visitante anónimo | Conocer lugares, alojamientos y tours; solicitar una reserva | NV-01 a NV-05 | Público, sin sesión; puede enviar solicitudes | Aprobado |
| Turista registrado (`TOURIST`) | Guardar y recuperar recorridos personalizados | NV-06, además de las públicas | Autenticado; mecanismo pendiente (A5) | Aprobado como perfil |
| Personal de la agencia (`ADMIN`) | Revisar y resolver solicitudes | NA-01 a NA-04 | Autenticado y autorizado | Aprobado como perfil |
| Prestadores turísticos | Visibilidad de su oferta | Promoción indirecta | Sin rol ni portal en el MVP | Aprobado como beneficiario indirecto |

El público incluye turistas nacionales e internacionales, visitantes y residentes (README §1.1). La necesidad de soportar varios idiomas para visitantes internacionales no está definida; se registra como pregunta abierta (PQ-05).

## 5. Funcionalidades agrupadas por capacidades

Las siete funcionalidades F01–F07 constituyen el alcance funcional aprobado del producto. Se agrupan aquí por la capacidad de negocio a la que contribuyen.

| Capacidad | Funcionalidad | Necesidad que responde | Valor que aporta | Estado |
|---|---|---|---|---|
| Descubrimiento | F01 — Exploración de atractivos turísticos | NV-01 | Catálogo clasificado, búsqueda y fichas | Aprobada; HU-001 documentada |
| Descubrimiento | F02 — Catálogo de hoteles, posadas y alojamientos | NV-02 | Comparación de opciones de hospedaje | Aprobada; sin HU representativa |
| Descubrimiento | F03 — Tours y experiencias turísticas | NV-03 | Información de itinerario descriptivo, duración y punto de encuentro | Aprobada; sin HU representativa |
| Ubicación | F06 — Mapa turístico interactivo | NV-05 | Contexto geográfico y acceso a fichas | Aprobada; sin HU representativa |
| Solicitud | F04 — Solicitudes de reserva | NV-04, NA-01 | Expresar interés sin cuenta ni pago | Aprobada; HU-002 documentada |
| Operación | F05 — Gestión de solicitudes por la agencia | NA-02 a NA-04 | Resolución controlada de solicitudes | Aprobada; HU-003 documentada |
| Planificación | F07 — Planificador personalizado de recorridos | NV-06 | Itinerarios propios persistentes | Aprobada; sin HU representativa |

El detalle de cada funcionalidad está en README §1.2; las reglas funcionales se desarrollan en [`business-flows.md`](business-flows.md).

## 6. Flujos funcionales principales

| Flujo | Inicio | Resultado | Actor | Documento de detalle |
|---|---|---|---|---|
| BF-01 Descubrir un atractivo | Inicio o catálogo | Ficha consultada con ubicación | Visitante | [`business-flows.md`](business-flows.md#bf-01--descubrimiento-y-exploración) |
| BF-02 Solicitar alojamiento o tour | Ficha de un servicio activo | Solicitud registrada en `PENDING` con referencia | Visitante | [`business-flows.md`](business-flows.md#bf-02--solicitud-de-reserva) |
| BF-03 Resolver una solicitud | Bandeja administrativa | Solicitud en `CONFIRMED` o `REJECTED` | `ADMIN` | [`business-flows.md`](business-flows.md#bf-03--gestión-administrativa-de-solicitudes) |
| BF-04 Planificar un recorrido | Catálogo o mapa | Recorrido guardado y recuperable | `TOURIST` | [`business-flows.md`](business-flows.md#bf-04--planificación-de-un-recorrido-personalizado) |

## 7. Propuesta preliminar de priorización del MVP

**Estado: pendiente de decisión humana (A9).** La priorización por versiones y MoSCoW no está aprobada; este apartado no la decide. Solo hay dos hechos aprobados:

- Las siete funcionalidades definen el alcance del producto, pero no deben desarrollarse todas en la segunda entrega.
- Para la documentación académica se seleccionaron tres historias representativas: HU-001 (F01), HU-002 (F04) y HU-003 (F05).

Para facilitar la decisión se presentan dos alternativas de secuenciación, ambas compatibles con el alcance aprobado:

| Alternativa | Orden sugerido | Ventajas | Limitaciones |
|---|---|---|---|
| A — Flujo representativo primero | F01 → F04 → F05, luego F02/F03, F06 y F07 | Coincide con HU-001–HU-003 y con los tres tickets; recorre consulta, solicitud y resolución de punta a punta | F04 necesita alojamientos o tours activos (F02/F03), aunque sea como datos de prueba; F05 depende de resolver la autenticación (A5) y el listado administrativo (A1) |
| B — Catálogo completo primero | F01, F02, F03 y F06 → F04 → F05 → F07 | El catálogo queda coherente antes de recibir solicitudes | Retrasa la validación del flujo de solicitud, que es el de mayor riesgo de reglas; se aleja del orden de las historias documentadas |

Con cualquiera de las dos, F07 depende de la decisión de autenticación (A5) y de la cuenta `TOURIST`.

## 8. Funcionalidades que podrían considerarse en fases futuras

Las siguientes capacidades están **explícitamente fuera del MVP** según el README. Se listan como candidatas a evaluar; ninguna está aprobada para una fase concreta.

| Capacidad excluida | Fuente de la exclusión | Motivo de exclusión |
|---|---|---|
| Cobro o pago en línea | README §1.2, F02–F04 | Aumenta el alcance operativo, legal y de seguridad |
| Comprobación automática o en tiempo real de disponibilidad | README §1.2 | Requiere integración con prestadores |
| Integración obligatoria con operadores o proveedores | README §1.2 | Dependencia externa no aprobada |
| Generación de itinerarios mediante IA | README §1.2, F07 | Fuera de alcance |
| Optimización de rutas | README §1.2, F07 | Fuera de alcance |
| Portal de autogestión de prestadores | README §1.1 | Sin rol aprobado |
| Notificaciones automáticas de solicitudes | README §1.2; [TICKET-002](../delivery/tickets/TICKET-002.md) (alcance) | Excluidas del registro backend |

## 9. Decisiones que aumentan la complejidad del MVP

| Decisión | Por qué aumenta la complejidad | Estado |
|---|---|---|
| Mecanismo de autenticación | Condiciona F05, F07, sesiones, CSRF y pruebas de seguridad | Pendiente (A5) |
| Contrato del listado administrativo de solicitudes | HU-003 lo requiere, pero no está entre los tres endpoints | Pendiente (A1) |
| Filtros por ubicación en F02/F03 | El modelo solo tiene `address` y `meeting_point` como texto | Pendiente (A2) |
| Uso del planificador sin cuenta | Un borrador no persistido añade estado en el cliente | Pendiente (A13) |
| Contenido en varios idiomas | Afecta el modelo de contenido y la UX | Pregunta abierta (PQ-05) |

## 10. Riesgos, dependencias, supuestos y preguntas abiertas

### 10.1. Riesgos

| Riesgo | Consecuencia | Tratamiento previsto | Estado |
|---|---|---|---|
| Información turística desactualizada | Consultas con datos incorrectos | Curación editorial por la agencia | Aprobado; frecuencia pendiente |
| El visitante interpreta `PENDING` como reserva confirmada | Expectativas equivocadas | Mensaje explícito de recepción, sin garantía de disponibilidad | Aprobado |
| Autenticación sin definir | Bloquea F05 y F07 | Resolver antes de implementarlas | Pendiente (A5) |
| F01–F07 tratadas como implementación simultánea | Alcance excesivo | Ejecución incremental | Aprobado; prioridad pendiente (A9) |

### 10.2. Dependencias

- F04 depende de que existan alojamientos (F02) o tours (F03) activos.
- F05 depende de F04 y de la autorización `ADMIN`.
- F06 depende de las coordenadas de los catálogos.
- F07 depende de F01 y de la cuenta `TOURIST`.

### 10.3. Supuestos

| Supuesto | Estado |
|---|---|
| Mecanismo de comunicación posterior con el visitante tras resolver la solicitud | Pendiente (A18); no se asume ningún mecanismo de notificación ni de contacto |
| El contenido del catálogo lo carga y mantiene la agencia | Supuesto; el mecanismo de carga del contenido no está definido (PQ-06) |
| Una solicitud corresponde a un único alojamiento o tour | Aprobado |

### 10.4. Preguntas abiertas

| Código | Pregunta |
|---|---|
| PQ-01 | ¿Qué prioridad y secuencia tendrán F01–F07? (A9) |
| PQ-02 | ¿Con qué frecuencia y criterio se actualizarán las fichas turísticas? |
| PQ-03 | ¿Qué detalles de interacción tendrá el panel administrativo? (README §1.2) |
| PQ-04 | ¿Cómo informará la agencia al visitante el resultado de su solicitud? (A18) |
| PQ-05 | ¿Debe el contenido estar disponible en más de un idioma? |
| PQ-06 | ¿Cómo se cargará y mantendrá el contenido del catálogo? No existe una funcionalidad aprobada de administración de catálogo. |

## 11. Validación de calidad del entregable

| Pregunta del prompt | Resultado |
|---|---|
| ¿Cada funcionalidad responde a una necesidad identificada? | Sí: tablas de §2 y §5 (NV-01 a NV-06, NA-01 a NA-05). |
| ¿Están representados los turistas y el personal de la agencia? | Sí: §2.1, §2.2 y §4. |
| ¿Los flujos principales tienen un principio y un resultado claro? | Sí: §6, desarrollados en `business-flows.md`. |
| ¿Las recomendaciones se distinguen de las decisiones aprobadas? | Sí: columna de estado y §7 marcado como pendiente. |
| ¿Hay funcionalidades que aumenten innecesariamente la complejidad? | No se añaden funcionalidades; §9 identifica las decisiones que podrían aumentarla. |
| ¿Quedaron identificadas las decisiones pendientes? | Sí: §7, §9 y §10.4, enlazadas al [registro central](../README.md#registro-de-pendientes). |

PQ-06 (carga de contenido) es una observación nueva de esta ejecución: el README no describe cómo se cargan los atractivos, alojamientos y tours. No se propone ninguna funcionalidad para resolverlo.
