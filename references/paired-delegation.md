# Paired Delegation / Same-Role Dual-Perspective Protocol

## Purpose

A single capable subagent can still stop too early once it finds one plausible framing. For non-trivial reasoning and planning work, the organization therefore defaults to **at least two independent instances of the same role** before a material artifact is treated as mature.

This protocol is not a voting system and it is not permission to combine several professions inside one prompt.

Read `references/role-purity.md` with this protocol.

## Core rule

For every **non-trivial cognitive workstream**, the Orchestrator should normally create at least two isolated agents with the **same Agent-Key / same professional responsibility**.

Examples:

- `thinker-A` + `thinker-B`;
- `product-planner-A` + `product-planner-B`;
- `graphic-design-planner-A` + `graphic-design-planner-B`;
- `ux-planner-A` + `ux-planner-B`;
- `frontend-architect-A` + `frontend-architect-B`;
- `backend-architect-A` + `backend-architect-B`;
- `security-planner-A` + `security-planner-B`;
- `qa-strategist-A` + `qa-strategist-B`.

Two different specialties do **not** satisfy the same-role pair requirement. If the task needs UX and Graphic Design, create a UX pair and a Graphic Design pair as separate stages or branches.

## Planning before execution

The default paired pattern is for thinking, discovery, planning, design and review artifacts.

The pair should determine **how the work should be done**, not apply the work unless their stable role is explicitly an implementation role.

For example:

~~~text
Graphic Design Planner A ─┐
                          ├─ visual plan/specification
Graphic Design Planner B ─┘

later

Graphic/Frontend Implementer -> applies approved plan
~~~

Do not let a planning pair silently become production executors.

## Default pattern

~~~text
canonical objective + evidence
        ↓
   ┌─────────────┐
   │             │
Role A          Role B
same role       same role
isolated        isolated
plan            plan
   │             │
   └──────┬──────┘
          ↓
compare agreements / contradictions / omissions
          ↓
A reviews B's role-specific artifact
B reviews A's role-specific artifact
          ↓
resolve with evidence / escalation
          ↓
canonical role-specific synthesis
~~~

## Phase 1 — Independent construction

A and B receive:

- the same current objective;
- the same canonical state/evidence needed for that role;
- the same authority boundary;
- the same role contract;
- the same expected artifact class.

They must not see each other's draft or reasoning before their first return.

They may choose different approaches inside the same professional role.

## Phase 2 — Comparison

The parent records:

- agreements;
- contradictions;
- unique findings from A;
- unique findings from B;
- assumptions made by only one side;
- evidence needed to resolve disagreement;
- questions that belong to another specialist role or the user.

Do not resolve by majority vote.

## Phase 3 — Same-role cross-review

A receives B's material artifact and reviews it **only through the same role it already owns**.

B does the same against A.

Example: a Graphic Design Planner may critique visual hierarchy, typography, composition, visual consistency and related graphic-design decisions. It must not turn that review into UX research, backend planning, security analysis or code implementation.

## Phase 4 — Synthesis

The canonical role artifact is produced only after material disagreements are:

- resolved with evidence;
- incorporated;
- explicitly rejected with evidence by the owning role/authority; or
- escalated.

The Orchestrator may coordinate the synthesis but must not invent missing domain decisions. Unresolved specialist decisions go back to the same-role pair or to the appropriate new specialist pair.

## Recurrent Thinker loops

Thinkers are the first example of this protocol.

For non-trivial ideation/discovery:

~~~text
Thinker Wave 1
  -> Thinker A
  -> Thinker B
  -> merge material questions
  -> owners answer/update canonical state
  -> destroy both contexts

Thinker Wave 2
  -> new Thinker A
  -> new Thinker B
  -> repeat against updated state
~~~

Every wave uses fresh contexts. Continue until the configured convergence gate is met or unresolved material uncertainty requires escalation.

Thinkers only discover questions/gaps. They do not become planners or solution owners.

## Department sequencing

A complex project should normally move through **pairs of narrowly defined roles**, not one broad agent that tries to cover the whole department.

Example:

~~~text
IDEA
  ↓
Thinker A + Thinker B (fresh waves until useful convergence)
  ↓
Product Planner A + Product Planner B
  ↓
UX Planner A + UX Planner B
  ↓
Graphic Design Planner A + Graphic Design Planner B
  ↓
Information Architecture Planner A + B (when needed)
  ↓
Frontend Architecture Planner A + B
  ↓
Backend Architecture Planner A + B
  ↓
Security Planner A + B
  ↓
QA Strategy Planner A + B
  ↓
approved cross-department synthesis
  ↓
implementation roles
  ↓
independent validation roles
~~~

The exact departments depend on the task. Do not spawn unnecessary pairs merely as ritual.

## Execution rule

The two-perspective planning rule does **not** mean two implementers should edit the same unstable source in parallel.

Preferred execution pattern:

~~~text
mature paired plan
    ↓
Implementation Owner
    ↓
Independent Reviewer / Validator
~~~

Parallel implementers are permitted only when workstreams have explicit, non-overlapping ownership and integration responsibility is recorded.

## Agent manifest additions

For paired work, each instance records:

~~~text
Pair-Group: <stable group id>
Pair-Position: A | B
Pair-Role: <same Agent-Key for both members>
Independence-Requirement: INITIAL_ISOLATION
Peer-Artifact-Visibility: NONE_UNTIL_FIRST_RETURN | AFTER_FIRST_RETURN
Work-Phase: DISCOVER | PLAN | REVIEW | SYNTHESIZE | IMPLEMENT | VERIFY
Production-Write-Authority: YES | NO
~~~

For a valid planning pair:

- `Pair-Role` must match;
- `Work-Phase` should normally be `PLAN` (or `DISCOVER` for Thinkers);
- `Production-Write-Authority` should normally be `NO`.

## Orchestrator responsibilities

Before accepting a non-trivial role artifact, the Orchestrator must be able to answer:

- Who was role-instance A?
- Who was role-instance B?
- Did both have the same stable role?
- Did they form their initial plans independently?
- What did each uniquely identify?
- What did they disagree on?
- How was each material disagreement resolved?
- Is the resulting artifact still planning/specification, or did someone exceed authority and implement?

If A and B are different professions, the same-role pair requirement was not satisfied.

## Exceptions

The pair may be skipped only for genuinely trivial, low-risk, fully specified work where a second same-role perspective adds no material uncertainty reduction.

Record:

`Pairing-Exception: <reason>`

Token cost or impatience alone is not sufficient justification for ambiguous, architectural, user-facing, security-sensitive or expensive-to-rework work.

## Anti-patterns

Do not:

- use two different specialties as the required pair;
- define one agent with several roles to avoid creating the needed organization;
- give B the answer from A before B forms its own position;
- use the pair as a vote;
- let planning pairs apply production changes;
- let Thinkers become planners or implementers;
- make one "UI expert" simultaneously own UX, graphic design, accessibility, frontend architecture and validation;
- run two implementers against the same unstable files merely to satisfy a numeric rule;
- keep paired agents alive as memory stores after their assignment is complete.

## Design principle

**Important work should normally be planned by at least two independent instances of the same narrowly defined role before the organization commits to downstream execution.**

Coverage comes from many well-defined roles and departments. Independence comes from multiple isolated instances of each important role.