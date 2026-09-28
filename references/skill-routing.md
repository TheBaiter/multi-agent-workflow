# External Skill Routing

## Purpose

Agent profiles may depend on reusable external skills without copying those skills into this repository or widening the agent's professional role.

A **role** defines ownership and authority. A **skill** defines an applicable operating procedure or reference workflow. Loading a skill never grants new decision authority, never changes `Production-Write-Authority`, and never permits an agent to absorb a neighboring profession.

Morrison is responsible for attaching the correct skill references to each child manifest and for preserving progressive disclosure.

## Skill reference contract

Every stable agent manifest must expose:

```text
Required-Skills:
- Skill: <skill name>
  Source: <canonical repository/entrypoint>
  Coverage: <FULL_ENTRYPOINT | ROUTED_SUBSET | assignment-specific rule>

Conditional-Skills:
- Skill: <skill name>
  Source: <canonical repository/entrypoint>
  Status: ACTIVE | NOT_ACTIVE | BLOCKED
  Activate-When: <condition>
  Coverage-Anchor: <receipt/artifact or NONE>

Context-Checkpoint-Target:
- <authoritative task / canonical artifact / repository context owner>
```

A skill reference identifies at minimum:

- stable skill name;
- canonical repository/source;
- canonical entrypoint;
- activation condition;
- whether the current agent must read it completely or only its routed subset;
- any role-boundary constraint.

Do not duplicate the external skill's full policy text into role profiles. Point to the canonical source.

## Mandatory spawn-time injection

Skill routing is part of agent creation, not optional metadata added after work begins.

Before Morrison spawns any stable child:

1. select the atomic role and bounded assignment;
2. resolve inherited required skills;
3. evaluate conditional skills against the actual task/artifact surface;
4. write `Required-Skills`, `Conditional-Skills` and `Context-Checkpoint-Target` into the concrete `AGENT-MANIFEST`;
5. ensure the child can access the current canonical skill source;
6. only then start the child.

If an older generic manifest template omits skill fields, this contract still requires Morrison to append them before spawn. The omission is a template gap, not permission to create a skill-less agent.

A child must not claim a required skill was applied merely because its profile or parent mentions the skill. The concrete assignment must resolve the current skill source and applicable coverage.

If a required skill source cannot be accessed, mark the assignment skill state `BLOCKED` or explicitly reduced according to the owning workflow. Do not reconstruct a required current procedure from memory.

## Default skill for the entire organization

### `agent-context-foundation`

Canonical source:

- Repository: `https://github.com/TheBaiter/agent-context-foundation`
- Entrypoint: `SKILL.md`

This skill is a **default required skill for every stable role**, including Morrison and every historical specialized backend-defect personality.

It establishes the repository-context and durable-memory discipline used by the organization:

- minimum viable context and progressive disclosure;
- one canonical owner for durable knowledge;
- authoritative task traceability for meaningful work;
- separation between active task history and reusable memory;
- evidence-based promotion: `discovered -> candidate -> verified -> durable`;
- compaction, supersession, retirement and removal of stale memory instead of append-only accumulation;
- preservation of exact source/test/owner/handoff anchors;
- issue/task-first handling for meaningful discovered defects when a tracker exists;
- fresh validation and resumable handoff state;
- no secrets/private customer data in reusable memory.

### Active context/memory duty

Every stable child actively manages context during its assignment; it does not merely read `agent-context-foundation` once.

At minimum it must:

1. use only the context needed for the current assignment;
2. keep active investigation/progress in the authoritative task rather than duplicating it into reusable memory;
3. preserve exact evidence, owner and handoff anchors needed by the next role/batch;
4. identify verified reusable findings separately from temporary hypotheses;
5. promote durable knowledge only when verified and place it under one canonical owner;
6. supersede/retire stale reusable knowledge instead of appending competing truth;
7. checkpoint material decisions/findings before returning;
8. terminate after handoff rather than remain alive as a memory store.

`Context-Checkpoint-Target` tells the child where assignment state must be persisted. Morrison must provide it whenever meaningful work is delegated.

### Memory ownership rule

`agent-context-foundation` does **not** mean every child creates an independent memory system.

- Morrison owns organization-wide canonical orchestration state.
- Role owners may update the authoritative task/artifact they own.
- Stable specialists may propose or write durable role/project knowledge only when their assignment and repository authority allow it.
- Durable knowledge is promoted only after verification and is placed in one canonical owner.
- Child conversations are not durable memory.
- A completed child must checkpoint material findings before termination rather than remain alive as a memory store.

