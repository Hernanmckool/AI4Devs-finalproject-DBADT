# Prompts — Descubre Barquisimeto — Agencia Digital de Turismo

## 1. Descripción general del producto

### Prompt 1 — Definición estratégica del producto (Product Discovery)

```text
# Rol y experiencia

Actúa como un Product Owner Senior y Product Discovery Lead,
especializado en plataformas digitales de turismo y experiencias
de viaje en Latinoamérica.

Tienes experiencia en la definición de productos digitales desde
cero, investigación de necesidades de usuarios, identificación
de oportunidades de negocio y construcción de MVP.

Tu responsabilidad es ayudarme a transformar una idea de negocio
en una definición de producto clara, viable y preparada para
su posterior diseño y desarrollo.

Actuarás como mi asesor. Las decisiones finales sobre el alcance,
las funcionalidades y las prioridades serán tomadas por mí.

# Objetivo

Definir la visión, propuesta de valor, público objetivo y alcance
funcional inicial de "Descubre Barquisimeto — Agencia Digital de
Turismo".

El resultado debe servir como documento base para las siguientes
fases: arquitectura de software, modelo de datos, diseño de API,
historias de usuario y planificación del desarrollo.

# Contexto del negocio

Barquisimeto, capital del estado Lara, Venezuela, cuenta con
atractivos culturales, históricos, gastronómicos y naturales
que pueden formar parte de diferentes experiencias turísticas.

Quiero crear una agencia digital de turismo que permita
centralizar en una sola plataforma la información que necesita
un visitante para conocer la ciudad y planificar su estadía.

La propuesta contempla:

- Descubrimiento de atractivos turísticos y lugares emblemáticos.
- Información sobre hoteles, posadas y alternativas de alojamiento.
- Tours, recorridos y experiencias guiadas.
- Solicitudes de reserva de alojamientos y tours.
- Ubicación geográfica de lugares de interés.
- Herramientas para organizar recorridos personalizados.

La plataforma estará orientada a turistas nacionales e
internacionales y deberá ofrecer una experiencia moderna,
intuitiva y adaptable a dispositivos móviles.

También deberá contemplar las necesidades operativas del
personal de la agencia que administrará la información
turística y gestionará las solicitudes recibidas.

# Método de análisis

Antes de proponer el alcance definitivo:

1. Identifica los problemas que enfrentan los visitantes al
   descubrir y organizar actividades turísticas en Barquisimeto.

2. Diferencia las necesidades del turista de las necesidades
   operativas de la agencia.

3. Identifica los principales perfiles de usuario y los
   objetivos que cada uno intenta cumplir.

4. Describe los recorridos de usuario más importantes, desde
   el descubrimiento de un atractivo hasta la solicitud de
   una reserva o la planificación de una visita.

5. Propón las capacidades necesarias para satisfacer esos
   recorridos, justificando el valor que aporta cada una.

6. Identifica las decisiones que pueden aumentar la
   complejidad del MVP y que requieren validación humana.

# Entregables esperados

Presenta una definición de producto que incluya:

1. Visión del producto y problema que busca resolver.
2. Objetivos de negocio y propuesta de valor diferencial.
3. Público objetivo y perfiles principales de usuario.
4. Funcionalidades propuestas, agrupadas por capacidades.
5. Flujos funcionales principales del turista y la agencia.
6. Propuesta preliminar de priorización para el MVP.
7. Funcionalidades que podrían incorporarse en fases futuras.
8. Riesgos, dependencias, supuestos y preguntas abiertas.

Utiliza tablas cuando permitan comparar funcionalidades,
prioridades o perfiles de usuario.

# Restricciones y criterios de decisión

- No asumas que todas las funcionalidades propuestas deben
  formar parte del MVP.
- No definas tecnologías ni arquitectura de software en
  esta etapa.
- No incorpores pagos, integraciones externas o procesos
  operativos complejos sin consultar previamente.
- No inventes estadísticas del mercado turístico ni
  métricas de negocio.
- Distingue los requisitos confirmados de las
  recomendaciones pendientes de aprobación.
- No tomes decisiones de producto en mi nombre.
- Presenta alternativas con sus ventajas y limitaciones
  cuando existan decisiones relevantes.

# Validación de calidad

Antes de entregar, verifica:

- ¿Cada funcionalidad responde a una necesidad identificada?
- ¿Están representados los turistas y el personal de la agencia?
- ¿Los flujos principales tienen un principio y un resultado claro?
- ¿Las recomendaciones se distinguen de las decisiones aprobadas?
- ¿Existen funcionalidades propuestas que aumenten
  innecesariamente la complejidad del MVP?
- ¿Quedaron identificadas las decisiones pendientes?

# Formato de respuesta

Documento Markdown estructurado, con un nivel de detalle
suficiente para iniciar la definición funcional del producto.

Presenta primero el análisis y las recomendaciones.

No avances a la arquitectura ni a la implementación.
Espera mi aprobación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §1.1 y §1.2: objetivos, perfiles, siete capacidades y pendientes de alcance.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### Prompt 2 — Delimitación del MVP y definición de flujos de negocio

```text
# Rol

Actúa como Business Analyst Senior, especializado en el
levantamiento de requisitos y la definición funcional de
plataformas digitales de turismo.

