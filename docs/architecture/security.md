# Seguridad y protección de datos

> **Prompt de origen:** §2.5, Prompt 1 — Diseño de seguridad y protección de datos, en [`prompts.md`](../../prompts.md).
> **Fuente de decisiones aprobadas:** [`README.md`](../../README.md) §2.5; reglas de [`business-flows.md`](../product/business-flows.md).
> **Estado del documento:** requisitos y controles **propuestos**. Ninguna medida está implementada ni verificada. No se afirman conformidad legal ni certificaciones.

Este documento es la referencia principal de la **matriz de permisos**.

## 1. Activos y datos tratados

| Activo | Datos | Sensibilidad |
|---|---|---|
| Solicitudes de reserva | `contact_name`, `contact_email`, `contact_phone`, `observations`, fechas, personas | Datos personales de visitantes |
| Cuentas | `name`, `email`, `password_hash`, `role` | Datos personales y credenciales |
| Recorridos | Plan del turista vinculado a su cuenta | Datos personales asociados a hábitos |
| Catálogo | Atractivos, alojamientos, tours e imágenes | Información pública; requiere integridad |
| Secretos | Credenciales de la base de datos y del mecanismo de autenticación | Críticos |

## 2. Superficies de ataque

| Superficie | Exposición | Riesgos principales |
|---|---|---|
| Vistas públicas del frontend | Pública | XSS mediante contenido dinámico; scraping |
| `GET /api/v1/attractions` | Pública | Parámetros maliciosos, consultas costosas, abuso de volumen |
| `POST /api/v1/booking-requests` | Pública, sin autenticación | Spam, inyección, cargas grandes, recolección de datos ajenos |
| `PATCH /api/v1/booking-requests/{id}/status` | Autenticada `ADMIN` | Elevación de privilegios, acceso indebido, condiciones de carrera |
| Acceso y sesión (`TOURIST` y `ADMIN`) | Pública | Fuerza bruta, robo de sesión, CSRF si se usan cookies |
| Recorridos de turistas | Autenticada | Acceso a recorridos ajenos (IDOR) |
| PostgreSQL | Privada | Exposición accidental, credenciales filtradas |
| Coolify y VPS | Administrativa | Acceso no autorizado a despliegues y secretos |
| Repositorio y CI | GitHub | Filtración de secretos, cambios no revisados |
| Logs y backups | Interna | Divulgación de datos personales |

## 3. Matriz de permisos por perfil

**Requisito funcional aprobado (README §2.5); mecanismo de autenticación pendiente.**

| Operación | Visitante | `TOURIST` | `ADMIN` | Estado |
|---|---|---|---|---|
| Explorar atractivos, alojamientos y tours | Sí | Sí | Sí | Aprobado |
| Enviar solicitud de reserva | Sí | Sí | Sí | Aprobado |
| Guardar y editar sus propios recorridos | No | Sí | No definido | Aprobado; A7 pendiente |
| Consultar recorridos de otros usuarios | No | No | No definido | A7 pendiente |
| Consultar y resolver solicitudes de terceros | No | No | Sí | Aprobado |
| Crear cuentas administrativas | No | No | Solo por procedimiento autorizado | Aprobado; flujo técnico pendiente |

**Por endpoint aprobado:**

| Endpoint | Visitante | `TOURIST` | `ADMIN` | Respuesta si no autorizado |
|---|---|---|---|---|
| `GET /api/v1/attractions` | Sí | Sí | Sí | — |
| `POST /api/v1/booking-requests` | Sí | Sí | Sí | — |
| `PATCH /api/v1/booking-requests/{id}/status` | No | No | Sí | `401` sin autenticar; `403` con rol distinto de `ADMIN` |

Las solicitudes no se vinculan a una cuenta: `booking_requests` no tiene `user_id`. Un `TOURIST` autenticado tampoco puede consultar "sus" solicitudes; es una consecuencia del modelo aprobado, no un control adicional.

## 4. Evaluación de mecanismos de autenticación

**Estado: pendiente de aprobación ([ADR-P01](decisions/ADR-P01-authentication.md)).** Este análisis se elabora por primera vez en esta ejecución y no selecciona ningún mecanismo.

