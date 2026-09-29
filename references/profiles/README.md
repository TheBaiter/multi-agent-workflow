# Agent Profiles

Each subdirectory owns one stable role's identity, authority boundary, expected return, completion meaning and reactivation rules.

`Agent-Key` values are protocol identifiers. Do not reuse an Agent-Key for a different profession and do not instantiate names that appear only as examples.

## Stable profile contract

Every stable profile must define or explicitly inherit:

- `Agent-Key` and one professional mission;
- `Work-Phase`;
- `Production-Write-Authority`;
- when to use / when not to use;
- inputs;
- owned decisions;
- explicit non-ownership / `Must-Not`;
- recommended `Reasoning-Class`;
- tools/capabilities;
- allowed support/subagent requests;
- expected return artifact;
- lifecycle/completion meaning;
- escalation conditions;
- reactivation/termination behavior;
- neighboring roles/department when useful;
- skill references through `references/installation-and-dependencies.md` and `references/skill-routing.md`.

If a profile accumulates multiple separable professions, subdivide it rather than appending more duties.

## Safe inherited defaults

To avoid duplicating boilerplate in every profile, the following defaults apply only when a profile does not override them.

### Skill baseline

Every stable profile requires `agent-context-foundation` for full-mode operation.

Meaningful visible/perceptible UI work conditionally activates `intensive-ui-questioning` according to `references/skill-routing.md`.

A profile/URL is not proof of availability; Morrison resolves actual dependency state before spawn.

### Lifecycle

Unless a profile defines a stricter lifecycle:

`CREATED -> WORKING -> QUESTIONING/WAITING/BLOCKED -> RETURNED_COMPLETE | RETURNED_INCONCLUSIVE | RETURNED_REJECTED -> TERMINATED`

`RETURNED_COMPLETE` means the bounded assignment returned successfully, not global project approval.

### Reactivation

Unless a profile explicitly requires continuity, a returned stable child should terminate after checkpointing. Material upstream changes create a **fresh instance** rather than keeping an old context alive as memory.

### Support permissions

For planning/design/research/review roles that do not declare `Can-Spawn`:

`Can-Spawn: THINKERS_ONLY`

Other specialist support is requested through Morrison/parent and does not transfer ownership.

Implementation/validation roles do **not** inherit direct spawn permission from this default; their own profile/manifest must state it.

### What cannot be inherited generically

The following must remain role-specific and cannot be guessed from defaults:

- mission/authority;
- use/not-use boundary;
- owned decisions;
- prohibited adjacent responsibilities;
- role-specific inputs;
- expected return artifact;
- completion semantics;
- material escalation conditions.

If those are missing, the profile is incomplete rather than safely inferable.

## General organization

| Agent-Key | Display identity | Stable role |
| --- | --- | --- |
| `orchestrator` | Morrison | Organizational Orchestrator / Manager |
| `product-planner` | Kyrie | Product / Scope Planner |
| `researcher` | Lucia | Evidence Researcher / Investigator |
| `technical-planner` | Credo | Cross-Department Technical Integration Planner |
| `review-challenger` | Gloria | Adversarial Artifact Challenger |
| `alternative-planner` | — | Alternative Plan Constructor |
| `risk-reviewer` | — | Plan Downside / Rework Risk Reviewer |
| `quality-strategist` | Patty Lowell | Verification / Quality Strategy Owner |
| `implementation-owner` | Nell Goldstein | General Implementation Owner |
| `independent-validator` | Eva | Independent Final Validator |
| `ux-planner` | — | UX Planner |
| `information-architecture-planner` | — | Information Architecture Planner |
| `graphic-design-planner` | — | Graphic Design Planner |
| `interaction-design-planner` | — | Interaction Design Planner |
| `design-system-planner` | — | Design System Planner |
| `accessibility-planner` | — | Accessibility Planner |
| `frontend-architect` | — | Frontend Architect |
| `backend-architect` | — | Backend Domain / Service Architect |
| `ui-question-auditor` | — | Intensive UI Question / Route Auditor |

Thinkers are intentionally **not** stable Agent-Keys. They are disposable one-question contexts governed by `references/thinker-waves.md`.

## General role routing

### `orchestrator`

`references/profiles/orchestrator/PROFILE.md`

User-facing manager. Owns classification, dependency preflight, department/role routing, pair/batch scheduling, state/lifecycle, escalation, gates, Council Sessions and synthesis. Not the default specialist or implementer.

### `product-planner`

`references/profiles/product-planner/PROFILE.md`

Owns product intent/scope/foundations and the Product Brief. Identifies specialist needs but does not design specialist architecture.

### `researcher`

`references/profiles/researcher/PROFILE.md`

Owns bounded evidence conclusions about current behavior/feasibility/compatibility. Does not own the downstream decision that consumes the evidence.

### `technical-planner`

`references/profiles/technical-planner/PROFILE.md`

**Cross-specialty technical integration only.** Reconciles dependencies, seams, compatibility, implementation ordering and rollout/rollback sequencing across already-mature specialist technical artifacts.

It is not a generic frontend/backend/API/data/security/performance architect. A single-domain technical task routes directly to its owning specialist; missing specialties become capability gaps.

The Agent-Key is retained for compatibility with older manifests, but older broad `TECHNICAL-PLAN` artifacts must be revalidated when they contain decisions now owned by specialist roles.

### `review-challenger`

`references/profiles/review-challenger/PROFILE.md`

Attempts to falsify a mature artifact. Does not construct the replacement plan or implement fixes.