Tu responsabilidad será analizar la propuesta de producto
previamente definida, identificar ambigüedades y ayudarme
a establecer un alcance funcional que pueda implementarse
de manera incremental.

Trabajarás como asesor técnico-funcional. Toda modificación
del alcance deberá contar con mi aprobación.

# Contexto

Estamos desarrollando "Descubre Barquisimeto — Agencia
Digital de Turismo", una plataforma destinada a facilitar
el descubrimiento y la planificación de experiencias
turísticas en Barquisimeto, Venezuela.

Durante la definición inicial identificamos siete
capacidades principales:

F01. Exploración de atractivos turísticos.
F02. Consulta de hoteles, posadas y alojamientos.
F03. Exploración de tours y visitas guiadas.
F04. Solicitudes de reserva de alojamientos y tours.
F05. Gestión administrativa de solicitudes de reserva.
F06. Visualización de lugares mediante mapas.
F07. Planificación de recorridos turísticos personalizados.

Estas capacidades constituyen la base funcional del
producto y deben mantenerse como referencia.

# Trabajo solicitado

Necesito que analices los flujos de negocio asociados
a estas capacidades antes de avanzar a la arquitectura.

Para ello:

1. Identifica los actores involucrados y sus
   responsabilidades dentro de la plataforma.

2. Describe el recorrido de un visitante que descubre
   un atractivo turístico, explora opciones disponibles
   y decide solicitar una reserva.

3. Define el flujo administrativo para recibir,
   revisar y gestionar solicitudes de reserva.

4. Analiza cómo un turista podría organizar un recorrido
   personalizado y qué implicaciones tendría guardar
   esa planificación para consultarla posteriormente.

5. Identifica las validaciones, dependencias y situaciones
   excepcionales que debemos contemplar.

6. Señala cuáles de estas capacidades requieren
   decisiones funcionales adicionales antes de
   comenzar el desarrollo.

# Límites del producto

Ten en cuenta las siguientes condiciones:

- Las reservas se gestionarán como solicitudes.
- No habrá cobros ni pasarelas de pago en esta etapa.
- El envío de una solicitud no garantiza disponibilidad.
- Los visitantes podrán explorar información turística
  sin autenticarse.
- La plataforma contará con un área administrativa
  para gestionar solicitudes.
- No propongas integraciones con operadores turísticos
  ni proveedores externos como requisitos obligatorios.
- No incorpores funcionalidades adicionales sin
  presentarlas previamente para aprobación.

# Resultado esperado

Presenta un documento funcional que contenga:

- Actores y responsabilidades.
- Flujos de negocio principales.
- Reglas y validaciones por flujo.
- Casos alternativos y excepciones.
- Dependencias entre funcionalidades.
- Decisiones que requieren aprobación.

Para cada regla funcional, identifica si se encuentra
confirmada o si es una propuesta pendiente.

Evita diseñar tablas, endpoints o componentes técnicos:
esas definiciones corresponderán a fases posteriores.

Finaliza con las preguntas pendientes de negocio y
espera mis indicaciones antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §1.2 y §1.3: dependencias, límites y recorridos con excepciones.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### Prompt 3 — Diseño de experiencia de usuario (UX)

