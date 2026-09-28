# Plan Reopening / Alternative Challenge Protocol

## Purpose

A coherent plan can still be mediocre because its authors converged too early around the first plausible frame.

This protocol prevents `PLAN COMPLETE` from meaning `STOP THINKING`.

Before expensive implementation, a substantial mature plan should normally be **reopened deliberately** by fresh roles that did not author it and that have distinct review responsibilities.

The goal is not endless redesign. The goal is to discover better alternatives, hidden user friction, unsupported assumptions, avoidable future rework and failure modes while change is still cheap.

## Maturity states

Use these conceptual states:

- `DRAFT`: still being authored;
- `MATURE`: primary planning pair believes the artifact is coherent;
- `REOPENING`: fresh review/alternative work is active;
- `REVISED`: owner incorporated material reopening findings;
- `EXECUTION_READY`: reopening gate passed and unresolved material issues are owned/escalated;
- `STALE`: an upstream premise changed.

`MATURE` is not automatically `EXECUTION_READY`.

## Reopening trigger

Reopen a plan when one or more apply:

- user-facing flow or design is expensive to redo;
- architecture/data/security decisions have broad blast radius;
- the plan has already gone through material revisions;
- the first implementation would establish a long-lived foundation;
- the plan depends on several assumptions;
- prior work on the project has required avoidable redesign/rework;
- the Orchestrator detects strong convergence around one frame with little alternative exploration.

Tiny, fully specified, low-risk work may skip reopening with an explicit reason.

## Default reopening sequence

The roles are distinct and must not be collapsed into one broad reviewer.

~~~text
MATURE PLAN
   ↓
fresh one-question Thinkers
   ↓
Review Challenger A+B
   ↓
Alternative Planner A+B
   ↓
Risk Reviewer A+B when material
   ↓
route findings to premise owners
   ↓
plan owner revises / defends with evidence
   ↓
fresh targeted Thinker question(s) when needed
   ↓
EXECUTION_READY or BLOCKED/USER_DECISION
~~~

Use `references/batched-delegation.md` to execute these stages in chunks when agent slots are limited.

## 1. Fresh Thinker questions

Each Thinker instance returns exactly **one strongest material question** and terminates.

Use multiple fresh instances/waves to explore more branches. Do not ask one Thinker for a long checklist.

Useful lenses include:

- what would make this flow feel unnatural to a normal user?;
- what obvious adjacent need will force rework immediately after launch?;
- what assumption exists only because the current plan chose one frame early?;
- what step, state or recovery path is missing?;
- what part could be simpler?;
- what future foundation is accidentally blocked?;
- what evidence would make us choose a different plan?;
- what are we not considering because the artifact already looks complete?.

Thinkers only expose questions. They do not redesign the plan.

## 2. Review Challenger

Use existing `review-challenger` A+B.

Its job is falsification:

- attack unsupported assumptions;
- find contradictions;
- produce counterexamples;
- identify omitted branches;
- challenge unjustified complexity;
- show where the plan would fail its stated objective.

It does **not** own a replacement plan.

## 3. Alternative Planner

Use `alternative-planner` A+B.

Its job is constructive divergence: independently derive a materially different viable approach from the same objective and fixed constraints.

The role must be allowed to conclude `NO_MATERIAL_BETTER_ALTERNATIVE` when divergence would merely be stylistic.

The role does not select the winning plan. It exposes an alternative so the owning planner/authority can compare trade-offs with evidence.

## 4. Risk Reviewer

Use `risk-reviewer` A+B when downside/rework exposure is material.

Its job is not to prove the plan wrong or design a replacement. It maps:

- likely rework triggers;
- irreversible or expensive commitments;
- operational/user adoption friction;
- dependencies that can fail late;
- maintenance burden;
- rollout/recovery risk;
- failure scenarios where the plan remains technically correct but practically costly.

## Comparison record

The Orchestrator or delegated plan owner should maintain:

~~~text
PLAN-REOPENING

Artifact: <anchor>
Started-From: <revision>
Thinker-Questions: <question ids>
Challenge-Pair: <pair id/status>
Alternative-Pair: <pair id/status>
Risk-Pair: <pair id/status or NOT_REQUIRED>
Material-Findings: <ids/anchors>
Alternative-Approaches: <anchors>
Decisions-Reopened: <ids>
Decisions-Preserved: <ids + evidence>
Plan-Revision: <new anchor/status>
Remaining-Questions: <ids>
Disposition: EXECUTION_READY | REVISE_AGAIN | USER_DECISION | BLOCKED
~~~

## Owner response

The original plan owner may defend the existing approach, but every material reopening finding must be one of:

- `INCORPORATED`;
- `REJECTED_WITH_EVIDENCE`;
- `DEFERRED_WITH_OWNER`;
- `ROUTED_TO_ANOTHER_ROLE`;
- `ESCALATED_TO_USER`.

`WE_ALREADY_PLANNED_THIS` is not a disposition.

## User-facing collaborative council

The user normally speaks only with the Orchestrator, but may explicitly ask to discuss a plan with selected specialists.

When supported by the host, Morrison may open a temporary **Council Session** containing the relevant specialist instances.

Rules:

- Morrison remains chair and organizational authority;
- every specialist speaks only from its one role;
- the user may question or challenge individual specialists;
- specialists may disagree openly;
- disagreement still resolves through evidence/authority, not voting;
- decisions are written back to canonical state;
- the council ends when its purpose is resolved and unneeded specialist contexts terminate.

If the host cannot expose multiple live subagents directly in one conversational surface, Morrison must relay clearly labeled specialist artifacts/questions instead of pretending direct multi-agent conversation occurred.

Council mode is optional. It does not replace normal delegation-first operation.

## Convergence

A reopened plan may become `EXECUTION_READY` when:

- material one-question Thinker findings are resolved/routed;
- required Challenger pair completed;
- required Alternative Planner pair completed;
- Risk Reviewer completed when warranted;
- all material findings have explicit dispositions;
- the canonical plan was revised or defended with evidence;
- no unresolved issue would materially change implementation without an identified owner/escalation;
- a fresh final targeted question pass produces no new material reason to reopen again.

For high-risk work, the Orchestrator may require more than one clean fresh question pass.

## Anti-patterns

Do not:

- treat a first mature draft as execution-ready by default;
- ask the original planner to be its only challenger;
- merge challenger, alternative planner and risk reviewer into one overloaded role;
- require alternatives merely for cosmetic novelty;
- keep reopening after no material new information appears;
- use majority vote to select a plan;
- let alternative exploration silently expand user-approved scope;
- expose specialists to the user without preserving Morrison as chair/authority;
- keep council participants alive as durable memory.

## Design principle

**A good plan should survive both attempts to break it and serious attempts to replace it before expensive execution begins.**