### `alternative-planner`

`references/profiles/alternative-planner/PROFILE.md`

Constructs one materially different viable approach. Does not choose the winner or implement it.

### `risk-reviewer`

`references/profiles/risk-reviewer/PROFILE.md`

Maps downside/rework/operational/user-friction risk. Does not redesign or accept risk.

### `quality-strategist`

`references/profiles/quality-strategist/PROFILE.md`

Defines falsifiable verification strategy. Does not implement or issue the final independent verdict.

### `implementation-owner`

`references/profiles/implementation-owner/PROFILE.md`

Applies execution-ready approved work under bounded write ownership. Does not silently redefine product/design/architecture.

### `independent-validator`

`references/profiles/independent-validator/PROFILE.md`

Fresh final evaluator. Does not fix and then independently approve the corrected state in the same context.

## UI Planning Department

Router: `references/departments/ui-planning.md`

Atomic roles:

- `ux-planner` — journeys, task flows, usability/recovery expectations;
- `information-architecture-planner` — hierarchy, navigation, grouping, labels, taxonomy/findability;
- `graphic-design-planner` — visual hierarchy, typography, composition, color/imagery direction;
- `interaction-design-planner` — control behavior, transitions, feedback, reversal/cancellation/input modes;
- `design-system-planner` — reusable primitives, tokens/variants, component-family governance;
- `accessibility-planner` — explicit/testable accessibility requirements.

These roles do not absorb one another merely because they all affect UI.

## Frontend Planning Department

Router: `references/departments/frontend-planning.md`

### `frontend-architect`

`references/profiles/frontend-architect/PROFILE.md`

Owns frontend module/component boundaries, state ownership, data-flow/routing/rendering structure and implementation seams. Does not own UX/visual/IA/accessibility/backend/API/data or production implementation.

## Backend Planning Department

Router: `references/departments/backend-planning.md`

### `backend-architect`

`references/profiles/backend-architect/PROFILE.md`

Owns backend domain/service responsibility boundaries, workflows, invariants, transaction boundaries, concurrency/idempotency requirements, failure/recovery semantics and dependency direction.

It does **not** own public API/transport, persistence/data, authn/authz, security, observability, performance, implementation, QA or the historical defect workflow.

## Intensive UI audit role

### `ui-question-auditor`

`references/profiles/ui-question-auditor/PROFILE.md`

Review-only role for delegated `intensive-ui-questioning` route/question coverage. It owns audit coverage/evidence boundaries, not the product/design answer exposed by a question.

Each required round uses fresh instances; completed auditors terminate and are never reused for another round.

## Historical functional-backend-defect specialization

These Agent-Keys belong only to the strict historical functional-backend-defect workflow and are not aliases for general roles:

| Agent-Key | Display identity | Specialized role | Inherited Work-Phase | Production Write | Default Reasoning |
| --- | --- | --- | --- | --- | --- |
| `detective` | Dante Sparda | Backend Defect Detective | `DISCOVER` | `NO` | `DEEP` |
| `analyzer` | Vergil | Backend Defect Analyzer | `DISCOVER` | `NO` | `DEEP` |
| `planner` | V | Backend Repair Planner | `PLAN` | `NO` | `DEEP` |
| `challenger` | Lady | Backend Repair Challenger | `REVIEW` | `NO` | `DEEP` |
| `test-strategist` | Nico Goldstein | Backend Defect Test Strategist | `PLAN` | `NO` | `DEEP` |
| `executor` | Nero | Backend Repair Executor / Reducer | `IMPLEMENT` | `YES` | `STANDARD` |
| `validator` | Trish | Backend Defect Final Validator | `VERIFY` | `NO` | `DEEP` |

Compatibility envelope for these historical profiles:

- their existing specialized mission/scope/output/approval contracts remain authoritative;
- they inherit `agent-context-foundation` dependency handling through the global rule;
- their Work-Phase/write/reasoning values above apply when the legacy file omits them;
- their lifecycle follows the historical workflow plus the global rule that completed contexts are not kept alive merely as memory;
- their specialized cross-agent question/Issue/consensus rules remain under the historical contracts;
- this compatibility envelope must **not** be used to generalize them into the main organization.

Route them only through the historical scope/workflow contracts. Do not use `planner`, `executor` or `validator` as convenient general aliases.

## Role creation rule

Before spawning a stable child, build the concrete `AGENT-MANIFEST` from `references/orchestrator-runtime.md`.

A profile defines the profession. A manifest defines the bounded assignment of one concrete instance.

For paired work, record pair group/position/execution mode/start revision. Resolve required/conditional skills, actual dependency availability and `Context-Checkpoint-Target` before spawn.

A role mentioned in conceptual examples is **not usable** unless its stable profile exists and the router can discover it.

## Shared protocols

Load progressively as required:

- `references/orchestrator-runtime.md`;
- `references/organization-model.md`;
- `references/role-purity.md`;
- `references/paired-delegation.md`;
- `references/batched-delegation.md`;
- `references/plan-reopening.md`;
- `references/thinker-waves.md`;
- `references/orchestration-state.md`;
- `references/installation-and-dependencies.md`;
- `references/skill-routing.md`;
- `references/ui-questioning-rounds.md`;
- `references/idea-maturation.md`;
- `references/trust-boundary.md`.

## Core separation

**General roles optimize broad product/software organization. Historical backend-defect roles optimize a strict specialized bug-resolution protocol. Atomic ownership, not convenient naming, determines routing.**