```text
# Perfil profesional

Asume el rol de UX Product Designer Senior, especializado
en plataformas de turismo, planificación de viajes y
experiencias digitales orientadas al consumidor.

Tu responsabilidad será ayudarme a definir cómo los usuarios
interactuarán con Descubre Barquisimeto, tomando como base
los requisitos funcionales previamente aprobados.

Trabajarás como asesor de UX/UI. Las propuestas de diseño,
navegación e interacción deberán ser validadas por mí antes
de considerarse definitivas.

# Punto de partida

Descubre Barquisimeto es una agencia digital de turismo
enfocada en Barquisimeto, estado Lara, Venezuela.

La plataforma contempla siete funcionalidades:

F01. Exploración de atractivos turísticos.
F02. Consulta de alojamientos.
F03. Exploración de tours y visitas guiadas.
F04. Solicitudes de reserva.
F05. Gestión administrativa de solicitudes.
F06. Visualización de lugares en mapas.
F07. Planificación de recorridos personalizados.

El producto estará disponible a través de una aplicación
web responsive, orientada a turistas nacionales e
internacionales y al personal administrativo de la agencia.

# Experiencia que buscamos construir

Quiero que la experiencia sea visual, intuitiva y sencilla
de utilizar, especialmente desde dispositivos móviles.

Un visitante debe poder descubrir un lugar de interés,
consultar sus fotografías, comprender dónde se encuentra
y explorar las actividades relacionadas sin enfrentarse
a una navegación compleja.

También debe resultar sencillo consultar alojamientos,
explorar tours y enviar solicitudes de reserva.

Los turistas registrados podrán guardar y recuperar
sus recorridos personalizados.

El personal administrativo necesitará una experiencia
orientada a consultar y gestionar solicitudes recibidas.

# Actividades solicitadas

1. Identifica las principales necesidades de usabilidad
   de turistas y administradores.

2. Propón una organización de la información que permita
   descubrir atractivos, alojamientos y tours.

3. Describe los recorridos de navegación necesarios para
   explorar el catálogo turístico y consultar los detalles
   de cada elemento.

4. Define cómo debería presentarse la información
   geográfica y la interacción con mapas.

5. Analiza la experiencia de envío de una solicitud
   de reserva, incluyendo validaciones y mensajes
   de confirmación o error.

6. Describe la interacción del planificador de recorridos
   personalizados y su relación con la cuenta del turista.

7. Identifica los componentes visuales reutilizables
   que podrían facilitar una experiencia consistente.

8. Propón criterios para adaptar la interfaz a teléfonos,
   tablets y computadoras.

# Condiciones del diseño

- Prioriza la simplicidad y la claridad visual.
- No modifiques las reglas de negocio aprobadas.
- No incorpores pagos ni reservas confirmadas en tiempo real.
- La exploración del catálogo no debe exigir autenticación.
- No agregues funcionalidades por considerarlas habituales
  en otras plataformas turísticas.
- Contempla estados de carga, ausencia de resultados
  y errores de comunicación.
- Considera accesibilidad, legibilidad y navegación
  mediante teclado.
- No selecciones bibliotecas de componentes ni herramientas
  de diseño sin consultarme.

# Resultado solicitado

Presenta una propuesta funcional de experiencia de usuario
que contemple:

- Organización general de la navegación.
- Pantallas o vistas principales sugeridas.
- Recorridos de usuario más importantes.
- Componentes de interfaz reutilizables.
- Comportamiento responsive.
- Estados de interacción y mensajes al usuario.
- Recomendaciones de accesibilidad.
- Aspectos que necesitan validación de producto.

Cuando existan alternativas de diseño, presenta sus
ventajas y limitaciones.

No generes código ni implementes componentes.

El objetivo es definir una experiencia de usuario
coherente con el producto aprobado.

Espera mi aprobación antes de avanzar.

# Correspondencia documental
Ubica el resultado en README.md §1.3: vistas, recorridos, estados de interfaz y accesibilidad.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

## 2. Arquitectura del Sistema

### 2.1. Diagrama de arquitectura

**Prompt 1 — Diseño de arquitectura del sistema**

```text
# Rol
Actúa como Arquitecto de Software Senior especializado
en aplicaciones web full-stack, APIs REST y arquitectura
por capas.

# Objetivo
Diseñar y justificar la arquitectura técnica de
"Descubre Barquisimeto — Agencia Digital de Turismo",
partiendo de los requisitos funcionales ya definidos.

# Contexto tecnológico
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Arquitectura: Controller → Service → Repository.
- Base de datos: PostgreSQL.
- Infraestructura: Docker + Coolify en VPS propio.
- Organización: monorepo.

# Trabajo solicitado
1. Relaciona las funcionalidades F01-F07 con los
   componentes responsables de implementarlas.
2. Describe la comunicación frontend, API y base de datos.
3. Representa los flujos de consulta turística,
   solicitud de reserva y gestión administrativa.
4. Justifica la arquitectura seleccionada, indicando
   ventajas, limitaciones y riesgos técnicos.
5. Identifica decisiones pendientes sin resolverlas
   automáticamente.

# Entregables
- Diagrama de arquitectura en Mermaid.
- Diagrama de secuencia de solicitud de reserva.
- Explicación de componentes y comunicaciones.
- Justificación técnica de la arquitectura.
- Riesgos y decisiones pendientes.

# Restricciones
- Respeta las tecnologías y decisiones aprobadas.
- No incorpores microservicios ni servicios adicionales.
- No incluyas pagos ni disponibilidad en tiempo real.
- No presentes componentes planificados como implementados.
- No generes código.

Actúa como asesor técnico. Presenta la propuesta y
espera mi aprobación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §2.1: diagrama, secuencia, explicación y riesgos.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

**Prompt 2 — Evaluación y registro de decisiones arquitectónicas (ADR)**

```text
# Rol
Actúa como Arquitecto de Software Senior especializado
en evaluación de arquitecturas y documentación de
decisiones técnicas mediante Architecture Decision
Records (ADR).

# Objetivo
Analizar las decisiones arquitectónicas de
"Descubre Barquisimeto" y documentar sus fundamentos,
ventajas, limitaciones y consecuencias.

# Contexto
La arquitectura definida contempla:
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Patrón: arquitectura por capas.
- Base de datos: PostgreSQL.
- Infraestructura: Docker + Coolify en VPS propio.
- Organización: monorepo.

# Trabajo solicitado
1. Identifica las decisiones arquitectónicas
   más relevantes para el proyecto.
2. Justifica cada decisión según los requisitos
   funcionales, mantenibilidad y complejidad.
3. Evalúa las ventajas y desventajas de las
   tecnologías y patrones seleccionados.
4. Identifica riesgos técnicos y posibles
   consecuencias a futuro.
5. Señala decisiones pendientes que requieran
   mi aprobación antes de implementarse.

# Entregables
Documenta las decisiones relevantes mediante ADR,
incluyendo:
- Contexto y problema.
- Decisión adoptada.
- Alternativas consideradas.
- Consecuencias positivas y negativas.
- Riesgos y limitaciones.

# Restricciones
- No modifiques las tecnologías aprobadas.
- No inventes decisiones ni alternativas evaluadas.
- No introduzcas componentes adicionales.
- Distingue decisiones aprobadas de las pendientes.
- No generes código.

Presenta los ADR en Markdown y espera mi aprobación
antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §2.1: fichas ADR documentales; no simular archivos/versiones de ADR inexistentes.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### 2.2. Descripción de componentes

**Prompt 1 — Definición de componentes y responsabilidades**

```text
# Rol
Actúa como Arquitecto de Software Senior especializado
en diseño modular, aplicaciones full-stack y
separación de responsabilidades.

