# ADR-D03 — Infraestructura Docker + Coolify en VPS KVM 4 propio

| Campo | Valor |
|---|---|
| Estado | Aprobada; **no desplegada** |
| Fecha de la decisión | No registrada |
| Fecha de este registro | 2026-10-19 (ejecución documental de la entrega 1) |
| Fuente | [`README.md`](../../../README.md) §2.4 |

## Contexto y problema

El proyecto necesita ejecutar frontend, backend y PostgreSQL con costos y operación controlados, sin depender de servicios cloud gestionados.

## Decisión

- Servidor **VPS KVM 4**: 4 vCPU, 16 GB de RAM, 200 GB NVMe y 16 TB de transferencia.
- **Coolify** para administrar aplicaciones y contenedores.
- **Docker** para aislar y ejecutar frontend, backend y PostgreSQL.
- Código fuente en GitHub (monorepo, [ADR-D04](ADR-D04-monorepo.md)).

## Alternativas consideradas

No documentadas en el registro aprobado. El README precisa: "No se afirma haber realizado pruebas comparativas de proveedores".

## Consecuencias positivas

- Costos y operación centralizados en un único servidor.
- Despliegue independiente de frontend y backend.
- Variables de entorno gestionadas en Coolify, sin credenciales en Git.

## Consecuencias negativas

- Punto único de falla para interfaz, API y base de datos.
- La responsabilidad de backups, actualizaciones y recuperación recae en el equipo.

## Riesgos y limitaciones

| Riesgo | Mitigación prevista | Estado |
|---|---|---|
| Caída del host | Health checks y procedimiento de recuperación | Propuesto; RTO/RPO pendientes (A8) |
| Pérdida de datos | Backups restaurables fuera del VPS principal | Requisito aprobado; mecanismo, proveedor, frecuencia, retención y recuperación pendientes (A8, A15) |
| Competencia por recursos | Métricas y pruebas de carga | Propuesto |
| Despliegue defectuoso | Versionado de imágenes y rollback probado | Propuesto; procedimiento pendiente (A8) |

## Decisiones relacionadas pendientes

A8 (frecuencia y retención de backups, RTO/RPO, rollback, dominios y ambientes) y A15 (mecanismo y proveedor del almacenamiento externo; el requisito de backups fuera del VPS principal está aprobado). Detalle en [`deployment.md`](../deployment.md).
