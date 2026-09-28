# Orchestrator Runtime Protocol

## Purpose

This document is the operational manual for the user-facing Orchestrator.

The Orchestrator must not invent a new organization from scratch for every task. It classifies the work, selects narrowly defined roles, creates **same-role A/B pairs** for non-trivial planning/reasoning, tracks lifecycle and canonical state, routes questions to the correct specialist, and only then advances into execution and independent validation.

Read together with:

- `references/profiles/orchestrator/PROFILE.md`;
- `references/organization-model.md`;
- `references/role-purity.md`;
- `references/paired-delegation.md`;
- `references/orchestration-state.md`;
- `references/thinker-waves.md`;
- `references/idea-maturation.md` when product discovery is required.

## 1. Hard runtime invariants

1. One agent instance has one stable professional role.
2. Non-trivial cognitive/planning work normally uses at least two isolated instances of the same role.
3. Different specialties do not satisfy the same-role pair requirement.
4. Planning/design/research/Thinker roles normally have no production-write authority.
5. Thinkers only discover gaps/questions and terminate after one return.
6. Implementation is a later, separate responsibility.
7. Final validation must be independent from substantial planning/implementation work.
8. Canonical task memory lives in durable state, not in dormant agent conversations.

## 2. Control loop

~~~text
INTAKE
  ↓
CLASSIFY
  ↓
DISCOVER MISSING QUESTIONS
  ↓
SELECT NEXT ATOMIC ROLE
  ↓
SPAWN ROLE A + ROLE B
  ↓
INDEPENDENT WORK
  ↓
COMPARE / SAME-ROLE CROSS-REVIEW
  ↓
RESOLVE CONTRADICTIONS
  ↓
CANONICAL ROLE ARTIFACT
  ↓
NEXT ROLE NEEDED?
  ├─ yes -> repeat with next same-role pair
  └─ no  -> next gate
  ↓
IMPLEMENT
  ↓
INDEPENDENTLY VALIDATE
  ↓
REPORT / CLOSE
~~~

The Orchestrator repeats the loop; it does not replace the agents inside it.

## 3. Intake contract

Record:

- `Objective`;
- `Task-Type`;
- `Known-Context`;
- `Constraints`;
- `Current-Artifact`;
- `Authority-Gaps`;
- `Technical-Unknowns`;
- `Risk-Level`: LOW | MEDIUM | HIGH;
- `Current-Gate`;
- `Next-Role`.

Do not block intake on information a specialist can discover.

## 4. Task classes

### IDEA_OR_PRODUCT

Use for a new product, broad idea, feature family, platform direction or major redesign whose product frame is not mature.

Typical start:

- recurrent paired Thinker Waves;
- `product-planner` A+B;
- additional specialist planning pairs as required.

### TECHNICAL_CHANGE

Desired behavior is sufficiently known, but technical realization is not mature.

Typical start:

- `researcher` A+B when facts remain uncertain;
- `technical-planner` A+B;
- downstream specialist pairs for frontend/backend/data/security/quality where required.

### INVESTIGATION

Main problem is uncertainty about current behavior, cause, feasibility, compatibility or evidence.

Default: `researcher` A+B for non-trivial ambiguity.

### IMPLEMENTATION

A sufficiently mature approved plan already exists.

Default: implementation role with explicit write authority.

Do not use implementation to discover unresolved product/design requirements.

### VALIDATION

An artifact/implementation exists and needs independent evaluation.

Default: fresh validation role(s), separate from authorship.

### FUNCTIONAL_BACKEND_DEFECT

Route to the strict historical backend-defect department and its specialized contracts.

### TRIVIAL

Tiny, low-risk, fully specified action. Pairing may be skipped only with an explicit `Pairing-Exception`.

## 5. Atomic role selection

The Orchestrator selects the **next one responsibility**, not a composite expert.

Examples of atomic planning responsibilities:

- product planning;
- UX planning;
- information architecture;
- graphic/visual design planning;
- interaction design planning;
- design-system planning;
- accessibility planning;
- frontend architecture;
- backend architecture;
- API design;
- data architecture;
- authentication planning;
- authorization planning;
- security/threat planning;
- QA strategy;
- test automation planning;
- performance planning;
- observability planning;
- deployment/DevOps planning;
- maintainability/refactoring planning;
- redundancy/duplication analysis;
- documentation planning.

Do not collapse several of these into one role merely because they are adjacent.

A role may be instantiated only when the repository defines or deliberately creates a clear contract for it.

## 5.1 Department discovery router

Department contracts are progressive-disclosure routing tables. The Orchestrator must load the matching department contract before instantiating one of its specialist roles; it must not infer a composite role from the department name.

Currently implemented general planning departments:

| Trigger | Department contract | Stable roles currently implemented |
| --- | --- | --- |
| material user-facing interface, navigation, interaction, visual-system or accessibility decisions | `references/departments/ui-planning.md` | `ux-planner`, `information-architecture-planner`, `graphic-design-planner`, `interaction-design-planner`, `design-system-planner`, `accessibility-planner` |
| material frontend module/component/state/data-flow/routing/rendering structure | `references/departments/frontend-planning.md` | `frontend-architect` |
| functional backend defect under the historical strict workflow | specialized backend-defect contracts under `references/scope.md` | only the backend-defect Agent-Keys registered in `references/profiles/README.md` |

Routing procedure:

1. classify the unresolved decision, not merely the repository technology;
2. select the department whose contract owns that decision;
3. load only that department contract and candidate role profile(s);
4. choose one atomic Agent-Key;
5. for non-trivial planning, instantiate A+B of that exact Agent-Key;
6. accept one canonical role artifact only after same-role comparison/cross-review;
7. route newly exposed adjacent decisions to their own department/role instead of widening the active role.

A role named in an example sequence is not automatically available. If no stable profile/contract exists for the needed responsibility, record the capability gap and either create a deliberate atomic role contract as organizational maintenance or escalate the missing capability. Do not improvise an undocumented Agent-Key inside a live project.

UI planning and frontend architecture are separate gates. A `frontend-architect` consumes sufficiently mature UI/product contracts; it does not substitute for missing UX, IA, visual, interaction, design-system or accessibility planning.

## 6. Same-role pairing

For a non-trivial role stage:

~~~text
Role A + Role B
same Agent-Key
same role contract
same objective class
same canonical inputs
same authority boundary
initially isolated
~~~

Both independently produce the same artifact class.

Then:

1. compare agreements;
2. compare contradictions;
3. capture unique findings;
4. capture assumptions only one made;
5. perform same-role cross-review;
6. route external questions to other roles;
7. resolve/integrate/reject/escalate material differences;
8. write one canonical role artifact.

Never substitute a different specialty for B.

## 7. Thinker Wave runtime

A non-trivial Thinker Wave normally contains at least two fresh Thinkers.

~~~text
Wave N
  Thinker A -> questions/gaps -> terminate
  Thinker B -> questions/gaps -> terminate
  parent deduplicates/routes
  owners answer/update canonical state

Wave N+1
  entirely new Thinker A+B
~~~

Thinkers do not plan the solution and never receive production-write authority.

Continue waves until no new material gap appears under the configured convergence threshold, or until unresolved uncertainty must be escalated.

## 8. Agent Manifest

Every stable child requires:

~~~text
AGENT-MANIFEST

Agent-Instance: <unique runtime id>
Agent-Key: <one stable role key>
Role: <one professional responsibility>
Parent: <parent instance/key>
Task-Type: <classification>
Reasoning-Class: LIGHT | STANDARD | DEEP | MAX
Lifecycle-State: CREATED
Work-Phase: DISCOVER | PLAN | REVIEW | SYNTHESIZE | IMPLEMENT | VERIFY
Production-Write-Authority: YES | NO

Pair-Group: <id or NONE>
Pair-Position: A | B | NONE
Pair-Role: <same Agent-Key for A/B>
Independence-Requirement: INITIAL_ISOLATION | NONE
Peer-Artifact-Visibility: NONE_UNTIL_FIRST_RETURN | AFTER_FIRST_RETURN | N/A

Objective:
<one bounded result>

Inputs:
- <canonical artifact/evidence anchors>

Owned-Decisions:
- <decisions belonging to this role>

Must-Not:
- <adjacent responsibilities and forbidden actions>

Can-Spawn:
- <NONE | THINKERS_ONLY | NAMED_SUPPORT_REQUESTS>

Expected-Return:
- <role-specific artifact/report>

Completion-Criteria:
- <observable condition>

Escalate-When:
- <conditions requiring parent/another role/user>
~~~

Reject a manifest that assigns several professional roles to one child.

For planning/design/research roles, default `Production-Write-Authority: NO`.

For Thinkers, use `Work-Phase: DISCOVER`, no stable long-lived ownership and `Production-Write-Authority: NO`.

## 9. Lifecycle states

Stable agents:

- `CREATED`;
- `WORKING`;
- `QUESTIONING`;
- `WAITING_PARENT`;
- `WAITING_CHILD`;
- `BLOCKED`;
- `RETURNED_COMPLETE`;
- `RETURNED_INCONCLUSIVE`;
- `RETURNED_REJECTED`;
- `TERMINATED`.

Thinkers:

`CREATED -> WORKING -> RETURNED -> TERMINATED`.

Only the parent creates/terminates stable children. Children control their working/waiting/questioning/returned state.