# Objetivo
Documentar los componentes de la arquitectura de
"Descubre Barquisimeto", estableciendo sus funciones,
dependencias y mecanismos de comunicación.

# Contexto
La arquitectura aprobada utiliza:
- Next.js + TypeScript para el frontend.
- Go + Chi v5 para el backend.
- Patrón Controller → Service → Repository.
- PostgreSQL como base de datos.
- Docker + Coolify para el despliegue.

El sistema contempla exploración turística,
alojamientos, tours, solicitudes de reserva,
gestión administrativa, mapas e itinerarios.

# Trabajo solicitado
1. Identifica los componentes funcionales del frontend
   y sus responsabilidades.
2. Define las responsabilidades de Controllers,
   Services y Repositories en el backend.
3. Relaciona cada componente con las funcionalidades
   F01-F07 del producto.
4. Explica las dependencias y comunicaciones entre
   componentes.
5. Identifica reglas de negocio que deben ejecutarse
   exclusivamente en el backend.

# Entregables
- Tabla de componentes y responsabilidades.
- Matriz de trazabilidad entre componentes y F01-F07.
- Diagrama Mermaid de dependencias.
- Recomendaciones para mantener bajo acoplamiento
  y alta cohesión.

# Restricciones
- Respeta la arquitectura previamente aprobada.
- No agregues tecnologías ni funcionalidades nuevas.
- No dupliques reglas de negocio entre frontend y backend.
- No generes código de implementación.
- Identifica cualquier decisión pendiente de aprobación.

Presenta el resultado en Markdown y espera mi
validación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §2.2: matriz F01–F07, capas y dependencias.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### 2.3. Estructura del proyecto y archivos

**Prompt 1 — Estructura del monorepo y harness de desarrollo con IA**

```text
# Rol
Actúa como Arquitecto de Software Senior especializado
en monorepos, desarrollo asistido por IA y diseño de
harnesses para agentes de programación.

# Objetivo
Definir la estructura del proyecto "Descubre Barquisimeto"
y proponer un harness que permita desarrollar de manera
consistente, reproducible y supervisada.

# Contexto
Stack aprobado:
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Arquitectura: Controller → Service → Repository.
- Base de datos: PostgreSQL.
- Infraestructura: Docker + Coolify.
- Metodología: SDD y TDD (RED → GREEN → REFACTOR).

# Trabajo solicitado
1. Diseña la estructura de directorios del monorepo,
   incluyendo frontend, backend, base de datos,
   documentación y pruebas.

2. Propón la organización de un harness de desarrollo
   que contemple:
   - Reglas persistentes mediante AGENTS.md o CLAUDE.md.
   - Skills reutilizables para tareas de desarrollo.
   - Subagentes especializados en testing,
     implementación y revisión adversarial.
   - Hooks para automatizar verificaciones repetitivas.

3. Define las responsabilidades y límites de cada agente,
   evitando que quien implementa modifique los tests
   para conseguir que pasen.

4. Establece el flujo de trabajo:
   especificación aprobada → tests → implementación
   → validación → revisión humana.

5. Identifica qué reglas deben ser instrucciones
   para los agentes y cuáles requieren controles
   automatizados verificables (guardrails).

# Entregables
- Árbol de directorios del monorepo.
- Estructura propuesta del harness.
- Responsabilidades de agentes y skills.
- Reglas de desarrollo y puntos de aprobación humana.
- Justificación de las decisiones propuestas.

# Restricciones
- No modifiques el stack ni la arquitectura aprobada.
- No introduzcas herramientas adicionales sin aprobación.
- Ningún agente puede aprobar sus propios cambios.
- No ejecutes comandos, crees archivos ni modifiques
  el repositorio durante esta etapa.
- Diferencia los componentes propuestos de los
  efectivamente implementados.

Presenta el diseño en Markdown y espera mi aprobación.

# Correspondencia documental
Ubica el resultado en README.md §2.3: monorepo aprobado y extensión de harness **propuesta**, sin archivos creados.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### 2.4. Infraestructura y despliegue

**Prompt 1 — Diseño de infraestructura y estrategia de despliegue**

```text
# Rol
Actúa como Arquitecto DevOps Senior, especializado
en despliegues de aplicaciones full-stack mediante
Docker, Coolify y servidores VPS autogestionados.

# Objetivo
Diseñar la infraestructura y el proceso de despliegue
de "Descubre Barquisimeto", priorizando seguridad,
mantenibilidad y costos operativos controlados.

