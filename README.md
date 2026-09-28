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
  ├─ UI / Frontend / Backend specialist planners
  ├─ Review Challenger
  ├─ Alternative Planner
  ├─ Risk Reviewer
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
- `references/installation-and-dependencies.md`
- `references/skill-routing.md`

## El Orchestrator no improvisa agentes

Cada subagente estable nace con un `AGENT-MANIFEST`.

El perfil define **qué clase de empleado es**.

El manifest define **qué trabajo concreto tiene permitido realizar esta instancia**.

El manifest también registra las skills requeridas/condicionales y su disponibilidad real. Una URL de GitHub no cuenta como prueba de que una dependencia esté instalada.

## Clasificación de tareas

El Orchestrator utiliza tipos explícitos:

- `IDEA_OR_PRODUCT`
- `TECHNICAL_CHANGE`
- `INVESTIGATION`
- `IMPLEMENTATION`
- `VALIDATION`
- `FUNCTIONAL_BACKEND_DEFECT`
- `TRIVIAL`

El tipo puede cambiar cuando aparece nueva evidencia.

## Roles y departamentos generales

Los roles generales están registrados en `references/profiles/README.md` y se descubren mediante contratos departamentales.

Entre los roles actuales se incluyen:

- `orchestrator`;
- `product-planner`;
- `researcher`;
- `technical-planner`;
- planners especializados de UI;
- `frontend-architect`;
- `backend-architect`;
- `ui-question-auditor`;
- `review-challenger`;
- `alternative-planner`;
- `risk-reviewer`;
- `quality-strategist`;
- `implementation-owner`;
- `independent-validator`.

`backend-architect` se descubre a través de `references/departments/backend-planning.md` y posee únicamente arquitectura backend de dominio/servicios, workflows, invariantes, transacciones, concurrencia/idempotencia y semántica de fallos. API pública, datos/persistencia, auth, security, observability y performance siguen siendo responsabilidades separadas.

Los perfiles históricos `detective/analyzer/planner/challenger/test-strategist/executor/validator` pertenecen al departamento estricto de bugs backend y **no son aliases de estos roles generales**.

## Madurar ideas antes de programar

Uno de los problemas que esta skill intenta atacar ocurre antes de escribir código.

La organización utiliza una etapa de **Idea Maturation / Product Discovery** antes de una implementación importante.

Los hallazgos se clasifican como:

- `NOW`: entra ahora;
- `FOUNDATION`: quizá no sea visible ahora, pero la base actual no debería bloquearlo;
- `DEFERRED`: conocido y conscientemente pospuesto;
- `OPTION`: posible dirección que requiere una decisión futura;
- `REJECTED`: considerado y descartado.

Contrato:

`references/idea-maturation.md`

## Thinker Waves

Los **Thinkers** son contextos descartables cuya única función es encontrar preguntas y huecos.

Regla central:

> un Thinker = una pregunta material = terminar.

La nueva Wave no hereda la conversación de la anterior. El proyecto recuerda decisiones y evidencia; el revisor no recuerda cómo razonó el revisor anterior.

Contrato:

`references/thinker-waves.md`

## Pares y batching

El trabajo cognitivo no trivial utiliza normalmente pares A+B frescos del **mismo Agent-Key**.

La organización puede ser más grande que la cantidad de slots disponibles: trabaja por tandas, persiste resultados/backlog, termina contextos y reutiliza los slots con agentes nuevos.

Contratos:

- `references/paired-delegation.md`
- `references/batched-delegation.md`

## Intensive UI Questioning

Para trabajo UI/frontend visible o perceptible se activa `intensive-ui-questioning` cuando corresponde.

En trabajo delegado no trivial, la integración usa `ui-question-auditor` con **4 rondas frescas por defecto** y **5** para casos amplios/de alto riesgo/costo de retrabajo o cuando la ronda 4 todavía cambia materialmente el artefacto.

Cada ronda usa instancias/nombres nuevos; los hallazgos sobreviven mediante estado canónico, no reutilizando el contexto conversacional del auditor anterior.

Contrato local:

