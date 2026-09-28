# multi-agent-workflow

[![skills.sh](https://skills.sh/b/TheBaiter/multi-agent-workflow)](https://skills.sh/TheBaiter/multi-agent-workflow)

Skill experimental para organizar trabajo de producto y desarrollo como una **organización de agentes reales**, con un Orchestrator como única interfaz normal con el usuario.

La idea central es sencilla:

> el usuario administra la intención; el Orchestrator administra la organización.

El objetivo no es sumar agentes por sumar agentes. Es reducir retrabajo separando responsabilidades, haciendo preguntas antes de que el código congele decisiones incompletas y evitando que el mismo contexto sea quien idea, implementa y aprueba todo.

## Modelo general

~~~text
USER
  ↓
ORCHESTRATOR
  ↓
DELEGATED WORK OWNER
  ├─ Product Planner
  ├─ Analyzer / Researcher
  ├─ Technical Planner
  ├─ Challenger
  ├─ Test Strategist
  ├─ Executor
  ├─ Validator
  └─ Ephemeral Thinker Waves
~~~

No es un pipeline obligatorio. El Orchestrator levanta únicamente la organización necesaria para la tarea actual.

## El Orchestrator es la puerta de entrada

Normalmente el usuario habla sólo con el Orchestrator.

Su trabajo es:

- entender el objetivo;
- detectar qué información realmente falta;
- evitar preguntarle al usuario cosas que el propio proyecto puede responder;
- elegir quién debe trabajar;
- delegar;
- decidir secuencia y paralelismo;
- asignar capacidad/razonamiento según dificultad cuando el runtime lo permita;
- recibir resultados y objeciones;
- escalar únicamente decisiones que requieren autoridad del usuario;
- devolver una síntesis coherente.

El Orchestrator **no es el programador por defecto**.

No debería hacer todo el análisis, escribir el plan, implementar y luego validarse a sí mismo cuando existen subagentes reales disponibles.

Su perfil está en:

`references/profiles/orchestrator/PROFILE.md`

El modelo organizacional completo está en:

`references/organization-model.md`

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

## Todos tienen voz, no todos tienen autoridad

Los agentes pueden cuestionarse entre sí.

Una objeción material no desaparece porque otro agente quiera avanzar, pero tampoco cada opinión se convierte en un bloqueo.

La autoridad se mantiene escalonada:

~~~text
User
  ↓
Orchestrator
  ↓
Delegated owner
  ↓
Specialists
~~~

Una pregunta se resuelve en el nivel más bajo que realmente posee esa decisión.

Si evidencia, documentación, tests, código o un especialista pueden responderla, se resuelve internamente.

El usuario recibe preguntas sólo cuando son realmente decisiones de producto, alcance, preferencia, información externa o aceptación de riesgo bajo su autoridad.

## Delegación recursiva

Un Planner o dueño de trabajo puede levantar sus propios ayudantes.

Por ejemplo:

~~~text
Orchestrator
  ↓
Planner
  ├─ Thinker A
  ├─ Thinker B
  ├─ Security specialist
  └─ Test strategist
~~~

Pero cada agente debe tener:

- un objetivo concreto;
- un padre al que retornar;
- autoridad explícita;
- contexto canónico;
- un resultado esperado;
- una condición de escalamiento.

La intención es construir una organización, no un swarm sin dueño.

## Modelos y niveles de razonamiento

La jerarquía organizacional no implica que el manager deba ser el modelo más costoso.

Cuando el runtime lo permita, el Orchestrator puede enrutar capacidad por necesidad:

- `LIGHT`: coordinación, routing, estado, chequeos mecánicos;
- `STANDARD`: implementación normal, investigación acotada, pruebas rutinarias;
- `DEEP`: arquitectura ambigua, planificación costosa, debugging complejo, challenge adversarial, migraciones, concurrencia, integridad y validación crítica;
- `SPECIALIST`: capacidades/herramientas específicas.

Es válido usar un Orchestrator relativamente liviano si sabe detectar incertidumbre, delegar y escalar correctamente.

No es válido ahorrar capacidad asignando deliberadamente un agente insuficiente a una decisión cara o irreversible.

## Separar plan, ejecución y validación

Para trabajo sustancial se prefiere:

~~~text
Planner / Owner
      ↓
Executor
      ↓
Independent Validator
~~~

El Executor puede devolver una planificación si descubre que no se puede implementar sin alterar una premisa.

No debería rediseñar silenciosamente el contrato.

El Validator recibe requisitos y evidencia actuales, no una orden de "confirmar que el Executor está bien".

## Estado canónico

La conversación de un agente no debería ser la única memoria del proyecto.

La organización necesita un artefacto canónico apropiado al entorno: Issue, documento de tarea, Product Brief, plan técnico u otro estado durable.

Como mínimo debería permitir reconstruir:

- objetivo;
- scope;
- decisiones fijas;
- preguntas abiertas;
- evidencia;
- dueño/etapa actual;
- plan vigente;
- estado de implementación;
- estado de validación;
- siguiente acción.

Esto permite matar/recrear agentes sin perder el proyecto.

## Departamento especializado: backend functional defects

El workflow original no desapareció.

Ahora funciona como un **departamento especializado** que el Orchestrator puede activar cuando existe un defecto funcional backend real.

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

Ese protocolo mantiene sus reglas estrictas:

- scope funcional backend;
- pases diferenciados;
- GitHub Issue como case file;
- `Agent-Key` estable;
- preguntas y retornos;
- estados fail-closed;
- ejecución manual o por Executor;
- evidencia;
- aprobación unánime para cierre.

Contratos relacionados:

- `references/scope.md`
- `references/workflow.md`
- `references/state-machine.md`
- `references/issue-protocol.md`
- `references/evidence-policy.md`
- `references/consensus.md`

Estas restricciones no se aplican mecánicamente a cualquier trabajo general.

## Perfiles

~~~text
references/profiles/
  orchestrator/
  product-planner/
  detective/
  analyzer/
  planner/
  challenger/
  test-strategist/
  executor/
  validator/
~~~

Los Thinkers no tienen perfil persistente: son contextos efímeros.

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
- acceso al estado durable que gobierna la tarea.

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