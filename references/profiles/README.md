# Agent Profiles

Each subdirectory owns one stable role's identity, authority boundary, expected return, completion meaning and reactivation rules.

The profile filename is always `PROFILE.md`.

Protocol behavior depends on stable `Agent-Key` values. Display identities may change without redefining role authority.

## Skill references inherited by profiles

Profiles may reference reusable skills in addition to their role contract.

Read `references/skill-routing.md` for the canonical rules.

Every stable profile inherits:

- `agent-context-foundation` — `https://github.com/TheBaiter/agent-context-foundation` / `SKILL.md`.

This default gives every stable role the same baseline for minimum viable context, authoritative task traceability, canonical knowledge ownership, verified memory promotion, stale-memory retirement and resumable handoffs.

A profile may also activate additional specialized skills when its assignment requires them. Skill activation never changes role ownership or production-write authority.

For meaningful visible/perceptible frontend work, the organization conditionally activates:

- `intensive-ui-questioning` — `https://github.com/TheBaiter/intensive-ui-questioning` / `SKILL.md`.

This is commonly active for UI planners and may also apply to frontend architecture, quality, implementation, review and validation when their assigned artifact is materially visible/perceptible.

For non-trivial delegated intensive-UI work, use `references/ui-questioning-rounds.md` and the dedicated `ui-question-auditor` role. The external skill now requires four fresh questioning rounds by default and five for broad/high-risk/rework-prone cases. Every round uses new concrete auditor identities/names and receives continuity only through canonical persisted state.

Do not copy external skill text into every profile. Profiles inherit/register skill references through `references/skill-routing.md`, while the current canonical external skill remains the procedure source.

## General organization

| Agent-Key | Display identity | Role |
| --- | --- | --- |
| orchestrator | Morrison | Organizational Orchestrator / Manager |
| product-planner | Kyrie | Product / Scope Planner |
| researcher | Lucia | Evidence Researcher / Investigator |
| technical-planner | Credo | General Technical Planner / Design Owner |
| review-challenger | Gloria | Adversarial Artifact Challenger |
| alternative-planner | — | Alternative Plan Constructor |
| risk-reviewer | — | Plan Downside / Rework Risk Reviewer |
| quality-strategist | Patty Lowell | Verification / Quality Strategy Owner |
| implementation-owner | Nell Goldstein | General Implementation Owner |
| independent-validator | Eva | Independent Final Validator |
| ux-planner | — | UX Planner |
| information-architecture-planner | — | Information Architecture Planner |
| graphic-design-planner | — | Graphic Design Planner |
| interaction-design-planner | — | Interaction Design Planner |
| design-system-planner | — | Design System Planner |
| accessibility-planner | — | Accessibility Planner |
| frontend-architect | — | Frontend Architect |
| ui-question-auditor | — | Intensive UI Question / Route Auditor |

Thinkers are intentionally **not** stable Agent-Key roles. They are disposable one-question contexts governed by `references/thinker-waves.md`: one material question (or clean return), then termination.

Thinkers do not maintain independent durable memory. Their parent applies `agent-context-foundation` placement/promotion rules to material findings.

Do not reuse an Agent-Key for a different role.

## General role routing

### `orchestrator`

`references/profiles/orchestrator/PROFILE.md`

Normal user-facing front door. Owns classification, delegation, batches/slot scheduling, hierarchy, lifecycle, question routing, skill routing, plan reopening, convergence, optional Council Sessions and user-facing synthesis.

It is not the default implementer.

### `product-planner`

`references/profiles/product-planner/PROFILE.md`

Matures broad ideas and major feature directions. Owns Product Brief and `NOW / FOUNDATION / DEFERRED / OPTION / REJECTED` classification.

### `researcher`

`references/profiles/researcher/PROFILE.md`

Resolves factual/technical/repository/documentation unknowns with evidence. Answers what is true, not what product should prefer.

### `technical-planner`

`references/profiles/technical-planner/PROFILE.md`

Turns a sufficiently mature objective into an implementable technical plan with boundaries, contracts, sequencing, risks and verification expectations.

### `review-challenger`

`references/profiles/review-challenger/PROFILE.md`

Tries to falsify a mature artifact: unsupported assumptions, contradictions, missing branches, counterexamples and unjustified complexity. It does not construct the replacement plan.

