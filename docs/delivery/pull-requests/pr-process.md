# Proceso de Pull Requests, CI y revisión adversarial

> **Prompt de origen:** §7, Prompt 1 — Gestión de Pull Requests, CI y revisión adversarial, en [`prompts.md`](../../../prompts.md).
> **Fuente de decisiones aprobadas:** [`README.md`](../../../README.md) §7; guardrails en [`sdd-harness.md`](../../ai/sdd-harness.md#7-catálogo-de-guardrails).
> **Estado del documento:** **diseño de proceso.** No existe ningún workflow de GitHub Actions, protección de rama, bot ni agente revisor configurado. Ningún control de este documento se ha ejecutado en CI.

## 1. Plantilla de descripción de Pull Request

Se completa solo con información real del cambio; lo que no se haya ejecutado se declara como tal.

```markdown
## Objetivo y referencia
- Historia: [HU-00x]
- Ticket: [TICKET-00x]
- Requisitos y escenarios de spec: [HU-00x-Rxx, HU-00x-Sxx]

## Cambios incluidos
- [Archivos o comportamientos modificados, sin afirmar lo no implementado]

## Especificaciones afectadas
- [Specs o contratos modificados, con aprobación humana si corresponde (HAP-01/HAP-03)]

## Evidencia TDD
- RED: [prueba y salida real del fallo esperado]
- GREEN: [salida real de la suite]
- REFACTOR: [cambios y suite en verde]

## Verificaciones
- [Comandos realmente ejecutados y resultados]
- [Verificaciones manuales realizadas]
- [Controles no aplicables o no configurados, con motivo]

## Impacto y riesgos
- [Áreas afectadas, compatibilidad, datos, seguridad]

## Revisión adversarial
- [Enlace al informe; hallazgos y resolución]

## Checklist
- [ ] Cambios dentro del alcance y del contrato aprobados
- [ ] Pruebas y controles aplicables con evidencia
- [ ] Ninguna prueba modificada por el agente implementador sin HAP-02
- [ ] Revisión de seguridad y de datos sensibles
- [ ] Hallazgos adversariales resueltos o justificados
- [ ] Revisión humana completada
```

## 2. Controles CI previstos y condiciones de bloqueo

**Plataforma prevista:** GitHub Actions (Prompt §7). Ningún workflow existe ni se crea en esta ejecución.

| Control | Guardrail | Se activa cuando cambia | Condición de bloqueo | Estado |
|---|---|---|---|---|
| Lint, typecheck y compilación de Next.js | GR-08 | `frontend/` | Falla cualquiera de los tres | Propuesto |
| Lint y compilación de Go | GR-08 | `backend/` | Falla la compilación o el lint | Propuesto |
| Pruebas unitarias de Go y del frontend | GR-03 | `frontend/`, `backend/` | Alguna prueba falla | Propuesto |
| Integración con PostgreSQL aislado | GR-03, GR-07 | `backend/`, `database/` | Falla una prueba o una migración | Propuesto |
| Cobertura de servicios de negocio | GR-04 | `backend/internal/services/` | Menos del 80 % | Meta aprobada; control no configurado |
| Lint y comparación del contrato OpenAPI | GR-05 | `docs/api/`, `backend/` | YAML inválido o rutas implementadas distintas del contrato | Propuesto; comparador por diseñar |
| Validación de specs | GR-01 | `openspec/` (si se adopta) | Spec inválida o sin aprobación | Condicionado a la adopción de OpenSpec |
| `govulncheck` | GR-09 | `backend/`, `go.mod` | Vulnerabilidad sin tratar | Propuesto |
| Detección de secretos | GR-10 | Todo | Credencial detectada | Propuesto; herramienta no seleccionada |
| Calidad documental | GR-13 | `docs/`, `README.md`, `prompts.md` | Mermaid inválido, enlace roto o YAML inválido | Propuesto |

**Reglas de bloqueo:**
1. Solo bloquean los checks obligatorios **definidos y comprobados**.
2. Un check no configurado **no se presenta como aprobado ni superado**.
3. Un fallo de un check obligatorio impide el merge hasta corregirlo. Saltarse un check requiere una decisión humana registrada en el PR.

## 3. Revisión adversarial

| Aspecto | Definición |
|---|---|
| Ejecutor | Subagente independiente, distinto de los que escribieron las pruebas y la implementación |
| Permisos | **Solo lectura**; no modifica código, pruebas ni specs; no aprueba |
| Entradas | Diff del PR, specs y escenarios citados, `openapi.yaml`, `data-model.md` y resultados de CI |
| Busca | Incumplimientos de la spec; casos límite sin probar; problemas de seguridad (autorización, validación, datos personales); supuestos incorrectos; pruebas debilitadas; cambios fuera de alcance |
| Salida | Informe con un hallazgo por entrada: archivo, línea, escenario afectado, evidencia y severidad |
| Severidad (propuesta) | **Bloqueante** (rompe la spec, la seguridad o la integridad), **Mayor** (caso límite relevante sin cubrir), **Menor** (mejora) |
| Límite | No sustituye las pruebas ni la aprobación humana |

**Registro de hallazgos (propuesto):**

| ID | Severidad | Archivo:línea | Escenario | Descripción | Resolución | Decisión humana |
|---|---|---|---|---|---|---|
| ADV-01 | … | … | … | … | Corregido / Justificado / Diferido | Aprobado por … |

Las severidades y su efecto de bloqueo son una **propuesta** pendiente de aprobación.

## 4. Aprobación humana

| Situación | Aprobación requerida |
|---|---|
| Todo PR | Revisión y aprobación del responsable antes del merge (GR-12, HAP-05) |
| Cambios de spec o de contrato | HAP-01 / HAP-03 antes de implementar |
| Cambios de pruebas existentes | HAP-02 |
| Hallazgos bloqueantes justificados sin corregir | Decisión explícita registrada en el PR |
| Migraciones destructivas o despliegues | HAP-06 |

Ningún agente aprueba sus propios cambios.

## 5. Checklist de aprobación y cierre

- [ ] El PR cita historia, ticket y requisitos reales.
- [ ] Hay evidencia RED → GREEN → REFACTOR de cada regla nueva.
- [ ] Los checks obligatorios configurados están en verde; los no configurados se declaran.
- [ ] El contrato y el esquema coinciden con lo aprobado (3 endpoints, 15 tablas).
- [ ] No hay secretos ni datos personales reales.
- [ ] Los hallazgos adversariales están resueltos o justificados.
- [ ] El responsable humano aprueba.
- [ ] Tras el merge, la documentación afectada se actualiza en el mismo PR o en uno vinculado.

## 6. Verificaciones según el tipo de PR

| Verificación | PR001 (documental) | PR con código |
|---|---|---|
| Enlaces, estructura Markdown, Mermaid y YAML | Sí | Si cambian documentos |
| Coherencia README ↔ prompts ↔ `docs/` | Sí | Si cambian documentos |
| Estados "aprobado", "previsto" y "ejecutado" no confundidos | Sí | Sí |
| Lint, compilación y pruebas | **No aplica**: no hay código | Sí |
| Cobertura, `govulncheck` | No aplica | Sí |
| Revisión adversarial | Opcional, sobre la coherencia documental | Obligatoria |
| Aprobación humana | Sí | Sí |

Para PR001 no se inventa evidencia de pruebas de aplicación ni de CI. Ver [`PR-001.md`](PR-001.md).