# Infraestructura aprobada
- VPS KVM 4: 4 vCPU, 16 GB RAM y 200 GB NVMe.
- Plataforma de despliegue: Coolify.
- Contenedores: Docker.
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Base de datos: PostgreSQL.
- Organización del código: monorepo.

# Trabajo solicitado
1. Define la distribución de frontend, backend y
   PostgreSQL dentro de la infraestructura.
2. Describe el proceso de despliegue desde el
   repositorio hasta el VPS mediante Coolify.
3. Establece cómo gestionar variables de entorno,
   secretos y configuraciones por ambiente.
4. Propón mecanismos de HTTPS, aislamiento de
   PostgreSQL y control de acceso administrativo.
5. Define una estrategia de backups, monitoreo,
   recuperación y rollback.
6. Identifica riesgos operativos y limitaciones
   de utilizar un único VPS.

# Entregables
- Diagrama de despliegue en Mermaid.
- Descripción de la infraestructura.
- Flujo de despliegue y actualización.
- Estrategia de seguridad y recuperación.
- Riesgos y decisiones pendientes.

# Restricciones
- Respeta la infraestructura y tecnologías aprobadas.
- No introduzcas servicios cloud externos.
- No expongas PostgreSQL públicamente.
- No inventes configuraciones que aún no se definieron.
- No generes archivos de configuración ni ejecutes
  despliegues sin autorización.

Entrega la propuesta en Markdown y espera mi
aprobación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §2.4: despliegue previsto, riesgos y decisiones abiertas.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### 2.5. Seguridad

**Prompt 1 — Diseño de seguridad y protección de datos**

```text
# Rol
Actúa como Arquitecto de Seguridad de Software Senior,
especializado en aplicaciones web, APIs REST y protección
de datos personales.

# Objetivo
Definir los requisitos y controles de seguridad de
"Descubre Barquisimeto", considerando su arquitectura,
los perfiles de usuario y los datos que procesará.

# Contexto
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Base de datos: PostgreSQL.
- Infraestructura: Docker + Coolify en VPS propio.
- Usuarios: visitantes, turistas registrados y ADMIN.
- Reservas: solicitudes sin pagos en línea.
- Arquitectura: Controller → Service → Repository.

# Trabajo solicitado
1. Identifica las superficies de ataque y los
   principales riesgos de seguridad.
2. Evalúa las necesidades de autenticación y
   autorización según cada perfil de usuario.
3. Propón controles para proteger los endpoints
   administrativos y los datos personales.
4. Define estrategias de validación de entradas,
   prevención de ataques comunes y manejo seguro
   de errores.
5. Analiza la gestión de secretos, HTTPS, permisos
   de base de datos y seguridad de contenedores.
6. Propón medidas de auditoría, registro de eventos
   y protección frente a abusos de la API.

# Entregables
- Matriz de riesgos y controles de seguridad.
- Matriz de permisos por perfil.
- Recomendaciones de protección de datos.
- Controles de seguridad por componente.
- Decisiones pendientes de aprobación.

# Restricciones
- No selecciones un mecanismo de autenticación
  sin evaluar alternativas y solicitar aprobación.
- No incorpores servicios externos sin autorización.
- No inventes requisitos legales ni certificaciones.
- No generes código ni modifiques la infraestructura.
- Distingue las medidas propuestas de las aprobadas.

Entrega el análisis en Markdown y espera mi aprobación.

# Correspondencia documental
Ubica el resultado en README.md §2.5: controles, matriz de roles, riesgos y medidas propuestas.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

### 2.6. Estrategia de pruebas

**Prompt 1 — Estrategia de testing basada en SDD, TDD y guardrails**

```text
# Rol
Actúa como QA Architect Senior especializado en
Spec-Driven Development (SDD), Test-Driven Development
(TDD), automatización de pruebas y calidad de software
asistido por agentes de IA.

# Objetivo
Diseñar la estrategia de calidad de "Descubre Barquisimeto",
utilizando especificaciones verificables como referencia
para las pruebas y la implementación.

# Contexto
Stack aprobado:
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Base de datos: PostgreSQL.
- Arquitectura: Controller → Service → Repository.

Herramientas previstas:
- Go testing y httptest.
- Vitest y React Testing Library.
- Playwright para pruebas E2E.
- k6 para rendimiento.
- govulncheck para análisis de vulnerabilidades.

# Trabajo solicitado
1. Propón cómo aplicar SDD utilizando OpenSpec,
   convirtiendo los criterios de aceptación de las
   historias HU001-HU003 en requisitos y escenarios
   verificables.

2. Define el proceso TDD:
   RED → GREEN → REFACTOR, asegurando que los tests
   se escriban desde la especificación antes de
   implementar las reglas de negocio.

3. Establece una estrategia de pruebas unitarias,
   integración, contrato y E2E para las
   funcionalidades F01-F07.

4. Define la separación de responsabilidades entre
   agentes de testing, implementación y revisión,
   evitando modificaciones injustificadas de tests
   para conseguir resultados exitosos.

5. Propón guardrails automatizados para verificar:
   - Cumplimiento de las especificaciones aprobadas.
   - Ejecución satisfactoria de pruebas.
   - Consistencia del contrato OpenAPI.
   - Análisis de vulnerabilidades.
   - Cobertura de servicios de negocio.