Disposable Thinkers are not stable personalities. They receive the minimum canonical context needed to ask one question, return it, and terminate. Their parent decides whether a finding becomes a task question, evidence, candidate memory, or nothing. Thinkers must not maintain durable memory themselves.

### Freshness rule

Agents must consult the current canonical skill source when the skill applies. Prior familiarity or a remembered summary is not proof that the current procedure was followed.

## UI / perceptible-work skill

### `intensive-ui-questioning`

Canonical source:

- Repository: `https://github.com/TheBaiter/intensive-ui-questioning`
- Entrypoint: `SKILL.md`

Activate this skill for meaningful **visible or perceptible frontend/UI work**.

It is an operating procedure for questioning and validating UI work before implementation/review, including outcome, user job, removal/reuse, ownership, pattern identity, state lifecycle, redundancy, responsiveness, accessibility, feedback, provenance/modes, visual evidence and routed specialized question packs.

When activated, treat it as a live procedure, not remembered advice. Follow its entrypoint/router and every activated owner/pack to route closure using progressive disclosure.

### Roles that commonly activate it

The skill is normally required when these roles are assigned visible/perceptible UI work:

- `ux-planner`;
- `information-architecture-planner`;
- `graphic-design-planner`;
- `interaction-design-planner`;
- `design-system-planner`;
- `accessibility-planner`;
- `frontend-architect` when architecture materially affects visible/perceptible UI behavior;
- `quality-strategist` when defining UI verification;
- `implementation-owner` when implementing visible/perceptible frontend changes;
- `independent-validator` when validating visible/perceptible frontend changes;
- `review-challenger`, `alternative-planner`, or `risk-reviewer` when their assigned artifact is materially UI-facing.

Do not activate it for purely backend/data work with no visible/perceptible consequence.

### Role-purity interaction

`intensive-ui-questioning` contains many question domains. Activating it does **not** turn one role into all UI professions.

Each agent:

1. uses the skill to inspect the full applicable route;
2. answers checks that fall within its owned decisions/evidence;
3. records/routes questions owned by another atomic role;
4. does not silently decide another role's specialty;
5. preserves one canonical owner for each decision.

Example: an `interaction-design-planner` may discover a keyboard/focus requirement while traversing the UI skill. It records and routes that requirement to `accessibility-planner`; discovery does not transfer ownership.

## Skill routing by task surface

Morrison determines skill activation after classifying the task and before spawning the child.

```text
Task / artifact
   ↓
select atomic role
   ↓
inherit agent-context-foundation
   ↓
classify additional skill activations
   ↓
resolve Context-Checkpoint-Target
   ↓
build AGENT-MANIFEST with skill references
   ↓
spawn child
```

Skills may also become active later when evidence changes task shape. When that occurs, update the manifest/task state and re-run only affected work as needed.

## Conflict and authority rules

External skills supplement the organization but do not outrank higher authority.

They must not silently change:

- user objective;
- role ownership;
- same-role pairing requirements;
- production-write authority;
- department routing;
- required validation gates;
- user-vs-agent decision authority.

If an external skill exposes a required decision outside the current role, route the decision. If an external skill conflicts with project-specific active instructions or higher-priority authority, record the conflict and escalate to Morrison rather than improvising.

## Profile reference model

Profiles do not need to duplicate every inherited skill. The canonical inheritance rule is:

```text
ALL STABLE PROFILES
  -> REQUIRED: agent-context-foundation

VISIBLE/PERCEPTIBLE UI ASSIGNMENT
  -> CONDITIONAL/ACTIVE: intensive-ui-questioning
```

Profiles with strongly recurring specialized skill use should include a compact `Skill references` section pointing here, as the UI profiles do. The shared skill body remains canonical here/external; do not paste complete external procedures into every personality.

A profile may declare additional specialized skills later. Those additions must state activation conditions and must not broaden the role's authority.

## Completion check

Before terminating a stable child, confirm:

- required skills were actually loaded/applied or explicitly blocked;
- applicable conditional skills were activated;
- skill-derived questions outside the role were routed rather than absorbed;
- material findings were persisted in the authoritative task/canonical artifact named by `Context-Checkpoint-Target`;
- verified reusable knowledge was promoted only to its canonical owner;
- temporary task history was not copied into reusable memory;
- stale or superseded memory was retired or superseded instead of left as competing truth;
- exact source/test/owner/handoff anchors required by the next role were preserved;
- no child context is being retained merely as memory.

## Core principle

**Roles decide who owns the work. Skills decide how that owner should operate. Every stable role inherits `agent-context-foundation`; visible/perceptible UI work additionally routes through `intensive-ui-questioning` without breaking role purity. Every completed child checkpoints material state before it dies.**