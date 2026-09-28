# multi-agent-workflow

[![skills.sh](https://skills.sh/b/TheBaiter/multi-agent-workflow)](https://skills.sh/TheBaiter/multi-agent-workflow)

Skill experimental para organizar trabajo de producto y software como una **organización de agentes especializados**, con Morrison/Orchestrator como interfaz normal con el usuario.

> El usuario administra intención y autoridad. Morrison administra la organización.

Morrison no es el programador por defecto. Clasifica, delega, enruta preguntas, controla gates, conserva estado canónico y sintetiza resultados.

## Modelo general

```text
USER
  ↓
MORRISON / ORCHESTRATOR
  ↓
organizational backlog
  ↓
bounded delegation batches
  ├─ one-question Thinkers
  ├─ same-role A+B specialist pairs
  ├─ researchers
  ├─ implementation owners
  └─ independent validators
  ↓
canonical artifacts/state
  ↓
MORRISON
  ↓
USER
```

La organización conceptual puede tener muchas especialidades aunque el runtime sólo permita pocos subagentes simultáneos. El trabajo se ejecuta por tandas: cada tanda persiste hallazgos/artefactos/backlog, termina contextos y libera slots para la siguiente.

## Principios centrales

### Un agente, un rol

Cada personalidad estable tiene:

- un `Agent-Key`;
- una responsabilidad profesional principal;
- una asignación acotada;
- un `Work-Phase`;
- `Production-Write-Authority` explícita.

No se crean agentes compuestos como UX+Visual+Accessibility+Frontend o Backend+DB+Security.

### A+B del mismo rol

Trabajo cognitivo no trivial usa normalmente dos instancias frescas e independientes del **mismo Agent-Key**.

A y B trabajan aislados primero, luego comparan, hacen cross-review dentro de su especialidad y sintetizan sólo tras resolver/rutar/escalar diferencias materiales.

Dos especialidades distintas no satisfacen ese par.

### Un Thinker = una pregunta = terminar

Los Thinkers son contextos descartables.

Cada Thinker:

1. recibe estado canónico actual;
2. encuentra una sola pregunta material o devuelve `THINKER-CLEAN`;
3. retorna;
4. termina inmediatamente.

No planifica, implementa, valida ni mantiene memoria durable.

### Planning != implementation != validation

Los planners/reviewers normalmente no escriben producción.

Flujo general:

```text
planning
  ↓
plan reopening when required
  ↓
EXECUTION_READY
  ↓
Implementation Owner
  ↓
Independent Validator
```

### Plan reopening

Un plan `MATURE` no es automáticamente `EXECUTION_READY`.

Para trabajo importante/caro de rehacer se reabre con responsabilidades distintas:

- fresh Thinkers -> huecos;
- `review-challenger` A+B -> falsificación;
- `alternative-planner` A+B -> alternativa materialmente distinta;
- `risk-reviewer` A+B -> riesgo/retrabajo/fricción cuando corresponde.

## Departamentos / roles actuales

El catálogo canónico está en `references/profiles/README.md`.

Entre los roles generales actuales:

- `orchestrator`;
- `product-planner`;
- `researcher`;
- `technical-planner`;
- `ux-planner`;
- `information-architecture-planner`;
- `graphic-design-planner`;
- `interaction-design-planner`;
- `design-system-planner`;
- `accessibility-planner`;
- `frontend-architect`;
- `backend-architect`;
- `ui-question-auditor`;
- `review-challenger`;
- `alternative-planner`;
- `risk-reviewer`;
- `quality-strategist`;
- `implementation-owner`;
- `independent-validator`.

### Backend Planning

`backend-architect` se descubre a través de `references/departments/backend-planning.md`.

Posee únicamente arquitectura backend de dominio/servicios, workflows, invariantes, transacciones, concurrencia/idempotencia y semántica de fallos.

No posee API pública, persistencia/data, authentication/authorization, security, observability, performance, implementación ni QA. Esas responsabilidades se enrutan a especialistas separados o se registran como capability gaps si todavía no existe contrato estable.

### Historical functional backend defects

El workflow histórico sigue existiendo como un departamento especializado y aislado:

```text
detective -> analyzer -> planner -> challenger -> test-strategist -> executor -> validator -> consensus
```

Sus Agent-Keys no son aliases de los roles generales.

## Intensive UI Questioning

Para trabajo UI/frontend visible o perceptible se activa `intensive-ui-questioning` cuando corresponde.

Para trabajo delegado no trivial, MAW usa el rol `ui-question-auditor` y `references/ui-questioning-rounds.md`:

- 4 rondas frescas por defecto;
- 5 para trabajo amplio/de alto riesgo/rework-prone o cuando ronda 4 todavía cambia materialmente el artefacto;
- agentes nuevos en cada ronda;
- runtime IDs/nombres nuevos;
- preguntas procesadas una por una;
- continuidad mediante estado canónico, no reutilizando el hidden context del auditor anterior.

La skill UI puede descubrir preguntas de UX, IA, visual, accessibility, frontend, etc., pero no transfiere ownership: cada decisión se enruta al rol atómico correspondiente.

## Estado canónico

La organización no depende del chat para recordar el proyecto.

`references/orchestration-state.md` conserva, entre otras cosas:

- objetivo/task type/riesgo/gate;
- dependency availability;
- plan maturity;
- pair groups;
- batch/slot state;
- organizational backlog;
- preguntas con owner;
- artefactos canónicos;
- plan reopening;
- Council Session;
- implementación;
- validación;
- siguiente acción.

Principio:

> agentes pueden morir; el conocimiento canónico no.

## Dependencias de skills

MAW usa skills externas como **procedimientos**, no como nuevos roles.

### Requerida para modo completo

`agent-context-foundation`

Repositorio: `https://github.com/TheBaiter/agent-context-foundation`

Aplica progressive disclosure, ownership canónico, task traceability, promoción de conocimiento verificado, retiro de memoria obsoleta y handoffs resumibles.

### Requerida cuando hay UI visible/perceptible relevante

`intensive-ui-questioning`

Repositorio: `https://github.com/TheBaiter/intensive-ui-questioning`

### Dependency preflight

Morrison no interpreta una URL como instalación.

Antes de crear un agente estable registra cada dependencia como:

- `AVAILABLE`;
- `MISSING`;
- `BLOCKED`;
- `NOT_REQUIRED`.

Y opera en:

- `FULL`;
- `REDUCED`;
- `BLOCKED`.

Ver `references/installation-and-dependencies.md` y `references/skill-routing.md`.

## Instalación

### Skill individual

```bash
npx skills add TheBaiter/multi-agent-workflow
```

### Instalación completa actual

Mientras no exista un Pack publicado:

```bash
npx skills add TheBaiter/agent-context-foundation
npx skills add TheBaiter/intensive-ui-questioning
npx skills add TheBaiter/multi-agent-workflow
```

Instalar sólo MAW sigue siendo válido como Skill standalone, pero no autoriza a afirmar garantías `FULL` si falta una dependencia requerida para la tarea.

## Instalación única con skills.sh Pack

skills.sh soporta **Packs**, colecciones de varias skills instalables con un único comando.

Ése es el mecanismo recomendado para distribuir este conjunto como una sola instalación manteniendo cada skill en su repositorio canónico.

Pack objetivo:

```text
Multi-Agent Workflow Pack
- TheBaiter/agent-context-foundation
- TheBaiter/intensive-ui-questioning
- TheBaiter/multi-agent-workflow
```

Estado actual:

`Pack-Status: NOT_PUBLISHED`

No se publica ni documenta un ID ficticio.

Cuando exista un Pack real, este README deberá contener su URL exacta. El formato de instalación será:

```bash
npx skills add https://skills.sh/p/<real-pack-id>
```

Un Agent Plugin puede ser útil en el futuro para empaquetar además tools/MCP/resources, pero **no es necesario** para conseguir instalación única de estas tres skills.

## Requisitos de runtime

Para garantías completas se necesita:

- runtime capaz de crear subagentes/contextos realmente aislados;
- acceso al repositorio/evidencia relevante;
- estado durable/canónico;
- disponibilidad real de las skills requeridas/activas;
- idealmente control de reasoning/tools/capabilities por hijo.

Si no hay subagentes reales, puede utilizarse modo degradado, pero no debe afirmarse que existió independencia multi-agente.

## Council Session

Normalmente el usuario habla sólo con Morrison.

Si el usuario pide discutir directamente con especialistas, Morrison puede abrir una Council Session temporal cuando el host lo soporta. Morrison sigue siendo chair; cada participante conserva una sola especialidad.

Si la UI/runtime no permite múltiples voces reales, Morrison retransmite outputs etiquetados y no finge participación directa.

## Contratos principales

- `SKILL.md`
- `references/profiles/orchestrator/PROFILE.md`
- `references/orchestrator-runtime.md`
- `references/organization-model.md`
- `references/role-purity.md`
- `references/paired-delegation.md`
- `references/batched-delegation.md`
- `references/orchestration-state.md`
- `references/plan-reopening.md`
- `references/installation-and-dependencies.md`
- `references/skill-routing.md`
- `references/thinker-waves.md`
- `references/ui-questioning-rounds.md`
- `references/profiles/README.md`

## Estado

**Experimental.**

La meta es que el usuario pueda hablar con un manager que organice especialistas, no administrar manualmente una colección de prompts; y que la organización invierta razonamiento/revisión antes de comprometerse con trabajo caro de rehacer.