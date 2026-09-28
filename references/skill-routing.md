# External Skill Routing

## Purpose

Agent profiles may depend on reusable external skills without copying those skills into this repository or widening the agent's professional role.

A **role** defines ownership and authority. A **skill** defines an applicable operating procedure or reference workflow. Loading a skill never grants new decision authority, never changes `Production-Write-Authority`, and never permits an agent to absorb a neighboring profession.

Morrison is responsible for attaching the correct skill references to each child manifest and for preserving progressive disclosure.

## Skill reference contract

Every stable agent manifest should expose:

```text
Required-Skills:
- <skill reference>

Conditional-Skills:
- Skill: <skill reference>
  Activate-When: <condition>
```

A skill reference should identify at minimum:

- stable skill name;
- canonical repository/source;
- canonical entrypoint;
- activation condition;
- whether the current agent must read it completely or only its routed subset;
- any role-boundary constraint.

Do not duplicate the external skill's full policy text into role profiles. Point to the canonical source.

## Default skill for the entire organization

### `agent-context-foundation`

Canonical source:

- Repository: `https://github.com/TheBaiter/agent-context-foundation`
- Entrypoint: `SKILL.md`

This skill is a **default required skill for every stable role**, including Morrison.

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

### Memory ownership rule

`agent-context-foundation` does **not** mean every child creates an independent memory system.

- Morrison owns organization-wide canonical orchestration state.
- Role owners may update the authoritative task/artifact they own.
- Stable specialists may propose or write durable role/project knowledge only when their assignment and repository authority allow it.
- Durable knowledge is promoted only after verification and is placed in one canonical owner.
- Child conversations are not durable memory.
- A completed child should checkpoint material findings before termination rather than remain alive as a memory store.

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
3. records/routs questions owned by another atomic role;
4. does not silently decide another role's specialty;
5. preserves one canonical owner for each decision.

Example: an `interaction-design-planner` may discover a keyboard/focus requirement while traversing the UI skill. It records and routes that requirement to `accessibility-planner`; discovery does not transfer ownership.

## Skill routing by task surface

Morrison should determine skill activation after classifying the task and before spawning the child.

```text
Task / artifact
   ↓
select atomic role
   ↓
inherit agent-context-foundation
   ↓
classify additional skill activations
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

A profile may declare additional specialized skills later. Those additions must state activation conditions and must not broaden the role's authority.

## Completion check

Before terminating a stable child, confirm:

- required skills were actually loaded/applied or explicitly blocked;
- applicable conditional skills were activated;
- skill-derived questions outside the role were routed rather than absorbed;
- material findings were persisted in the authoritative task/canonical artifact;
- verified reusable knowledge was promoted only to its canonical owner;
- stale or superseded memory was not left as competing truth;
- no child context is being retained merely as memory.

## Core principle

**Roles decide who owns the work. Skills decide how that owner should operate. Every stable role inherits `agent-context-foundation`; visible/perceptible UI work additionally routes through `intensive-ui-questioning` without breaking role purity.**