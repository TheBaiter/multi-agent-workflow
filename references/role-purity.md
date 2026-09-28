# Atomic Role / Single-Responsibility Agent Contract

## Purpose

Every agent instance in this organization must have **one role only**.

An agent may perform several steps that belong naturally to that role, but it must not combine distinct professional responsibilities merely to reduce the number of agents.

The organization should gain coverage by creating more bounded specialists, not by turning one subagent into a miniature full-stack organization.

## Core rule

**One agent instance = one Agent-Key + one professional role + one bounded assignment.**

Do not create composite identities such as:

- UX/UI/Graphic Designer;
- Frontend Architect + Accessibility Reviewer;
- Backend + Database + Security Planner;
- QA + Performance + Security Validator;
- Planner + Implementer + Final Validator.

If a task needs those responsibilities, create separate agent instances for the separate roles.

## Role versus task

A role answers **what responsibility this agent owns**.

A task answers **what this instance must produce right now**.

Example:

~~~text
Agent-Key: graphic-design-planner
Role: Graphic Design Planner
Task: define visual hierarchy, typography, color, imagery, composition and reusable visual rules for the authenticated dashboard
~~~

The task may be narrow or broad, but the role remains Graphic Design Planner.

## Planning and execution are different roles

Planning agents must not silently become executors.

If the organization needs to determine how something should be built, use a planning/design role whose output is an artifact, specification, decision set or plan.

If the organization later needs to apply that plan, create a separate implementation role.

Examples:

- `graphic-design-planner` plans visual direction; a later design-production role creates final assets when needed;
- `ux-planner` plans flows/interactions; a later frontend implementation role applies approved behavior;
- `frontend-architect` plans frontend boundaries/contracts; `frontend-implementer` writes frontend code;
- `backend-architect` plans backend contracts/data flow; `backend-implementer` writes backend code;
- `security-planner` defines controls/threat responses; a security implementation owner or relevant code owner applies them;
- `qa-strategist` defines verification; test automation/QA execution roles execute it.

A planning agent may inspect code/design artifacts and may write its own planning artifact, but it must not apply production changes unless its stable role explicitly is an implementation role.

## Review inside one role

Reviewing another agent's artifact does not automatically create a second professional role when the review stays strictly inside the same specialization.

Example:

Two `graphic-design-planner` instances may independently create visual plans and then critique each other's visual-plan decisions. They remain Graphic Design Planners because the review concerns the same responsibility they own.

What they may not do is expand that cross-review into unrelated UX research, backend architecture, security, QA, or implementation work.

## Pairing rule

For non-trivial planning/reasoning work, paired delegation should normally instantiate **at least two agents of the same role**.

Examples:

~~~text
thinker-A + thinker-B
product-planner-A + product-planner-B
graphic-design-planner-A + graphic-design-planner-B
ux-planner-A + ux-planner-B
frontend-architect-A + frontend-architect-B
backend-architect-A + backend-architect-B
security-planner-A + security-planner-B
qa-strategist-A + qa-strategist-B
performance-planner-A + performance-planner-B
~~~

Other specialties may participate later as separate role pairs or separate departmental stages. They do not substitute for the same-role pair.

## Department sequencing

A department can contain many specialist roles, but each role remains atomic.

Example UI/design department:

~~~text
UI / DESIGN DEPARTMENT
  -> UX Planner A + UX Planner B
  -> Information Architecture Planner A + B
  -> Graphic Design Planner A + B
  -> Interaction Design Planner A + B
  -> Design-System Planner A + B
  -> Accessibility Planner A + B
~~~

The Orchestrator should activate only the roles materially needed for the task.

Do not merge these responsibilities into one "UI expert" merely because all of them relate to interface work.

## Thinker distinction

A Thinker has exactly one role: discover missing questions, assumptions, branches and validation gaps.

A Thinker does not become:

- planner;
- designer;
- researcher;
- implementer;
- validator.

A thinker may phrase a discovered gap precisely, but the owning specialist role decides what to do about it.

## Synthesis

Synthesis is coordination of outputs, not permission to absorb specialist responsibilities.

The parent/Orchestrator may:

- compare two same-role artifacts;
- list agreements and contradictions;
- route contradictions back to the paired specialists;
- record the resolved canonical artifact.

It should not invent missing domain decisions itself when those decisions belong to the specialist pair.

For a highly technical or domain-heavy synthesis, use a dedicated synthesis owner whose single responsibility is to reconcile already-produced specialist artifacts without becoming their executor.

## Agent manifest requirement

Every stable `AGENT-MANIFEST` must include:

~~~text
Agent-Key: <one stable role>
Role: <one professional responsibility>
Assignment: <one bounded result>
Work-Phase: DISCOVER | PLAN | REVIEW | SYNTHESIZE | IMPLEMENT | VERIFY
Production-Write-Authority: YES | NO
~~~

`Work-Phase` narrows what the role is doing in this instance; it does not grant a second role.

For planning roles, `Production-Write-Authority` defaults to `NO`.

For Thinkers, `Work-Phase` is `DISCOVER` and `Production-Write-Authority` is always `NO`.

## Anti-patterns

Do not:

- define a role with `and`/`+` responsibilities that belong to separate professions merely for convenience;
- let a planner implement because it already knows the plan;
- let an implementer redefine product/design requirements because they seem incomplete;
- let a reviewer silently fix production code unless its stable role explicitly owns implementation;
- use one "general expert" where the organization actually requires several distinct specialist decisions;
- count two different specialties as the required same-role A/B pair;
- allow a Thinker to become the owner of the solution it questioned.

## Design principle

**Specialization should be represented by organizational structure, not compressed into individual prompts.**

The Orchestrator should know which single-responsibility roles to instantiate and should combine their artifacts at the organizational level.