| Alternativa | Descripción | Ventajas | Limitaciones | Implicaciones |
|---|---|---|---|---|
| A — Sesión en servidor con cookie | El backend emite un identificador de sesión en una cookie `HttpOnly` y `Secure`; el estado de la sesión se guarda en el servidor | Revocación inmediata; el token no es accesible desde JavaScript | Requiere protección CSRF; necesita almacenar las sesiones, y el modelo aprobado no tiene tabla para ello | Añadir almacenamiento de sesiones afectaría al modelo de 15 tablas, lo que requiere aprobación |
| B — Token firmado emitido por el backend (por ejemplo, JWT) | Token portador con expiración, enviado en la cabecera `Authorization` o en una cookie | Sin estado de sesión en el servidor; encaja con el `BearerAuth` provisional | Revocación difícil antes de expirar; si se guarda en el navegador, se expone a XSS; gestión de claves de firma | Requiere decidir dónde se guarda, cuánto dura y cómo se rota |
| C — Proveedor de identidad externo | Delegar la autenticación en un servicio de terceros | Menos lógica de credenciales propia | **Introduce un servicio externo, que requiere autorización expresa** (Prompt §2.5); dependencia y costo | Afectaría a ADR-D03 (infraestructura propia) |

**Criterios sugeridos para decidir:** capacidad de revocar sesiones de `ADMIN`, protección frente a XSS y CSRF, impacto en el modelo de datos, complejidad de pruebas, ajuste a la exposición de la API (A14) y ausencia de servicios externos no autorizados.

**Pendientes asociados:** algoritmo de hash de contraseñas; política de expiración; bloqueo o ralentización tras intentos fallidos; recuperación de contraseña (no figura en el alcance aprobado).

## 5. Matriz de riesgos y controles

| ID | Riesgo | Superficie | Control propuesto | Validación posterior | Estado |
|---|---|---|---|---|---|
| SR-01 | Acceso indebido a solicitudes | API y panel `ADMIN` | Autenticación y verificación de rol en el backend | Pruebas de 401/403 y acceso cruzado | Propuesto |
| SR-02 | Inyección SQL | Parámetros y cuerpos | Consultas parametrizadas; nunca concatenar entradas | Pruebas con entradas maliciosas | Propuesto |
| SR-03 | Datos inválidos | Formularios y API | Validación en Go de tipos, formatos, longitudes y reglas; restricciones de PostgreSQL | Pruebas de validación por campo | Propuesto |
| SR-04 | XSS | Contenido del catálogo y observaciones mostradas en el panel | Salida escapada; sin HTML sin sanear | Revisión y pruebas de componentes | Propuesto |
| SR-05 | CSRF | Operaciones autenticadas con cookies | Protección CSRF si se adopta cookie (alternativa A) | Pruebas específicas | Condicionado a A5 |
| SR-06 | Abuso de endpoints públicos | `GET` y `POST` públicos | Límites de tamaño, tiempo y tasa | Pruebas de carga y respuesta controlada | Propuesto; parámetros y `429` pendientes (C5) |
| SR-07 | Divulgación de datos personales | Respuestas, logs y backups | Minimización; logs sin contacto ni observaciones; backups protegidos | Revisión de payloads y logs | Propuesto |
| SR-08 | Filtración de credenciales | Repositorio, CI y despliegue | Secretos en Coolify; nada en Git; permisos mínimos | Revisión de configuraciones sin exponer valores | Propuesto; herramienta de detección no seleccionada |
| SR-09 | Fuerza bruta en el acceso | Acceso `TOURIST` y `ADMIN` | Detección de intentos fallidos reiterados | Pruebas de seguridad | Propuesto; mecanismo pendiente (A5) |
| SR-10 | Resoluciones contradictorias | `PATCH` | Actualización condicionada y atómica; `409` | Prueba concurrente de integración | Aprobado como requisito |
| SR-11 | Acceso a recorridos ajenos | Funcionalidad F07 | Verificación de propiedad en el Service | Pruebas de acceso cruzado | Propuesto; sin contrato API (A10) |
| SR-12 | Fuga de información interna en errores | Toda la API | Mensajes genéricos; detalle solo en logs internos | Pruebas de `500` sin trazas | Propuesto |
| SR-13 | Vulnerabilidades en dependencias | Go y Next.js | `govulncheck`; revisión de dependencias de Next.js | Ejecución en CI | Propuesto; herramienta para Next.js no seleccionada |
| SR-14 | Exposición de PostgreSQL | Infraestructura | Sin puerto público; red privada | Revisión de la configuración de Coolify | Aprobado |

