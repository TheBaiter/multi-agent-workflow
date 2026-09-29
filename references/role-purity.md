# Atomic Role / Single-Responsibility Agent Contract

## Purpose

Every stable agent instance has **one professional role only**.

An agent may perform several steps that naturally belong to that profession, but it must not combine distinct professional responsibilities merely to reduce agent count.

## Core rule

**One stable agent instance = one Agent-Key + one professional responsibility + one bounded assignment.**

Do not create composite identities such as:

- UX + visual + accessibility + frontend;
- frontend architect + implementer + reviewer;
- backend + database + security;
- performance + observability + optimization;
- planner + implementer + final validator.

If several responsibilities are material, route them to separate roles/owners.

## Stable role versus assignment

A role answers **what profession/authority this agent owns**.

An assignment answers **what bounded result this concrete instance must return now**.

Example:

```text
Agent-Key: graphic-design-planner
Role: Graphic Design Planner
Assignment: define the visual hierarchy and composition plan for the authenticated dashboard
```

The assignment can narrow the scope; it cannot widen the profession.

## Only contracted Agent-Keys are instantiable

Conceptual examples may mention future specialties such as API planning, data architecture, security planning, performance planning or domain-specific implementation.

Those labels are **capabilities, not automatically valid Agent-Keys**.

Morrison may instantiate a role only when:

1. a stable profile/contract exists;
2. its authority boundary is defined;
3. the router/department can discover it;
4. the concrete manifest preserves that boundary.

If a needed specialty lacks a stable contract, record a capability gap. Do not invent the Agent-Key inside a live task.

## Planning, implementation and validation are different responsibilities

Planning/design agents produce plans/specifications/decisions/artifacts. They do not silently become production writers.

Implementation belongs to explicit implementation ownership.

Final validation belongs to a fresh independent validation role.

Examples using **currently contracted general roles**:

- `graphic-design-planner` defines visual direction; an explicit implementation owner later applies approved production changes;
- `ux-planner` defines user flows/usability requirements; it does not implement frontend code;
- `frontend-architect` defines frontend structure; it does not own production implementation;
- `backend-architect` defines backend domain/service architecture; it does not own public API/data/security or production implementation;
- `technical-planner` integrates already-owned specialist plans; it does not replace those specialists;
- `quality-strategist` defines verification strategy; it does not act as the final validator;
- `implementation-owner` implements execution-ready work; it does not validate its own substantial work as final judge;
- `independent-validator` validates and normally has no production-write authority.

A future specialized implementation role may be added deliberately, but its name is not valid merely because an example would be convenient.

## Review inside one profession

Reviewing another instance's artifact does not create a second profession when the review remains strictly inside the same specialization.

Example: two `graphic-design-planner` instances may independently create visual plans and then critique each other's visual decisions. They remain Graphic Design Planners.

They may not turn that cross-review into UX research, backend planning, security analysis, QA ownership or implementation.

## Same-role pairing

For non-trivial cognitive/planning/review work, normally create at least two fresh independent instances of the **same contracted Agent-Key**.

Valid current examples include:

```text
product-planner-A + product-planner-B
researcher-A + researcher-B
ux-planner-A + ux-planner-B
graphic-design-planner-A + graphic-design-planner-B
frontend-architect-A + frontend-architect-B
backend-architect-A + backend-architect-B
technical-planner-A + technical-planner-B
review-challenger-A + review-challenger-B
alternative-planner-A + alternative-planner-B
risk-reviewer-A + risk-reviewer-B
quality-strategist-A + quality-strategist-B
```

Thinkers follow their own disposable one-question contract rather than stable Agent-Key profiles.

Different specialties never satisfy one another's pair requirement.

## Department sequencing

A department may contain many professions, but each profile remains atomic.

Example UI planning sequence when all are materially required:

```text
UX Planner A+B
Information Architecture Planner A+B
Graphic Design Planner A+B
Interaction Design Planner A+B
Design-System Planner A+B
Accessibility Planner A+B
```

This is not a mandatory ritual. Activate only responsibilities that materially affect the task.

## Technical integration is not generic architecture

`technical-planner` is intentionally narrowed to cross-specialty integration.

It may reconcile:

- dependencies;
- compatibility;
- handoffs;
- implementation order;
- rollout/rollback order;
- contradictions that must be routed back to premise owners.

It may not absorb frontend/backend/API/data/security/performance architecture to avoid creating/routing the correct specialist.

## Thinker distinction

A Thinker has one responsibility only: return one strongest material unanswered question (or clean) and terminate.

A Thinker does not become planner, designer, researcher, implementer or validator.

The owning stable role decides what to do with the question.

## Synthesis

Synthesis coordinates already-owned outputs. It does not transfer domain authority to the synthesizer.

Morrison may compare artifacts, route contradictions and record resolved canonical state.

`technical-planner` may integrate mature specialist technical artifacts when cross-specialty sequencing/compatibility is itself the assigned profession.

Neither may invent missing specialist decisions.

## Manifest requirement

Every stable manifest includes at minimum:

```text
Agent-Key: <one contracted stable role>
Role: <one professional responsibility>
Assignment: <one bounded result>
Work-Phase: DISCOVER | PLAN | REVIEW | SYNTHESIZE | IMPLEMENT | VERIFY
Production-Write-Authority: YES | NO
```

It also preserves role-specific authority, tools, skill dependencies, batch/pair state and escalation rules under `references/orchestrator-runtime.md`.

For planning/design/research/review roles, production writes default to `NO`.

## Saturation test

Treat a role as a candidate for subdivision when it materially:

- owns multiple separable professions;
- produces artifacts that need independent owners;
- requires very different knowledge/tools/reasoning modes;
- mixes conflicting completion criteria;
- accumulates adjacent responsibilities through repeated `also`/`when applicable` clauses;
- needs excessive context from unrelated domains;
- can no longer go deep on its primary responsibility.

Refactor ownership rather than making the prompt larger.

## Anti-patterns

Do not:

- define a stable role as a bundle of neighboring professions;
- let a planner implement because it already knows the plan;
- let an implementer invent unresolved product/design/architecture;
- let a reviewer silently become a production fixer;
- use one generic expert when several independent decisions exist;
- count two different specialties as an A+B pair;
- let Thinkers own their solutions;
- instantiate uncontracted names from examples;
- solve a capability gap by widening the nearest existing role.

## Core principle

**Specialization belongs in organizational structure, not inside oversized prompts.**