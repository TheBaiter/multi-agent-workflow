# Paired Delegation / Dual-Perspective Protocol

## Purpose

A single capable subagent can still stop too early once it finds one plausible framing. For non-trivial reasoning, product, design, planning, investigation, review, or validation work, the organization should therefore default to **at least two independent perspectives** before a material artifact is treated as mature.

This protocol is not about duplicating work mechanically. It exists to force independent framing, disagreement discovery, cross-review, and evidence-backed synthesis before expensive downstream work begins.

## Core rule

For every **non-trivial cognitive workstream**, the Orchestrator should normally create at least two isolated participating contexts.

Examples:

- two Product/Scope perspectives before a Product Brief is mature;
- two technical planning perspectives before an expensive architecture/change plan is accepted;
- two UI/UX perspectives before a major interface direction is frozen;
- two security/reliability perspectives for high-impact design;
- two independent investigation paths when cause or feasibility is ambiguous;
- at least one independent review context in addition to the author of a substantial artifact.

The two perspectives must be capable of disagreeing.

A second agent that merely receives the first agent's conclusion and is asked to approve it does not satisfy this rule.

## Default pattern: Independent A/B -> Cross-review -> Synthesis

Use this pattern for planning, product discovery, architecture, UX/UI, security, QA strategy, performance strategy, and other work where an early framing can create substantial rework.

~~~text
canonical objective + evidence
        ↓
   ┌─────────────┐
   │             │
Agent A       Agent B
independent   independent
analysis      analysis
   │             │
   └──────┬──────┘
          ↓
compare agreements / contradictions / omissions
          ↓
A reviews B's material claims
B reviews A's material claims
          ↓
resolve with evidence / escalation
          ↓
canonical synthesis
~~~

### Phase 1 — Independent construction

A and B receive:

- the same current objective;
- the same canonical project/task state needed for the assignment;
- the same authority boundary;
- the same expected artifact class.

They must not receive each other's hidden reasoning or draft before their first independent return.

They may use different lenses or specialist backgrounds when that improves coverage.

### Phase 2 — Comparison

The parent or designated synthesis owner records:

- agreements;
- contradictions;
- unique findings from A;
- unique findings from B;
- assumptions only one side made;
- evidence required to resolve disagreement;
- questions that must go to another owner or the user.

Do not collapse two reports into one by majority vote.

### Phase 3 — Cross-review

A receives B's **material conclusions/artifact**, not B's hidden chain of thought, and is asked to identify concrete errors, missing cases, unsupported assumptions, and better alternatives.

B does the same against A.

Cross-review is adversarial but bounded to material issues.

### Phase 4 — Synthesis

A single canonical artifact is produced only after material disagreements are resolved, incorporated, explicitly rejected with evidence, or escalated.

The synthesis owner may be:

- the delegated work owner;
- a dedicated synthesis/review role;
- the Orchestrator for coordination-level synthesis only.

The synthesis owner must not erase unresolved disagreement merely to produce a clean plan.

If A and B remain materially split after evidence review, create a fresh tie-breaker/reviewer or escalate to the actual authority owner.

## Pairing models

Not every pair needs two identical roles.

### Parallel peers

Use two agents with the same responsibility when independent framing is valuable.

Examples:

- `technical-planner-A` + `technical-planner-B`;
- two UX planners;
- two researchers testing competing explanations.

### Complementary pair

Use different specialties that examine the same artifact from distinct ownership lenses.

Examples:

- UI Visual Designer + UX/Interaction Reviewer;
- Backend Architect + Data/Consistency Reviewer;
- Security Architect + Threat Model Reviewer;
- QA Strategist + Failure/Edge-Case Reviewer;
- Performance Specialist + Observability Specialist.

The pair still needs a defined synthesis owner.

### Primary + independent shadow

For medium-risk bounded work, one agent may be the primary owner while a second isolated context independently reconstructs/checks the result before handoff.

The shadow must not be prompted to confirm the primary.

## Execution exception

Do **not** interpret the two-agent minimum as "two agents should edit the same source concurrently."

For implementation, the preferred pattern is:

~~~text
approved plan
    ↓
Implementation Owner
    ↓
Independent Reviewer / Validator
~~~

