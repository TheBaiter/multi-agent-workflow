# multi-agent-workflow

[![skills.sh](https://skills.sh/b/TheBaiter/multi-agent-workflow)](https://skills.sh/TheBaiter/multi-agent-workflow)

Skill experimental para organizar trabajo de producto y software como una **organización de agentes especializados**, con Morrison/Orchestrator como interfaz normal con el usuario.

> El usuario administra intención y autoridad. Morrison administra la organización.

Morrison clasifica, delega, enruta preguntas, controla gates, conserva estado canónico y sintetiza resultados. No es el programador ni el arquitecto universal por defecto.

## Modelo

```text
USER
  <->
MORRISON / ORCHESTRATOR
  -> preguntas / Thinkers frescos
  -> departamentos y roles atómicos
  -> pares A+B del mismo rol
  -> tandas según slots disponibles
  -> artefactos / preguntas / backlog canónico
  -> implementación explícita
  -> validación independiente
  -> Morrison
  <->
USER
```

La organización conceptual puede ser mucho mayor que la concurrencia del runtime. Los agentes terminados liberan slots; sus resultados sobreviven en estado canónico.

## Reglas centrales

### Un agente, un rol

Cada personalidad estable tiene un `Agent-Key`, una profesión, una asignación acotada, `Work-Phase` y `Production-Write-Authority`.

No se crean agentes compuestos como UX+Visual+Accessibility+Frontend, Backend+DB+Security o Planner+Implementer+Validator.

Si un rol se satura, se divide organizacionalmente.

### Sólo roles contratados

Un nombre mencionado como capacidad no es automáticamente un Agent-Key.

Morrison sólo puede instanciar roles con perfil/contrato estable y ruta descubrible. Si falta una especialidad, registra un **capability gap** en vez de ensanchar el rol más cercano.

### A+B del mismo rol

Trabajo cognitivo no trivial usa normalmente dos instancias frescas e independientes del **mismo Agent-Key**.

A y B trabajan aislados primero; luego comparan, hacen cross-review dentro de su especialidad y sintetizan sólo tras resolver/rutar/escalar diferencias materiales.

Dos especialidades distintas no satisfacen el par.

### Un Thinker = una pregunta = terminar

Cada Thinker devuelve una única `THINKER-QUESTION` material o `THINKER-CLEAN` y termina inmediatamente.

No planifica, implementa, valida ni mantiene memoria durable.

### Planning != implementation != validation

Los planners/reviewers normalmente tienen `Production-Write-Authority: NO`.

```text
planning
  -> plan reopening cuando corresponde
  -> EXECUTION_READY
  -> Implementation Owner
  -> Independent Validator
```

## Roles/departamentos actuales

El catálogo canónico vive en `references/profiles/README.md`.

Roles generales contratados actualmente incluyen:

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

### UI Planning

`references/departments/ui-planning.md`

Separa UX, IA, diseño gráfico, interacción, design system y accesibilidad en roles atómicos.

### Frontend Planning

`references/departments/frontend-planning.md`

`frontend-architect` posee estructura frontend: módulos/componentes, state ownership, data flow, routing/rendering e integration seams. No absorbe UX/visual/accessibility/backend/API/data ni implementación.

### Backend Planning

`references/departments/backend-planning.md`

`backend-architect` posee únicamente arquitectura backend de dominio/servicios, workflows, invariantes, transacciones, concurrencia/idempotencia, failure/recovery semantics y dependency direction.

No posee API pública, persistencia/data, authn/authz, security, observability, performance, implementación ni QA. Esas responsabilidades se enrutan a especialistas separados o capability gaps.

### Technical Integration

El Agent-Key histórico `technical-planner` conserva su nombre por compatibilidad, pero su rol actual es **Cross-Department Technical Integration Planner**.

No es un arquitecto técnico genérico.

Se usa sólo cuando **dos o más planes técnicos especializados ya maduros** necesitan reconciliar:

- dependencias;
- compatibilidad entre contratos;
- seams/handoffs;
- orden de implementación;
- orden de rollout/migración/rollback;
- contradicciones que deben volver a los premise owners.

Un cambio sólo frontend va al especialista frontend. Uno sólo backend va al especialista backend. Una capacidad sin rol contratado queda como capability gap.

## Historical functional backend defects

El workflow histórico sigue existiendo como departamento especializado y aislado:

```text
detective -> analyzer -> planner -> challenger -> test-strategist -> executor -> validator -> consensus
```

Sus Agent-Keys no son aliases de los roles generales.

## Plan reopening

Un plan `MATURE` no es automáticamente `EXECUTION_READY`.

Para trabajo importante/caro de rehacer:

- fresh Thinkers -> huecos;
- `review-challenger` A+B -> falsificación;
- `alternative-planner` A+B -> alternativa materialmente distinta;
- `risk-reviewer` A+B -> riesgo/retrabajo/fricción cuando corresponde.

## Intensive UI Questioning

Para trabajo UI/frontend visible o perceptible se activa `intensive-ui-questioning` cuando corresponde.

En trabajo delegado no trivial, MAW usa `ui-question-auditor` y `references/ui-questioning-rounds.md`:

- 4 rondas frescas por defecto;
- 5 para trabajo amplio/de alto riesgo/rework-prone o cuando ronda 4 todavía cambia materialmente el artefacto;
- agentes/IDs/nombres nuevos en cada ronda;
- preguntas procesadas una por una;
- continuidad mediante estado canónico, no reutilizando el hidden context del auditor anterior.

La skill puede descubrir preguntas de muchas especialidades, pero no transfiere ownership entre roles.

## Estado canónico

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

> agentes pueden morir; el conocimiento canónico no.

## Dependencias de skills

MAW usa skills externas como procedimientos, no como nuevos roles.

### Requerida para modo completo

`agent-context-foundation`

Repositorio: `https://github.com/TheBaiter/agent-context-foundation`

### Requerida cuando hay UI visible/perceptible relevante

`intensive-ui-questioning`

Repositorio: `https://github.com/TheBaiter/intensive-ui-questioning`

Morrison hace dependency preflight antes de crear agentes estables y registra:

- `AVAILABLE`;
- `MISSING`;
- `BLOCKED`;
- `NOT_REQUIRED`.

El modo puede ser `FULL`, `REDUCED` o `BLOCKED`.

Una URL no cuenta como instalación.

## Instalación

### Skill individual

```bash
npx skills add TheBaiter/multi-agent-workflow
```

### Conjunto completo actual

Mientras no exista un Pack publicado:

```bash
npx skills add TheBaiter/agent-context-foundation
npx skills add TheBaiter/intensive-ui-questioning
npx skills add TheBaiter/multi-agent-workflow
```

Instalar sólo MAW sigue siendo válido como Skill standalone, pero no permite afirmar garantías `FULL` si una dependencia requerida no está disponible.

### Instalación única con skills.sh Pack

skills.sh soporta Packs de múltiples skills. Ése es el mecanismo previsto para una instalación única manteniendo cada skill en su repositorio canónico.

Pack objetivo:

```text
Multi-Agent Workflow Pack
- TheBaiter/agent-context-foundation
- TheBaiter/intensive-ui-questioning
- TheBaiter/multi-agent-workflow
```

Estado actual:

`Pack-Status: NOT_PUBLISHED`

No se documenta un ID ficticio. Cuando exista un Pack real, debe registrarse su URL exacta.

## Runtime necesario

Para garantías completas se requiere:

- subagentes/contextos realmente aislados;
- acceso al repositorio/evidencia relevante;
- estado durable/canónico;
- disponibilidad real de las skills requeridas/activas;
- idealmente control de reasoning/tools/capabilities por hijo.

Si no existen subagentes reales, puede funcionar en modo degradado, pero no debe afirmarse independencia multi-agente.

## Canonical entrypoint

`SKILL.md` es el router superior. Los contratos detallados viven en `references/` y los perfiles en `references/profiles/`.

El `default_prompt` de `agents/openai.yaml` es sólo bootstrap; no debe duplicar el sistema.

## Estado

**Experimental.**

El objetivo es que el usuario hable con un manager y no tenga que administrar manualmente una colección de prompts/agentes.