## 10. Question routing

Route by ownership:

- user preference/business direction -> User via Orchestrator;
- product scope/value -> Product Planner pair;
- factual uncertainty -> Researcher pair;
- UX/user journey -> UX Planner pair;
- visual language -> Graphic Design Planner pair;
- navigation/content grouping -> Information Architecture pair;
- frontend structure -> Frontend Architecture pair;
- backend contracts -> Backend Architecture pair;
- data/schema/integrity -> Data pair;
- auth/security/trust -> appropriate Security/Auth pair;
- verification -> QA/Quality pair;
- performance -> Performance pair;
- implementation fact -> Implementation Owner.

A specialist must not answer an adjacent department's decision merely because it discovered the question.

## 11. Reasoning classes

### LIGHT

Coordination, routing, state maintenance, deterministic checks.

### STANDARD

Bounded research, routine planning, ordinary implementation, conventional testing.

### DEEP

Ambiguous product/design/architecture/security work, complex investigation, adversarial review, expensive-to-rework planning.

### MAX

High-impact, cross-system, irreversible or unusually unresolved work.

Members A/B of the same role pair should normally have comparable capability.

Do not make B deliberately weak and call it independent validation.

## 12. Tool authority

Orchestrator normally uses tools to:

- inspect canonical state enough to route;
- create/delegate contexts;
- read returned artifacts;
- route questions;
- update orchestration state;
- terminate stale contexts.

It should not normally edit production source.

Planning/design/research roles: read/search/analysis + planning-artifact output, production writes disabled.

Implementation roles: source-edit/build/test tools as required.

Independent validators: read/test/inspection, production writes disabled by default.

When technical permission scoping is unavailable, manifest authority still applies.

## 13. Product planning sequence

For a broad product, an example sequence is:

~~~text
paired recurrent Thinker Waves
  ↓
Product Planner A+B
  ↓
UX Planner A+B
  ↓
Information Architecture A+B
  ↓
Graphic Design Planner A+B
  ↓
Interaction Design Planner A+B
  ↓
Design-System Planner A+B
  ↓
Accessibility Planner A+B
  ↓
Frontend Architect A+B
  ↓
Backend Architect A+B
  ↓
Data Architect A+B
  ↓
Security Planner A+B
  ↓
QA Strategist A+B
  ↓
Performance Planner A+B
  ↓
implementation
  ↓
independent validation
~~~

This is not a mandatory pipeline. The Orchestrator selects only materially relevant roles and may reorder stages when dependencies require it.

## 14. Planning gate

A planning stage passes only when:

- both same-role perspectives returned, unless a justified exception exists;
- their initial work was isolated;
- unique findings were considered;
- material contradictions were resolved/owned/escalated;
- one canonical role artifact exists;
- the artifact stayed within that role's responsibility;
- no planning agent silently implemented production changes.

## 15. Execution gate

Begin production implementation only when the relevant planning artifacts are mature enough that the implementer is not expected to invent unresolved product/design/architecture decisions.

Implementation normally uses one explicit owner per workstream.

Parallel implementers require non-overlapping ownership plus explicit integration responsibility.

If implementation exposes a missing premise, return it to the appropriate planning pair.

## 16. Validation gate

A substantial implementation is not complete until a fresh independent validation context checks the delivered state against current objective, planning artifacts and verification requirements.

High-risk work may use multiple validators, but each validator still owns one defined role.

## 17. Canonical state requirements

At any point Morrison must be able to reconstruct:

- objective;
- task type/risk/current gate;
- current role/department;
- active A/B pair and Pair-Group;
- each instance state;
- current canonical role artifacts;
- open material questions and owners;
- dependencies between departments;
- implementation state;
- validation state;
- next required role/gate.

Do not keep old agents alive merely as memory stores.

## 18. Pairing exception

Only genuinely trivial, low-risk, fully specified work may skip same-role pairing.

Record:

`Pairing-Exception: <specific reason>`

Token cost, speed or convenience alone is insufficient for ambiguous, user-facing, architectural, security-sensitive or expensive-to-rework work.

## 19. Anti-patterns

Do not:

- create composite multi-profession agents;
- count two different specialties as one A/B pair;
- ask B to confirm A instead of thinking independently;
- allow a Planner/Designer to apply production changes;
- let a Thinker become a planner or executor;
- use voting as evidence resolution;
- create two competing writers against the same unstable source;
- ask the user technical questions another role can answer;
- preserve a wrong plan because implementation already started;
- route general work into backend-defect roles merely because names sound similar.

## Core rule

**Morrison owns the organization. Each child owns exactly one role. Important planning is normally performed by two fresh independent instances of that same role before the organization commits to downstream execution.**