If implementation is naturally separable into independent workstreams, two implementation owners may work in parallel only when:

- file/contract ownership is clearly partitioned;
- unresolved shared architecture is already fixed;
- merge/integration ownership is explicit;
- each branch has independent validation.

Do not create two competing edits to the same unstable area merely to satisfy the pairing rule.

## Thinker Waves

A Thinker Wave for non-trivial work should normally contain **at least two fresh thinkers** with isolated initial contexts.

Each thinker:

- receives current canonical state;
- searches independently for missing questions/gaps;
- returns once;
- terminates.

The parent then deduplicates and routes material findings.

A later wave must use new fresh contexts.

One thinker may be sufficient only for tiny/low-risk bounded work where the Orchestrator records why a second perspective would add no material value.

## Department rule

When the Orchestrator activates a substantive department, that department should not normally consist of one isolated specialist working alone.

At minimum, provide either:

1. two independent peers; or
2. one primary specialist plus one independent complementary reviewer.

Examples:

### Product

- Product Planner A;
- Product Planner B / Product Challenger;
- fresh Thinker Wave when scope is broad.

### UI / UX

- UX/Interaction owner;
- Visual/UI or independent usability reviewer;
- accessibility specialist when applicable.

### Frontend

- frontend architecture/implementation owner;
- independent frontend reviewer focused on state, reuse, accessibility, performance, or integration as appropriate.

### Backend

- backend architecture/implementation owner;
- independent contract/data/security/concurrency reviewer as appropriate.

### Security

- security design owner;
- independent threat-model/adversarial reviewer.

### QA

- verification strategy owner;
- independent edge/failure/regression reviewer.

### Performance

- performance analysis/optimization owner;
- independent measurement/observability reviewer.

The exact roles should be chosen from the responsibility, not from a fixed ritual list.

## Orchestrator responsibilities

Before accepting a non-trivial delegated artifact, the Orchestrator must be able to answer:

- Who provided perspective A?
- Who provided perspective B?
- Were their initial constructions independent?
- What did they disagree on?
- How was each material disagreement resolved?
- Who owns the synthesis?
- Has a fresh independent reviewer challenged the synthesized artifact where risk warrants it?

If the answer to the first two questions is the same context, paired delegation did not occur.

## Manifest additions

For paired work, each `AGENT-MANIFEST` should also record:

~~~text
Pair-Group: <stable group id>
Pair-Position: A | B | REVIEWER | SYNTHESIS
Independence-Requirement: INITIAL_ISOLATION | COMPLEMENTARY_REVIEW
Peer-Artifact-Visibility: NONE_UNTIL_FIRST_RETURN | AFTER_FIRST_RETURN
~~~

The canonical orchestration state should record pair-group membership so a fresh Orchestrator can reconstruct who participated in a decision.

## Convergence

Paired work converges when:

- both required perspectives returned;
- material unique findings were considered;
- material contradictions are resolved, explicitly owned, or escalated;
- the canonical artifact records the synthesis rather than merely choosing one draft;
- any required independent gate after synthesis passes.

Two agents agreeing without showing differentiated investigation is not evidence of useful independence.

## Exceptions

The two-perspective default may be skipped only for genuinely trivial, low-risk, fully specified work where duplication would add no useful uncertainty reduction.

The exception should be explicit in orchestration state:

`Pairing-Exception: <reason>`

Do not use token cost or impatience alone as sufficient justification when the work is ambiguous, architectural, security-sensitive, user-facing, difficult to reverse, or expensive to rework.

## Anti-patterns

Do not:

- give B the answer from A before B forms an independent position;
- call A and B "independent" when they share the same reasoning transcript;
- use two agents only to produce a vote count;
- let the Orchestrator arbitrarily choose the preferred plan without resolving evidence;
- run two implementers against the same unstable files merely to satisfy a numeric rule;
- treat cross-review as permission for agents to expand scope outside their authority;
- keep paired agents alive as memory stores after their assignment is complete;
- count two nearly identical prompts with no differentiated evidence as meaningful validation.

## Design principle

**Important work should normally be thought through by more than one independent context before the organization commits to it.**

The objective is not consensus for its own sake. The objective is to make weak framing, missing scope, hidden assumptions, and fragile plans visible while they are still cheap to change.