# Agent Profiles

Each subdirectory owns one stable role's identity, operational personality, authority boundary, expected return, completion meaning, and reactivation rules.

The profile filename is always `PROFILE.md`.

Protocol behavior depends on stable `Agent-Key` values. Human-readable identities are display labels and may change without redefining role authority.

## General organization

These profiles are the default roles available to the Orchestrator for ordinary product/software work.

| Agent-Key | Display identity | Role |
| --- | --- | --- |
| orchestrator | Morrison | Organizational Orchestrator / Manager |
| product-planner | Kyrie | Product / Scope Planner |
| researcher | Lucia | Evidence Researcher / Investigator |
| technical-planner | Credo | General Technical Planner / Design Owner |
| review-challenger | Gloria | Adversarial Artifact Challenger |
| quality-strategist | Patty Lowell | Verification / Quality Strategy Owner |
| implementation-owner | Nell Goldstein | General Implementation Owner |
| independent-validator | Eva | Independent Final Validator |

Thinkers are intentionally **not** stable Agent-Key roles. They are disposable contexts governed by `references/thinker-waves.md` and terminate after one questioning delivery.

Do not reuse an Agent-Key for a different role.

## General role routing

### `orchestrator`

`references/profiles/orchestrator/PROFILE.md`

The normal user-facing front door. Owns task classification, delegation, hierarchy, capability/reasoning routing, lifecycle tracking, question routing, convergence and user-facing synthesis.

It is not the default implementer.

Read `references/orchestrator-runtime.md` with this profile.

### `product-planner`

`references/profiles/product-planner/PROFILE.md`

Matures broad ideas and major feature directions before detailed technical planning. Owns the Product Brief and `NOW / FOUNDATION / DEFERRED / OPTION / REJECTED` classification.

### `researcher`

`references/profiles/researcher/PROFILE.md`

Resolves factual/technical/repository/documentation unknowns with evidence. It answers what is true, not what the product should prefer.

### `technical-planner`

`references/profiles/technical-planner/PROFILE.md`

Turns a sufficiently mature objective into an implementable technical plan with boundaries, contracts, sequencing, risks and verification expectations.

### `review-challenger`

`references/profiles/review-challenger/PROFILE.md`

Independently attacks a mature artifact before downstream work relies on it. Has voice but does not become the artifact owner.

### `quality-strategist`

`references/profiles/quality-strategist/PROFILE.md`

Defines falsifiable acceptance and verification coverage before completion is claimed.

### `implementation-owner`

`references/profiles/implementation-owner/PROFILE.md`

Implements an approved general technical plan without silently redefining product behavior or architecture.

### `independent-validator`

`references/profiles/independent-validator/PROFILE.md`

Fresh independent final judge for substantial general work. Validates actual delivered state against objective, plan, verification contract and evidence.

## Functional backend defect specialization

The following historical profiles belong to the **strict functional-backend-defect department**. Their names may sound generic, but their actual contracts are intentionally backend-defect-specific.

| Agent-Key | Display identity | Specialized role |
| --- | --- | --- |
| detective | Dante Sparda | Backend Defect Detective |
| analyzer | Vergil | Backend Defect Analyzer |
| planner | V | Backend Repair Planner |
| challenger | Lady | Backend Repair Challenger |
| test-strategist | Nico Goldstein | Backend Defect Test Strategist |
| executor | Nero | Backend Repair Executor / Reducer |
| validator | Trish | Backend Defect Final Validator |

Specialized sequence:

`detective -> analyzer -> planner -> challenger -> test-strategist -> executor/manual owner -> validator -> consensus`

Use those profiles only when the task has been routed into the functional backend defect specialization under `references/scope.md`.

Do **not** use `planner` as the general technical planner, `executor` as the general implementation owner, or `validator` as the general final validator merely because their names are shorter. Their profiles carry stricter backend-repair assumptions, passes and Issue protocol.

## Role creation rule

Before a stable subagent is created, the parent must build the `AGENT-MANIFEST` defined in `references/orchestrator-runtime.md`.

A profile defines **what the role is**.

The manifest defines **what this concrete instance is doing now**.

Both are required for non-trivial delegated work.

The manifest supplies:

- parent;
- current objective;
- task classification;
- reasoning class;
- canonical inputs;
- owned decisions;
- forbidden actions;
- child-spawn permission;
- expected return;
- completion criteria;
- escalation conditions;
- reviewer freshness requirement.

## Lifecycle

Stable general agents use the organizational lifecycle in `references/orchestrator-runtime.md`:

`CREATED -> WORKING -> QUESTIONING/WAITING/BLOCKED -> RETURNED_* -> TERMINATED`

A returned role is not automatically global approval.

Thinkers use:

`CREATED -> WORKING -> RETURNED -> TERMINATED`

and must not be resumed for another questioning round.

## Editing a personality

When tuning one role:

- edit only that role's `PROFILE.md` unless a shared protocol truly changes;
- keep the primary responsibility narrow;
- preserve explicit forbidden actions;
- preserve organization authority boundaries;
- avoid turning it into a duplicate of another role;
- change display identity freely if desired, but change Agent-Key only as a deliberate protocol migration.

## Profile contract

Each profile should define:

- mission and primary objective;
- what it owns;
- what it does not own;
- recommended reasoning class;
- work/pass method when applicable;
- expected return artifact;
- explicit forbidden actions;
- completion/approval meaning;
- reactivation/termination behavior.

Shared organization, delegation, state, Issue, event, return, consensus, thinker and evidence rules belong in `references/`, not duplicated across every profile.

Canonical shared contracts include:

- `references/orchestrator-runtime.md`;
- `references/organization-model.md`;
- `references/idea-maturation.md`;
- `references/thinker-waves.md`;
- `references/workflow.md`;
- `references/issue-protocol.md`;
- `references/evidence-policy.md`;
- `references/trust-boundary.md`;
- `references/consensus.md`.

## Core separation

General organization profiles optimize for flexible product/software work.

Backend-defect profiles optimize for a strict auditable bug-resolution protocol.

The Orchestrator chooses the department first, then the role. It must not blur both contracts into one ambiguous agent.