## 6. Validación de entradas, ataques comunes y manejo de errores

- **Validación en dos niveles:** el Controller valida formato y tipos (`400`) y el Service valida las reglas (`400`, `404`, `409`). Ver [`api-reference.md`](../api/api-reference.md#4-reglas-de-validación).
- **Longitudes máximas** de nombres, correo, teléfono y observaciones: no definidas (dependen de A6). Deben fijarse antes de implementar para limitar la superficie de abuso.
- **Tamaño del cuerpo y tiempo de petición** limitados en el middleware; los valores están pendientes.
- **Errores:** formato `{error, message, details}`. `details` nunca incluye trazas, SQL ni datos de otros registros.
- **Cabeceras de seguridad HTTP** apropiadas; la lista concreta está pendiente.
- **CORS** restringido a orígenes autorizados si la API resulta accesible desde el navegador (alternativa A de A14). Las implicaciones de seguridad de ambas alternativas están en [`architecture.md` §4.1](architecture.md#41-exposición-de-la-api-decisión-pendiente-a14).

## 7. Controles por componente

| Componente | Controles |
|---|---|
| Frontend | Escapado de contenido; sin secretos en el código del cliente; validación de ayuda no autoritativa; CSRF y almacenamiento de sesión según A5 |
| Middleware | Autenticación; límites de tamaño, tiempo y tasa; registro sin datos personales |
| Controllers | Validación estricta de entrada; rechazo de tipos inesperados; respuestas de error estandarizadas |
| Services | Autorización por rol y propiedad; reglas de negocio; errores de dominio sin detalles internos |
| Repositories | SQL parametrizado; transacciones; actualización condicionada |
| PostgreSQL | FK, `CHECK`, `UNIQUE`; usuario de aplicación con permisos mínimos; red privada |
| Docker y Coolify | Imágenes base actualizadas; variables secretas; acceso restringido al panel |
| GitHub y CI | Revisión obligatoria; secretos de CI con permisos mínimos; controles de seguridad ([`pr-process.md`](../delivery/pull-requests/pr-process.md)) |

## 8. Protección de datos personales

- Solo se recogen los datos necesarios para gestionar la solicitud (README §2.5).
- Los datos de contacto solo son accesibles para `ADMIN`.
- Los logs no registran datos personales innecesarios.
- Desarrollo y pruebas usan datos sintéticos.
- **Retención:** no definida. Cuánto tiempo se conservan las solicitudes resueltas y los datos de contacto está pendiente.
- **Requisitos legales:** no se han determinado los requisitos de protección de datos aplicables. Este documento no los infiere ni declara su cumplimiento.

## 9. Auditoría y registro de eventos

| Evento | Información mínima propuesta | Estado |
|---|---|---|
| Acceso administrativo correcto o fallido | Momento, identidad o intento, resultado | Requisito aprobado; persistencia pendiente (A4) |
| Cambio de estado de una solicitud | Solicitud, estado anterior y nuevo, administrador, momento | Requisito aprobado; el modelo no tiene columnas para ello (A4) |
| Intentos de transición inválida o `409` | Solicitud y administrador | Propuesto |
| Intentos de autenticación fallidos reiterados | Origen y frecuencia | Aprobado como objetivo; mecanismo pendiente |

**A4:** registrar la auditoría en logs estructurados o en la base de datos es una decisión pendiente. Persistirla en PostgreSQL exigiría modificar el modelo de 15 tablas, lo que requiere aprobación.

## 10. Decisiones pendientes

| Código | Decisión |
|---|---|
| A4 | Mecanismo y persistencia de la auditoría |
| A5 | Mecanismo de autenticación (§4) |
| A7 | Permisos de `ADMIN` sobre recorridos |
| A14 | Exposición de la API, CORS |
| C5 | Parámetros de rate limiting y código `429` |
| — | Longitudes máximas de los campos, retención de datos, cabeceras de seguridad, herramientas de detección de secretos y de dependencias de Next.js |
