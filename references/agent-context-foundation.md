# Integration with agent-context-foundation

## Purpose

`multi-agent-workflow` uses **`agent-context-foundation`** as its baseline context/memory discipline for every stable role.

Canonical companion project:

`https://github.com/TheBaiter/agent-context-foundation`

Canonical skill name:

`agent-context-foundation`

This reference explains the responsibility boundary between the two skills. Runtime availability and installation semantics are owned by `references/installation-and-dependencies.md`; skill activation/injection semantics are owned by `references/skill-routing.md`.

## Current organizational scope

`multi-agent-workflow` is a **general manager-led multi-agent organization**, not only a functional-backend-defect workflow.

Morrison/Orchestrator may route work through product, research, UI, frontend, backend, plan-reopening, implementation, verification and validation roles/departments according to the task.

The historical functional-backend-defect workflow remains a specialized department inside the larger organization and keeps its own Agent-Keys/protocols.

## Canonical ownership

Use progressive disclosure and one canonical owner for each kind of durable knowledge:

- `SKILL.md` -> top-level entrypoint/router;
- `references/profiles/<agent-key>/PROFILE.md` -> canonical owner of each stable role's mission, authority, limits and return contract;
- `references/orchestrator-runtime.md` -> operational routing/gates/lifecycle;
- `references/orchestration-state.md` -> canonical organization state, dependencies, batches, pairs, backlog, questions and active gates;
- `references/skill-routing.md` -> external skill routing and role-boundary interaction;
- `references/installation-and-dependencies.md` -> actual dependency availability/install mode;
- `references/departments/*` -> department-level progressive-disclosure routing;
- authoritative task/Issue/project state -> current chronology and active execution decisions;
- source/config/schema/migrations -> implementation truth;
- repository durable context managed under `agent-context-foundation` -> only verified reusable knowledge.

Do not make `SKILL.md`, child conversations or private agent notes competing sources of truth.

## Responsibility boundary

### `agent-context-foundation` owns

Repository/project context discipline such as:

- minimum viable context;
- progressive disclosure;
- canonical durable knowledge ownership;
- task traceability foundations;
- verified knowledge promotion;
- stale/superseded memory retirement;
- resumable handoff state;
- exact source/test/owner anchors;
- issue/task-first handling of meaningful discovered defects when a tracker exists;
- durable repository planning/context conventions.

### `multi-agent-workflow` owns

Organization and execution coordination such as:

- Morrison as user-facing manager;
- task/authority/risk classification;
- department and atomic-role routing;
- same-role A+B pairing;
- batched delegation under runtime slot limits;
- one-question disposable Thinkers;
- plan reopening via challengers/alternatives/risk review;
- implementation ownership;
- independent validation;
- question escalation;
- Council Sessions;
- organizational backlog and gates;
- the specialized historical functional-backend-defect department.

`agent-context-foundation` does not turn a specialist into another profession. `multi-agent-workflow` does not redefine the context/memory rules owned by the companion skill.

## Active memory/context duty

When `agent-context-foundation` is `AVAILABLE`, every stable role must actively apply it during the assignment rather than treating it as background reading.

At minimum:

1. load only context needed for the bounded assignment;
2. keep active chronology in the authoritative task/state;
3. preserve exact evidence/owner/handoff anchors needed downstream;
4. distinguish hypotheses from verified reusable findings;
5. promote durable knowledge only after verification;
6. place promoted knowledge under one canonical owner;
7. retire/supersede stale reusable knowledge instead of appending competing truth;
8. checkpoint material findings before returning/termination.

A completed child must not remain alive merely as a memory store.

## Thinker boundary

Disposable Thinkers are not stable personalities and do not maintain durable memory.

They receive the minimum current canonical context needed to ask exactly one material question (or return clean), then terminate.

Their parent/Morrison decides whether the returned finding becomes:

- an open task question;
- evidence;
- a candidate reusable lesson;
- or nothing.

Only verified reusable conclusions may later be promoted under `agent-context-foundation`.

## Historical backend-defect department

When Morrison routes a task to the strict functional-backend-defect department, its specialized Issue/state/evidence/consensus contracts still apply.

That department is **one specialization**, not the scope definition of the whole `multi-agent-workflow` skill.

Do not reuse its short Agent-Keys (`planner`, `executor`, `validator`, etc.) as aliases for general organization roles.

## Missing dependency

If `agent-context-foundation` is unavailable, follow `references/installation-and-dependencies.md`:

- do not claim its guarantees were applied;
- mark the organization/path `REDUCED` or `BLOCKED` according to risk;
- preserve ordinary canonical task state where possible;
- never reconstruct the current external procedure from memory and present it as equivalent.

## Core principle

**`agent-context-foundation` owns how durable context stays trustworthy; `multi-agent-workflow` owns how specialized agents are organized around that trustworthy context.**