6. Identifica los escenarios críticos de reservas,
   autorización administrativa, concurrencia y
   transiciones de estado que requieren pruebas.

# Entregables
- Estrategia SDD + TDD.
- Matriz de trazabilidad: requisito → test.
- Pirámide de pruebas y herramientas.
- Guardrails propuestos y condiciones de bloqueo.
- Criterios de calidad para aprobar una entrega.

# Restricciones
- Objetivo mínimo de 80% de cobertura en servicios
  de negocio.
- Ningún agente puede alterar requisitos aprobados.
- No se considera válido un test que nunca demostró
  fallar cuando correspondía.
- Distingue validaciones automáticas de revisiones
  que necesitan intervención humana.
- No afirmes que OpenSpec o los guardrails ya están
  configurados.
- No generes código ni ejecutes herramientas.
- Presenta cualquier incorporación técnica
  para aprobación previa.

Entrega la propuesta en Markdown y espera mi aprobación.

# Correspondencia documental
Ubica el resultado en README.md §2.6: estrategia, trazabilidad y guardrails **propuestos**, sin resultados inventados.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

## 3. Modelo de Datos

**Prompt 1 — Diseño del modelo de datos relacional**

```text
# Rol
Actúa como Arquitecto de Datos Senior y especialista
en PostgreSQL, modelado relacional y diseño de bases
de datos para aplicaciones web.

# Objetivo
Diseñar y documentar el modelo de datos de
"Descubre Barquisimeto", garantizando integridad,
consistencia y trazabilidad con los requisitos
funcionales F01-F07.

# Contexto
La plataforma contempla atractivos turísticos,
categorías, alojamientos, servicios, tours,
solicitudes de reserva y recorridos personalizados.

El modelo aprobado contiene 15 tablas:

- users
- categories
- attractions
- attraction_categories
- attraction_images
- accommodations
- amenities
- accommodation_amenities
- accommodation_images
- tours
- tour_categories
- tour_images
- booking_requests
- travel_plans
- travel_plan_items

# Trabajo solicitado
1. Define los atributos, tipos de datos y claves
   primarias de cada entidad.
2. Establece las relaciones y claves foráneas,
   identificando las cardinalidades.
3. Define restricciones de integridad, unicidad
   y obligatoriedad de campos.
4. Propón índices según los principales patrones
   de consulta del sistema.
5. Analiza la consistencia de las solicitudes
   de reserva y los recorridos personalizados.
6. Identifica decisiones de modelado pendientes
   que requieran validación.

# Entregables
- Diagrama entidad-relación en Mermaid.
- Diccionario de datos.
- Tabla de relaciones y cardinalidades.
- Restricciones e índices recomendados.
- Estrategia de migraciones y evolución del esquema.

# Restricciones
- Utiliza PostgreSQL.
- Mantén las 15 tablas del alcance aprobado.
- No agregues entidades ni relaciones sin aprobación.
- No incorpores pagos ni disponibilidad en tiempo real.
- No generes migraciones SQL todavía.
- Distingue las decisiones aprobadas de las propuestas.

Entrega el diseño en Markdown y espera mi aprobación.

# Correspondencia documental
Ubica el resultado en README.md §3: 15 entidades, DER, diccionario, restricciones y migraciones previstas.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

## 4. Especificación de la API

**Prompt 1 — Diseño y documentación del contrato REST API**

```text
# Rol
Actúa como API Architect Senior, especializado en
diseño de APIs REST, OpenAPI y desarrollo backend
con Go y Chi v5.

# Objetivo
Definir el contrato de la API de "Descubre Barquisimeto",
garantizando consistencia, seguridad y alineación
con los requisitos funcionales aprobados.

# Contexto
- Backend: Go + Chi v5.
- Base de datos: PostgreSQL.
- Arquitectura: Controller → Service → Repository.
- Formato de intercambio: JSON.
- Especificación: OpenAPI 3.0.3.

El alcance contempla tres endpoints:

1. GET /api/v1/attractions
   Consulta pública de atractivos turísticos,
   con filtros y paginación.

2. POST /api/v1/booking-requests
   Creación pública de solicitudes de reserva
   para alojamientos o tours.
   Estado inicial: PENDING.

3. PATCH /api/v1/booking-requests/{id}/status
   Actualización administrativa de solicitudes.
   Transiciones permitidas:
   PENDING → CONFIRMED o REJECTED.

# Trabajo solicitado
1. Define parámetros, cuerpos de solicitud
   y estructuras de respuesta.
2. Establece validaciones y códigos HTTP.
3. Documenta casos exitosos y escenarios de error.
4. Define criterios de paginación y filtrado.
5. Especifica las restricciones de autorización
   de las operaciones administrativas.
6. Contempla concurrencia y actualización atómica
   de los estados de reserva.

# Entregables
- Contrato OpenAPI 3.0.3 en YAML.
- Ejemplos JSON de solicitudes y respuestas.
- Tabla de endpoints, parámetros y códigos HTTP.
- Reglas de validación y manejo de errores.

# Restricciones
- Mantén exclusivamente los tres endpoints aprobados.
- No agregues funcionalidades ni rutas adicionales.
- No selecciones el mecanismo de autenticación
  sin aprobación.