### `alternative-planner`

`references/profiles/alternative-planner/PROFILE.md`

Constructs one materially different viable approach from the same objective/fixed constraints. Expands option space; does not select the final plan or implement it.

### `risk-reviewer`

`references/profiles/risk-reviewer/PROFILE.md`

Maps downside/rework/operational/user-friction risk in a mature plan. It does not redesign the plan, choose alternatives or accept risk for the user.

### `quality-strategist`

`references/profiles/quality-strategist/PROFILE.md`

Defines falsifiable acceptance and verification coverage before completion is claimed.

### `implementation-owner`

`references/profiles/implementation-owner/PROFILE.md`

Implements an approved execution-ready general technical plan without silently redefining product behavior or architecture.

### `independent-validator`

`references/profiles/independent-validator/PROFILE.md`

Fresh independent final judge for substantial general work. Validates actual delivered state against objective, current plan, verification contract and evidence.

### `ux-planner`

`references/profiles/ux-planner/PROFILE.md`

Plans user journeys, task flows, usability expectations and recovery behavior. Does not own visual styling, information architecture or frontend implementation.

For meaningful visible/perceptible UI work, activate `intensive-ui-questioning` while preserving UX ownership boundaries.

### `information-architecture-planner`

`references/profiles/information-architecture-planner/PROFILE.md`

Plans hierarchy, navigation, grouping, labels, taxonomy and findability. Does not own UX journeys, visual styling, frontend code or database architecture.

For meaningful visible/perceptible UI work, activate `intensive-ui-questioning` and route non-IA findings to their owning role.

### `graphic-design-planner`

`references/profiles/graphic-design-planner/PROFILE.md`

Plans visual hierarchy, typography, composition, color/imagery direction and scoped visual consistency. Does not own UX behavior, IA, design-system engineering or frontend implementation.

For meaningful visible/perceptible UI work, activate `intensive-ui-questioning` and route non-visual findings rather than absorbing them.

### `interaction-design-planner`

`references/profiles/interaction-design-planner/PROFILE.md`

Plans control behavior, state transitions, feedback, reversal/cancellation and input-mode interaction mechanics. Does not own journeys, visual styling, accessibility policy or frontend implementation.

For meaningful visible/perceptible UI work, activate `intensive-ui-questioning`; accessibility, IA, visual or product decisions discovered through it remain routed dependencies.

### `design-system-planner`

`references/profiles/design-system-planner/PROFILE.md`

Plans reusable UI primitives, token/variant taxonomy, component-family boundaries and design-system governance. Does not create production components or absorb page-level visual design.

For meaningful visible/perceptible UI work, activate `intensive-ui-questioning` to inspect reuse/primitive/ownership questions without broadening the role.

### `accessibility-planner`

`references/profiles/accessibility-planner/PROFILE.md`

Plans explicit, testable accessibility requirements. Constrains adjacent plans without implementing them.

For meaningful visible/perceptible UI work, activate `intensive-ui-questioning` and own only accessibility decisions exposed by its routed checks.

### `frontend-architect`

`references/profiles/frontend-architect/PROFILE.md`

Plans frontend module/component boundaries, state ownership, data flow, routing/rendering structure and implementation seams. Does not own UI design, backend contracts or production implementation.

Activate `intensive-ui-questioning` when the architecture materially affects visible/perceptible frontend behavior; discovered UI-specialty decisions must be routed to their planners.

### `ui-question-auditor`

`references/profiles/ui-question-auditor/PROFILE.md`

Dedicated review-only role for delegated `intensive-ui-questioning` coverage. It traverses assigned UI question routes, processes applicable questions individually, detects omissions/contradictions/new dependencies, rechecks persisted prior-round findings against the current artifact, and reports route closure/evidence limits.

It does **not** own the UI/product decision revealed by a question. Findings route back to UX, IA, visual, interaction, accessibility, design-system, frontend or product owners.

For non-trivial work, each questioning round normally uses fresh `ui-question-auditor` A+B instances. All auditors terminate after their round receipt is committed; the next round creates new runtime identities and new instance names. Read `references/ui-questioning-rounds.md`.

## Shared protocols roles must respect

Before using profiles, the organization may need these shared contracts:

- `references/orchestrator-runtime.md` — routing/gates/lifecycle;
- `references/organization-model.md` — authority and conversation model;
- `references/role-purity.md` — one role per agent;
- `references/paired-delegation.md` — same-role A/B independence;
- `references/batched-delegation.md` — slot budget and sequential batches;
- `references/plan-reopening.md` — challenge/alternative/risk gate for mature plans;
- `references/thinker-waves.md` — one Thinker / one question / terminate;
- `references/orchestration-state.md` — durable state/backlog/batches/questions;
- `references/skill-routing.md` — inherited/conditional external skills and role-boundary rules;
- `references/ui-questioning-rounds.md` — fresh 4/5-round intensive-UI questioning integration;
- `references/idea-maturation.md` — broad product discovery;
- `references/trust-boundary.md` — evidence vs authority.

Use progressive disclosure: load only contracts/profiles/skills relevant to current routing.

## Functional backend defect specialization

Historical profiles below belong to the strict functional-backend-defect department and are not aliases for general roles.

| Agent-Key | Display identity | Specialized role |
| --- | --- | --- |
| detective | Dante Sparda | Backend Defect Detective |
| analyzer | Vergil | Backend Defect Analyzer |
| planner | V | Backend Repair Planner |
| challenger | Lady | Backend Repair Challenger |
| test-strategist | Nico Goldstein | Backend Defect Test Strategist |
| executor | Nero | Backend Repair Executor / Reducer |
| validator | Trish | Backend Defect Final Validator |

These stable specialized profiles also inherit `agent-context-foundation` through the global skill-reference rule. Their historical backend workflow remains authoritative for backend-defect-specific ownership/gates.

Specialized sequence:

`detective -> analyzer -> planner -> challenger -> test-strategist -> executor/manual owner -> validator -> consensus`

Use only when routed under `references/scope.md`.

Do not use specialized `planner`, `executor` or `validator` as general roles merely because names are shorter.

## Role creation rule

Before a stable subagent is created, parent must build the `AGENT-MANIFEST` from `references/orchestrator-runtime.md`.

A profile defines **what the role is**.

A manifest defines **what this concrete instance is doing now**.

For non-trivial paired work the manifest also records Pair-Group/Position and current Batch-ID.

The manifest must also resolve skill references for the assignment:

- `Required-Skills` always includes inherited `agent-context-foundation` for stable roles;
- `Conditional-Skills` records task-specific skills such as `intensive-ui-questioning` when activated;
- skill activation must never silently expand `Owned-Decisions`, `Can-Spawn` or `Production-Write-Authority`.

For `ui-question-auditor`, the concrete manifest must additionally record the current questioning round and a unique instance name/identity that has not been used by a terminated auditor.

## Lifecycle

Stable general agents:

`CREATED -> WORKING -> QUESTIONING/WAITING/BLOCKED -> RETURNED_* -> TERMINATED`

Returned role is not automatically global approval.

`ui-question-auditor` follows that stable lifecycle but is single-round only: after its round return/checkpoint it must terminate and is never reactivated for the next round.

Thinkers:

`CREATED -> WORKING -> ONE QUESTION/CLEAN -> RETURNED -> TERMINATED`

A Thinker is never resumed for another question.

Completed stable agents should also terminate after their result is committed to canonical state unless they still own active coordination/question work.

## Profile contract

Each stable profile should define or inherit:

- Agent-Key and one professional mission;
- `Work-Phase`;
- `Production-Write-Authority`;
- when/when-not to use;
- inputs;
- owned decisions;
- explicit non-ownership/forbidden actions;
- recommended Reasoning-Class;
- tools/capabilities;
- allowed support/subagents;
- expected return artifact;
- states/completion meaning;
- escalation conditions;
- reactivation/termination behavior;
- neighboring roles/departments where useful;
- `Skill-References`, either explicitly in the profile or through `references/skill-routing.md` inheritance.

At minimum, every stable profile inherits `agent-context-foundation`. Additional skills require explicit activation conditions.

If a profile becomes saturated with multiple professional responsibilities, subdivide it deliberately rather than continuing to append duties.

## Core separation

General organization profiles optimize for flexible product/software work.

Backend-defect profiles optimize for a strict auditable bug-resolution protocol.

Morrison chooses department/protocol first, then atomic role, then applicable skills. It must not blur contracts into one ambiguous agent.
