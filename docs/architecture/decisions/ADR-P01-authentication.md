# ADR-P01 — Mecanismo de autenticación

| Campo | Valor |
|---|---|
| Estado | **Pendiente**: no se ha seleccionado mecanismo |
| Fecha de este registro | 2026-10-19 (ejecución documental de la entrega 1) |
| Fuente | [`README.md`](../../../README.md) §1.2 (riesgos), §2.1 y §2.5; §4 (`BearerAuth` provisional) |

## Contexto y problema

Existen dos perfiles autenticados con accesos distintos:

- `TOURIST`: guarda y recupera sus propios recorridos (F07).
- `ADMIN`: consulta y resuelve solicitudes (F05).

El registro público asigna `TOURIST`; las cuentas `ADMIN` se crean solo mediante un procedimiento autorizado (README §2.5). El modelo de datos incluye `users.password_hash`.

El mecanismo elegido condicionará las sesiones, el uso de tokens o cookies, la protección CSRF, el manejo de expiración y cierre de sesión, y las pruebas de 401/403.

## Decisión

**Ninguna todavía.** No se selecciona JWT, cookie ni proveedor (README §2.1). El esquema `BearerAuth` del contrato OpenAPI es provisional y **no equivale a adoptar JWT** (README §4).

## Alternativas a evaluar

Las alternativas se analizan por primera vez en esta ejecución, a petición del Prompt §2.5, en [`security.md`](../security.md#4-evaluación-de-mecanismos-de-autenticación). No son alternativas evaluadas en el pasado.

## Consecuencias de mantenerla pendiente

- F05 y F07 no pueden implementarse por completo.
- El `PATCH` administrativo se documenta con un esquema de seguridad provisional.
- Las pruebas de autorización (401/403) pueden especificarse, pero no ejecutarse contra un mecanismo real.

## Criterios para cerrar este ADR

1. Evaluación de alternativas aprobada por el responsable del proyecto.
2. Definición del procedimiento de alta de cuentas `ADMIN`.
3. Actualización del esquema de seguridad en OpenAPI y de la protección CSRF y CORS, si corresponde.
4. Algoritmo de hash de contraseñas seleccionado, si se usan contraseñas locales.