- No incluyas pagos ni disponibilidad en tiempo real.
- No generes código de implementación.
- Identifica las decisiones pendientes.

Presenta la especificación para revisión y espera
mi aprobación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §4: exactamente tres operaciones, tabla y YAML OpenAPI 3.0.3.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

## 5. Historias de Usuario

**Prompt 1 — Definición de historias de usuario**

```text
# Rol
Actúa como Product Owner Senior y Business Analyst,
especializado en metodologías ágiles, definición de
historias de usuario y criterios de aceptación.

# Objetivo
Transformar los requisitos funcionales de
"Descubre Barquisimeto — Agencia Digital de Turismo"
en historias de usuario claras, verificables y
preparadas para su implementación.

# Contexto
El producto contempla siete funcionalidades F01-F07
y tres perfiles principales: visitantes, turistas
registrados y administradores.

Para esta etapa se han definido tres historias:

HU001 — Exploración de atractivos turísticos.
HU002 — Creación de solicitudes de reserva.
HU003 — Gestión administrativa de solicitudes.

Las reservas son solicitudes, no compras.
No existen pagos en línea ni confirmación automática
de disponibilidad.

# Trabajo solicitado
1. Redacta cada historia utilizando el formato:
   "Como [rol], quiero [necesidad], para [beneficio]".
2. Describe su objetivo y valor para el usuario.
3. Define criterios de aceptación mediante
   escenarios Given / When / Then (Gherkin).
4. Identifica reglas de negocio, validaciones
   y comportamientos ante errores.
5. Establece dependencias funcionales y
   condiciones necesarias para su implementación.
6. Relaciona cada historia con las funcionalidades
   del producto que corresponda.

# Entregables
Para cada historia incluye:
- Identificador y título.
- Descripción de la historia.
- Valor de negocio.
- Criterios de aceptación.
- Reglas funcionales.
- Dependencias y consideraciones.

# Restricciones
- Trabaja exclusivamente con HU001, HU002 y HU003.
- No incorpores nuevas funcionalidades.
- HU002 debe permitir solicitudes sin autenticación.
- HU003 debe restringirse a administradores.
- Respeta las transiciones PENDING → CONFIRMED
  o REJECTED.
- No generes código ni tareas técnicas.
- Identifica cualquier ambigüedad para mi aprobación.

Entrega las historias en Markdown y espera
mi validación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §5: HU001–HU003 y criterios verificables.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

**Prompt 2 — Validación de historias de usuario y criterios de aceptación**

```text
# Rol
Actúa como Product Owner Senior y QA Analyst,
especializado en validación de requisitos,
criterios de aceptación y trazabilidad funcional.

# Objetivo
Auditar las historias de usuario de
"Descubre Barquisimeto" para garantizar que sean
claras, completas, consistentes y verificables
antes de iniciar el desarrollo.

# Contexto
Se han definido tres historias de usuario:

- HU001: Exploración de atractivos turísticos.
- HU002: Creación de solicitudes de reserva.
- HU003: Gestión administrativa de solicitudes.

También contamos con los requisitos F01-F07,
el modelo de datos y el contrato REST API aprobados.

# Trabajo solicitado
1. Revisa la claridad y completitud de cada historia.
2. Verifica que los criterios de aceptación sean
   medibles y puedan convertirse en pruebas.
3. Identifica escenarios alternativos, errores
   y casos límite no contemplados.
4. Comprueba la coherencia entre las historias,
   las reglas de negocio y los endpoints aprobados.
5. Construye una matriz de trazabilidad entre
   historias, funcionalidades y API.
6. Identifica ambigüedades o contradicciones
   que requieran decisiones del Product Owner.

# Validaciones obligatorias
- HU001 debe contemplar filtros y paginación.
- HU002 permite solicitudes públicas sin registro.
- Toda solicitud nueva comienza en PENDING.
- HU003 requiere autorización administrativa.
- Las únicas transiciones válidas son
  PENDING → CONFIRMED o PENDING → REJECTED.
- No existen pagos ni validación de disponibilidad
  en tiempo real.

# Entregables
- Evaluación de calidad de HU001, HU002 y HU003.
- Criterios de aceptación ajustados en Gherkin.
- Matriz de trazabilidad funcional.
- Casos límite y escenarios faltantes.
- Lista de observaciones pendientes de aprobación.

# Restricciones
- No crees nuevas historias de usuario.
- No modifiques requisitos aprobados.
- No inventes endpoints ni reglas de negocio.
- Presenta las mejoras como propuestas.
- No generes código ni tickets de desarrollo.

Entrega el análisis en Markdown y espera
mi aprobación antes de continuar.

# Correspondencia documental
Ubica el resultado en README.md §5: Gherkin, trazabilidad y brechas sin rutas inventadas.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

## 6. Tickets de Trabajo

**Prompt 1 — Generación de tickets técnicos bajo metodología SDD y TDD**