`references/ui-questioning-rounds.md`

## Estado canónico de la organización

El chat del Orchestrator no debería ser la única memoria de quién está haciendo qué.

`references/orchestration-state.md` define estado durable para reconstruir objetivo, gates, decisiones, preguntas, batches, pares, backlog, artefactos, skills/dependencias, implementación y validación.

Principio:

> la organización puede olvidar conversaciones; no puede olvidar estado.

## Todos tienen voz, no todos tienen autoridad

Los agentes pueden cuestionarse entre sí. Una pregunta se resuelve en el nivel más bajo que realmente posee esa decisión.

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

No se busca un swarm permanente. Los agentes terminan cuando su trabajo fue checkpointed.

## Modelos y niveles de razonamiento

Cuando el runtime lo permita:

- `LIGHT`: coordinación, routing, estado, extracción mecánica;
- `STANDARD`: implementación normal, investigación acotada, pruebas rutinarias;
- `DEEP`: product discovery, arquitectura ambigua, root cause, security, challenge adversarial, migraciones, concurrencia, integridad y validación importante;
- `MAX`: decisiones de impacto/ambigüedad extraordinarios donde un error sería muy caro.

## Separar plan, ejecución y validación

Para trabajo sustancial:

~~~text
Product/Objective maturity
      ↓
Specialist planning pairs
      ↓
Plan reopening / quality strategy
      ↓
Implementation Owner
      ↓
Independent Validator
~~~

El implementador puede devolver la planificación si descubre que no se puede implementar sin alterar una premisa.

## Departamento especializado: backend functional defects

El workflow original no desapareció. Funciona como un **departamento especializado** que el Orchestrator activa cuando existe un defecto funcional backend real.

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

Estas restricciones no se aplican mecánicamente a cualquier trabajo general.

## Dependencias de skills

Para funcionamiento completo, esta skill usa:

1. `agent-context-foundation` — **requerida** como baseline para todos los roles estables;
2. `intensive-ui-questioning` — **requerida cuando se activa trabajo UI/frontend visible o perceptible**;
3. `multi-agent-workflow` — Orchestrator y organización.

Morrison verifica la disponibilidad real antes de crear agentes afectados. Estados posibles: `AVAILABLE`, `MISSING`, `BLOCKED`, `NOT_REQUIRED`.

Ver:

`references/installation-and-dependencies.md`

## Instalación completa recomendada

~~~bash
npx skills add TheBaiter/agent-context-foundation
npx skills add TheBaiter/intensive-ui-questioning
npx skills add TheBaiter/multi-agent-workflow
~~~

Instalar sólo `multi-agent-workflow` sigue siendo válido como Skill standalone, pero **no autoriza a afirmar garantías completas** si una dependencia requerida para la tarea no está disponible.

`agent-context-foundation` es obligatoria para el modo completo de roles estables. `intensive-ui-questioning` puede quedar `NOT_REQUIRED` cuando no existe trabajo UI/perceptible.

### Instalación en una sola operación

El formato actual permanece como Skill standalone con dependencias explícitas.

Una distribución futura "install once" debe ser un **Agent Plugin real** que empaquete/exponga las tres skills bajo el formato oficial de plugins/skills. No se incluye un `plugin.json` cosmético mientras las skills dependientes sigan siendo repositorios externos, porque eso produciría un paquete que parece autocontenido pero no lo es.

## Requisitos

Para ejecutar el protocolo completo se necesita:

- runtime capaz de levantar subagentes/contextos realmente aislados;
- acceso al repositorio/evidencia necesaria;
- acceso al estado durable que gobierna la tarea;
- disponibilidad real de las skills requeridas/activas;
- idealmente, capacidad de elegir reasoning/model/tools por agente.

Si no existen subagentes reales, puede utilizarse un modo degradado, pero no debería afirmarse que hubo independencia multi-agente.

## Estado

**Experimental.**

La meta es que el usuario pueda hablar con un manager, no administrar manualmente una colección de prompts; y que la organización invierta razonamiento barato antes de comprometerse con código caro de rehacer.