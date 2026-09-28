# multi-agent-workflow

[![skills.sh](https://skills.sh/b/TheBaiter/multi-agent-workflow)](https://skills.sh/TheBaiter/multi-agent-workflow)

Skill experimental para organizar trabajo de producto y desarrollo como una **organización de agentes reales**, con un Orchestrator como interfaz normal con el usuario.

La idea central:

> el usuario administra la intención; el Orchestrator administra la organización.

El objetivo no es sumar agentes por sumar agentes. Es reducir retrabajo separando responsabilidades, descubriendo preguntas antes de que el código congele decisiones incompletas y evitando que el mismo contexto sea quien idea, implementa y aprueba todo.

## Modelo general

~~~text
USER
  ↓
ORCHESTRATOR
  ├─ Product Planner
  ├─ Researcher
  ├─ Technical Planner
  ├─ Review Challenger
  ├─ Quality Strategist
  ├─ Implementation Owner
  ├─ Independent Validator
  └─ Ephemeral Thinker Waves
~~~

No es un pipeline obligatorio. El Orchestrator levanta únicamente la organización necesaria para la tarea actual.

## El Orchestrator es la puerta de entrada

Normalmente el usuario habla sólo con el Orchestrator.

Su trabajo es:

- entender el objetivo;
- separar decisiones del usuario de incógnitas que la organización puede resolver;
- clasificar el tipo de tarea;
- elegir el siguiente dueño del trabajo;
- crear un contrato explícito para cada subagente;
- decidir secuencia y paralelismo;
- asignar capacidad/razonamiento según dificultad;
- controlar qué puede tocar cada agente;
- conocer el estado de cada contexto activo;
- recibir resultados y objeciones;
- escalar únicamente decisiones que requieren autoridad del usuario;
- terminar contextos que ya cumplieron su función;
- devolver una síntesis coherente.

El Orchestrator **no es el programador por defecto**.

Contratos principales:

- `references/profiles/orchestrator/PROFILE.md`
- `references/orchestrator-runtime.md`
- `references/organization-model.md`
- `references/orchestration-state.md`

## El Orchestrator no improvisa agentes

Cada subagente estable nace con un `AGENT-MANIFEST`.

Conceptualmente:

~~~text
AGENT-MANIFEST

Agent-Key: technical-planner
Parent: orchestrator
Task-Type: TECHNICAL_CHANGE
Reasoning-Class: DEEP
Lifecycle-State: CREATED

Objective:
Diseñar el cambio X sin implementar.

Inputs:
- Product Brief actual
- repositorio/contratos relevantes

Owned-Decisions:
- arquitectura y estrategia técnica dentro del scope aprobado

Must-Not:
- cambiar producto
- escribir producción
- aprobar su propio plan como validación final

Can-Spawn:
- THINKERS_ONLY
- researcher

Expected-Return:
- TECHNICAL-PLAN

Completion-Criteria:
- plan implementable + acceptance explícita + sin huecos materiales abiertos

Escalate-When:
- falta decisión de producto
- evidencia técnica insuficiente
~~~

El perfil define **qué clase de empleado es**.

El manifest define **qué trabajo concreto tiene permitido realizar esta instancia**.

## Clasificación de tareas

El Orchestrator utiliza tipos explícitos:

- `IDEA_OR_PRODUCT`
- `TECHNICAL_CHANGE`
- `INVESTIGATION`
- `IMPLEMENTATION`
- `VALIDATION`
- `FUNCTIONAL_BACKEND_DEFECT`
- `TRIVIAL`

Ejemplos:

- una idea nueva -> Product Planner;
- una duda técnica/repo/documentación -> Researcher;
- comportamiento claro pero diseño pendiente -> Technical Planner;
- plan aprobado -> Implementation Owner;
- resultado terminado -> Independent Validator;
- bug funcional backend que cumple el scope estricto -> departamento especializado.

El tipo puede cambiar cuando aparece nueva evidencia.

## Perfiles generales

~~~text
references/profiles/
  orchestrator/
  product-planner/
  researcher/
  technical-planner/
  review-challenger/
  quality-strategist/
  implementation-owner/
  independent-validator/
~~~

Responsabilidades:

- `orchestrator`: organización, routing, autoridad, lifecycle y convergencia;
- `product-planner`: producto, alcance y Product Brief;
- `researcher`: hechos, evidencia, comportamiento actual, documentación y factibilidad;
- `technical-planner`: diseño técnico y contrato de implementación;
- `review-challenger`: ataque adversarial a artefactos maduros;
- `quality-strategist`: criterios falsables y estrategia de verificación;
- `implementation-owner`: implementación fiel del plan;
- `independent-validator`: evaluación final fresca e independiente.

Los perfiles históricos `detective/analyzer/planner/challenger/test-strategist/executor/validator` pertenecen al departamento estricto de bugs backend y **no son aliases de estos roles generales**.

## Madurar ideas antes de programar

Uno de los problemas que esta skill intenta atacar ocurre antes de escribir código.

Una idea inicial puede ser correcta pero incompleta. Por ejemplo:

> "quiero una página para crear renders 3D"

Eso no responde todavía:

- quién usa el producto;
- qué guarda;
- quién es dueño del contenido;
- si existe perfil/identidad;
- si hay contenido público o privado;
- si existe comunidad;
- cómo se descubre contenido;
- qué debe moderarse;
- qué datos deben ser reutilizables;
- qué seguridad necesita;
- cómo se prueba;
- qué podría consumir ese contenido en el futuro;
- qué decisiones serán caras de migrar después.

La organización utiliza una etapa de **Idea Maturation / Product Discovery** antes de una implementación importante.

Los hallazgos se clasifican como:

- `NOW`: entra ahora;
- `FOUNDATION`: quizá no sea visible ahora, pero la base actual no debería bloquearlo;
- `DEFERRED`: conocido y conscientemente pospuesto;
- `OPTION`: posible dirección que requiere una decisión futura;
- `REJECTED`: considerado y descartado.

Esto permite pensar el futuro sin convertir cada posibilidad en scope inmediato.

Contrato:

`references/idea-maturation.md`

Perfil:

`references/profiles/product-planner/PROFILE.md`

## Thinker Waves

Los **Thinkers** son contextos descartables cuya única función es encontrar preguntas y huecos.

No implementan. No aprueban. No poseen decisiones durables.

~~~text
estado canónico actual
        ↓
Thinker Wave nueva
        ↓
preguntas / huecos materiales
        ↓
roles responsables responden o cambian el artefacto
        ↓
estado canónico actualizado
        ↓
la Wave muere
        ↓
nueva Wave fresca si todavía hace falta cuestionar
~~~

La nueva Wave no hereda la conversación de la anterior.

El proyecto recuerda decisiones y evidencia; el revisor no recuerda cómo razonó el revisor anterior.

Contrato:

`references/thinker-waves.md`

## Estados de los agentes

Los subagentes estables utilizan un lifecycle común:

- `CREATED`
- `WORKING`
- `QUESTIONING`
- `WAITING_PARENT`
- `WAITING_CHILD`
- `BLOCKED`
- `RETURNED_COMPLETE`
- `RETURNED_INCONCLUSIVE`
- `RETURNED_REJECTED`
- `TERMINATED`

Thinkers:

`CREATED -> WORKING -> RETURNED -> TERMINATED`

Un `RETURNED_COMPLETE` significa que ese agente terminó **su encargo**, no que todo el proyecto esté aprobado.

## Estado canónico de la organización

El chat del Orchestrator no debería ser la única memoria de quién está haciendo qué.

`references/orchestration-state.md` define un estado durable con:

- objetivo;
- Task-Type;
- riesgo;
- gate actual;
- decisiones fijas;
- preguntas materiales abiertas y su dueño;
- artefactos canónicos;
- agentes activos;
- parent de cada agente;
- Reasoning-Class;
- lifecycle;
- qué espera cada uno;
- gates pasados/stale;
- siguiente acción.

Principio:

> la organización puede olvidar conversaciones; no puede olvidar estado.

Esto permite matar y recrear contextos sin depender de memoria conversacional.

## Todos tienen voz, no todos tienen autoridad

Los agentes pueden cuestionarse entre sí.

Una objeción material no desaparece porque otro agente quiera avanzar, pero tampoco cada opinión se convierte en un bloqueo.

La autoridad se mantiene escalonada:

~~~text
User
  ↓
Orchestrator
  ↓
Delegated Work Owner
  ↓
Supporting Specialist / Thinker
~~~

Una pregunta se resuelve en el nivel más bajo que realmente posee esa decisión.

Si evidencia, documentación, tests, código o un especialista pueden responderla, se resuelve internamente.

El usuario recibe preguntas sólo cuando son realmente decisiones de producto, alcance, preferencia, información externa o aceptación de riesgo bajo su autoridad.

## Delegación recursiva controlada

Un dueño de trabajo puede levantar ayudantes únicamente si su manifest lo autoriza.

Profundidad normal:

~~~text
User
  -> Orchestrator
       -> Work Owner
            -> Specialist / Thinker
~~~

No se busca un swarm.

El Orchestrator siempre debería poder responder:

- qué agentes están activos;
- quién es el parent de cada uno;
- qué posee cada uno;
- qué estado tiene;
- qué artefacto debe devolver;
- qué está esperando;
- cuáles pueden morir ahora.

Si no puede reconstruir eso, debe reparar el estado organizacional antes de seguir creando agentes.

## Modelos y niveles de razonamiento

La jerarquía organizacional no implica que el manager deba ser el modelo más costoso.

Cuando el runtime lo permita:

- `LIGHT`: coordinación, routing, estado, extracción mecánica;
- `STANDARD`: implementación normal, investigación acotada, pruebas rutinarias;
- `DEEP`: product discovery, arquitectura ambigua, root cause, security, challenge adversarial, migraciones, concurrencia, integridad y validación importante;
- `MAX`: decisiones de impacto/ambigüedad extraordinarios donde un error sería muy caro.

Las herramientas especialistas son otra dimensión distinta al Reasoning-Class.

Es válido usar un Orchestrator relativamente liviano si sabe detectar incertidumbre, delegar y escalar correctamente.

## Separar plan, ejecución y validación

Para trabajo sustancial general:

~~~text
Product/Objective maturity
      ↓
Technical Planner
      ↓
Review Challenger / Quality Strategist
      ↓
Implementation Owner
      ↓
Independent Validator
~~~

El Implementation Owner puede devolver la planificación si descubre que no se puede implementar sin alterar una premisa.

No debería rediseñar silenciosamente el contrato.

El Validator recibe requisitos y evidencia actuales, no una orden de "confirmar que el implementador está bien".

## Tool boundaries

Cuando el runtime permita limitar herramientas:

- Researcher -> lectura/search/docs/repositorio;
- Product Planner -> lectura, sin writes de producción;
- Technical Planner -> lectura/análisis, sin writes de producción;
- Thinker -> read-only;
- Review Challenger -> read/inspect;
- Quality Strategist -> diseño/ejecución de verificación cuando aplique;
- Implementation Owner -> write/build/test según plan;
- Independent Validator -> read/inspect/test, production writes desactivados por defecto.

Si el runtime no puede restringir técnicamente las herramientas, el manifest sigue siendo la frontera de autoridad.

## Gates

El Orchestrator no avanza por confianza verbal.

Los gates principales son:

- Product Gate;
- Plan Gate;
- Execution Gate;
- Validation Gate;
- User Decision Gate.

Un cambio material upstream puede marcar downstream como `STALE` y obligar a reevaluar solamente las partes afectadas.

## Departamento especializado: backend functional defects

El workflow original no desapareció.

Funciona como un **departamento especializado** que el Orchestrator activa cuando existe un defecto funcional backend real.

~~~text
Detective
  ↓
Analyzer
  ↓
Planner
  ↓
Challenger
  ↓
Test Strategist
  ↓
Implementation
  ↓
Validator
  ↓
Consensus / Close
~~~

Ese protocolo conserva sus reglas estrictas:

- scope funcional backend;
- pases diferenciados;
- GitHub Issue como case file;
- `Agent-Key` estable;
- preguntas y retornos;
- estados fail-closed;
- ejecución manual o por Executor;
- evidencia;
- aprobación unánime para cierre.

Perfiles especializados:

~~~text
references/profiles/
  detective/
  analyzer/
  planner/
  challenger/
  test-strategist/
  executor/
  validator/
~~~

Estas restricciones no se aplican mecánicamente a cualquier trabajo general.

## Companion: agent-context-foundation

Este proyecto utiliza [$agent-context-foundation](https://github.com/TheBaiter/agent-context-foundation) para contexto durable, progressive disclosure, ownership canónico y promoción de conocimiento reutilizable.

Responsabilidades:

- `agent-context-foundation`: conocimiento durable del repositorio y ownership contextual;
- `multi-agent-workflow`: organización y ejecución del trabajo entre agentes.

La cronología concreta de una tarea permanece en su estado canónico. Sólo conocimiento verificado y reutilizable debería promocionarse al contexto durable.

## Requisitos

Para ejecutar el protocolo completo se necesita:

- runtime capaz de levantar subagentes/contextos realmente aislados;
- acceso al repositorio/evidencia necesaria;
- acceso al estado durable que gobierna la tarea;
- idealmente, capacidad de elegir reasoning/model/tools por agente.

Si no existen subagentes reales, puede utilizarse un modo degradado, pero no debería afirmarse que hubo independencia multi-agente.

## Instalación

~~~bash
npx skills add TheBaiter/multi-agent-workflow
~~~

Companion recomendado:

~~~bash
npx skills add TheBaiter/agent-context-foundation
~~~

## Estado

**Experimental.**

La meta es que el usuario pueda hablar con un manager, no administrar manualmente una colección de prompts; y que la organización invierta razonamiento barato antes de comprometerse con código caro de rehacer.