```text
# Rol
Actúa como Tech Lead Senior especializado en
desarrollo asistido por IA, Spec-Driven Development
(SDD), Test-Driven Development (TDD) y planificación ágil.

# Objetivo
Transformar las historias de usuario aprobadas de
"Descubre Barquisimeto" en tickets técnicos ejecutables,
estableciendo un proceso de desarrollo guiado por
especificaciones, pruebas y validaciones automatizadas.

# Contexto
Stack tecnológico:
- Frontend: Next.js + TypeScript.
- Backend: Go + Chi v5.
- Base de datos: PostgreSQL.
- Arquitectura: Controller → Service → Repository.

Historias aprobadas: HU001, HU002 y HU003.
Contrato API y modelo relacional previamente definidos.

# Tickets a elaborar
1. Frontend: catálogo de atractivos turísticos,
   filtros, paginación y estados de interfaz.
2. Backend: endpoint público para registrar
   solicitudes de reserva de alojamientos y tours.
3. Base de datos: esquema PostgreSQL con
   las 15 tablas aprobadas.

# Trabajo solicitado
1. Documenta el objetivo, alcance, dependencias
   y criterios de aceptación de cada ticket.

2. Relaciona cada ticket con los requisitos y
   escenarios de su especificación OpenSpec.

3. Divide la implementación en tareas verificables
   respetando el ciclo:
   Spec aprobada → Tests (RED) → Implementación (GREEN)
   → Refactor → Verificación.

4. Define las responsabilidades de los agentes
   encargados de escribir tests, implementar código
   y revisar los resultados.

5. Establece los guardrails de cada ticket:
   - Cumplimiento de la especificación.
   - Tests automatizados satisfactorios.
   - Consistencia de contratos y migraciones.
   - Ausencia de modificaciones no autorizadas.
   - Revisión humana antes de cerrar el trabajo.

6. Incluye escenarios alternativos, casos límite,
   riesgos, estimación y definición de terminado.

# Entregables
- Tres tickets técnicos detallados en Markdown.
- Trazabilidad historia → spec → ticket → tests.
- Secuencia de implementación y validación.
- Criterios verificables de finalización.

# Restricciones
- No incorpores funcionalidades adicionales.
- No modifiques requisitos ni specs aprobadas.
- Los agentes no pueden alterar los tests para
  ocultar fallos de implementación.
- No ejecutes código ni crees archivos.
- No asumas que el harness o OpenSpec están
  configurados o ejecutándose.
- Toda decisión pendiente requiere mi aprobación.

Entrega los tickets y espera mi validación.

# Correspondencia documental
Ubica el resultado en README.md §6: tres tickets, secuencia SDD/TDD y definición de terminado.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```

## 7. Pull Requests

**Prompt 1 — Gestión de Pull Requests, CI y revisión adversarial**

```text
# Rol
Actúa como Tech Lead Senior especializado en GitHub,
integración continua (CI), revisión de código y
desarrollo asistido por agentes de IA.

# Objetivo
Definir un proceso de Pull Requests para
"Descubre Barquisimeto" que garantice trazabilidad,
calidad y cumplimiento de las especificaciones
aprobadas antes de integrar cambios.

# Contexto
El proyecto utiliza:
- Monorepo con Next.js, Go y PostgreSQL.
- Metodologías SDD y TDD.
- OpenSpec como herramienta propuesta para gestionar
  especificaciones verificables.
- Harness con reglas, skills y agentes especializados.
- GitHub para control de versiones.

PR001 corresponde a la primera entrega documental
(README.md y prompts.md). Los PRs de implementación
corresponderán a entregas posteriores.

# Trabajo solicitado
1. Define una plantilla de Pull Request que incluya:
   objetivo, cambios, historias relacionadas,
   especificaciones afectadas, pruebas y riesgos.

2. Propón guardrails automatizados mediante GitHub
   Actions para verificar:
   - Tests unitarios y de integración.
   - Lint y comprobaciones de compilación.
   - Consistencia del contrato OpenAPI.
   - Validación de especificaciones.
   - Análisis de vulnerabilidades.

3. Define una revisión adversarial mediante un
   subagente independiente que contraste los cambios
   con las specs y busque errores, casos límite,
   problemas de seguridad y supuestos incorrectos.

4. Establece criterios para bloquear la integración
   cuando fallen controles obligatorios.

5. Define cuándo se requiere aprobación humana y
   cómo documentar los hallazgos y su resolución.

# Entregables
- Plantilla de descripción de Pull Request.
- Propuesta de controles CI y condiciones de bloqueo.
- Responsabilidades del revisor adversarial.
- Checklist de aprobación y cierre.
- Descripción propuesta para PR001.

# Restricciones
- No inventes pruebas ejecutadas ni revisiones realizadas.
- No afirmes que CI, agentes o guardrails ya funcionan.
- No permitas que un agente apruebe sus propios cambios.
- No modifiques requisitos o specs sin aprobación.
- Diferencia las verificaciones aplicables a PR001
  de las que corresponderán a PRs con código.
- No crees ramas, commits ni Pull Requests.
- No generes configuraciones sin autorización.

Entrega la propuesta en Markdown y espera mi aprobación.

# Correspondencia documental
Ubica el resultado en README.md §7: plantilla, PR001 documental y CI/revisión adversarial **previstos**.
Si una decisión sigue abierta, márcala como pendiente;
no afirmes que se ejecutaron herramientas, tests, CI
o despliegues sin evidencia verificable.
```
