# Paired Delegation / Same-Role Dual-Perspective Protocol

## Purpose

A capable subagent can still stop at the first plausible framing. For non-trivial cognitive work, the organization therefore normally obtains **at least two fresh independent first returns from the same contracted role** before treating a material artifact as mature.

This is not voting and not permission to combine professions.

Read with `references/role-purity.md` and `references/batched-delegation.md`.

## Core rule

For every non-trivial cognitive workstream:

- first-return A and B use the same Agent-Key/profession;
- they receive the same objective, frozen relevant canonical evidence, authority boundary and expected artifact class;
- they remain independent until both first returns exist;
- comparison/cross-review begins only after both independent first returns;
- all cross-review remains inside the same profession;
- synthesis happens only after material differences are resolved, routed, rejected with evidence or escalated.

Two different specialties do **not** satisfy the pair requirement.

## Contracted-role rule

Only stable contracted Agent-Keys may form role pairs.

Current general examples include:

```text
product-planner-A + product-planner-B
researcher-A + researcher-B
ux-planner-A + ux-planner-B
information-architecture-planner-A + B
graphic-design-planner-A + B
interaction-design-planner-A + B
design-system-planner-A + B
accessibility-planner-A + B
frontend-architect-A + frontend-architect-B
backend-architect-A + backend-architect-B
technical-planner-A + technical-planner-B
review-challenger-A + review-challenger-B
alternative-planner-A + alternative-planner-B
risk-reviewer-A + risk-reviewer-B
quality-strategist-A + quality-strategist-B
```

A conceptual capability such as API/security/performance planning is not an Agent-Key until a stable profile exists. Record a capability gap instead of inventing one.

Thinkers are not stable Agent-Key roles; they follow `references/thinker-waves.md`.

## Phase 1 — independent construction

First-return members A and B receive:

- identical objective;
- identical frozen canonical input set/revision;
- identical authority boundary;
- identical role contract;
- identical expected artifact class;
- comparable reasoning capability when host permits.

Neither sees the other's artifact or hidden reasoning before its own first return.

Independence is about isolated context and equivalent starting evidence; it does not require wall-clock concurrency when the host cannot provide it.

## Phase 2 — comparison

After both first returns exist, the parent records:

- agreements;
- contradictions;
- unique findings from A;
- unique findings from B;
- assumptions made by only one side;
- evidence needed to resolve disagreement;
- questions owned by another role/authority.

Agreement is not proof by itself. Do not vote.

## Phase 3 — same-role cross-review

### Mode A — original-member cross-review

Use when A and B remain legitimately resumable after first returns without violating runtime slot/lifecycle constraints.

- A reviews B's material artifact through the same profession;
- B reviews A's material artifact through the same profession.

### Mode B — fresh same-role cross-review

Use when original A/B contexts had to terminate (for example, a one-slot runtime) or when fresh review is preferable.

Create fresh instances of the **same Agent-Key** after both first returns are durable:

```text
<role>-xreview-a -> reviews first-return B (with access to comparison record as allowed)
<role>-xreview-b -> reviews first-return A
```

Rules:

- cross-reviewers are new concrete identities/names;
- they receive the same role contract and the two first-return artifacts;
- each is assigned one bounded peer-review target;
- they do not retroactively become first-return A/B;
- they may not absorb neighboring specialties;
- they terminate after their cross-review artifact is durable.

If only one slot exists, these two cross-reviewers may run sequentially because independence between their review outputs is not the original first-return independence requirement; however, do not expose one cross-reviewer's hidden reasoning to the other.

Record:

`Cross-Review-Mode: ORIGINAL_MEMBERS | FRESH_SAME_ROLE_REVIEWERS`

## Phase 4 — synthesis

One canonical role artifact is produced only after every material difference/finding is:

- resolved with evidence;
- incorporated;
- rejected with explicit evidence by the proper owner/authority;
- routed to another role;
- or escalated.

### Synthesis owner

Prefer one of these, in order:

1. an original same-role member that remains validly resumable and can synthesize after cross-review;
2. a fresh same-role `SYNTHESIS` instance when original members terminated or fresh synthesis materially improves independence.

Morrison may coordinate mechanics/state but must not invent specialist domain decisions.

A fresh synthesis instance receives first returns, comparison record and cross-review artifacts. It may reconcile only decisions owned by that role and must escalate/reroute anything outside its authority.

Record:

`Synthesis-Mode: ORIGINAL_MEMBER | FRESH_SAME_ROLE_SYNTHESIZER`

No majority vote.

For cross-specialty technical artifacts, `technical-planner` may later integrate mature specialist outputs; that integration pair does not replace underlying specialist pairs.

## Pair record

Record at minimum:

```text
PAIR-GROUP

Pair-Group: <stable id>
Pair-Role: <Agent-Key>
Pair-Execution-Mode: CONCURRENT | FROZEN_SNAPSHOT_SEQUENTIAL
Pair-Start-Revision: <frozen canonical revision/input-set id>
First-Return-A: <instance + artifact>
First-Return-B: <instance + artifact>
Peer-Visibility-Before-First-Returns: NONE
Cross-Review-Mode: ORIGINAL_MEMBERS | FRESH_SAME_ROLE_REVIEWERS
Cross-Reviewer-A: <instance | NOT_REQUIRED>
Cross-Reviewer-B: <instance | NOT_REQUIRED>
Synthesis-Mode: ORIGINAL_MEMBER | FRESH_SAME_ROLE_SYNTHESIZER
Synthesis-Instance: <instance | original member>
Expected-Return: <artifact class>
```

Every first-return/cross-review/synthesis instance uses the same contracted Agent-Key for that pair group.

## Pair lifecycle

```text
CREATED
-> INDEPENDENT_WORK
-> FIRST_RETURNS
-> COMPARISON
-> CROSS_REVIEW
-> SYNTHESIS
-> RESOLVED | BLOCKED | STALE
```

If an upstream premise changes materially, mark affected synthesis stale and create fresh instances as required. Do not resurrect terminated contexts merely because their artifact exists.

## Slot-constrained execution

Use `references/batched-delegation.md`.

Preferred with >=2 child slots:

- concurrent A+B;
- original-member cross-review if contexts remain legitimately available;
- same-role synthesis.

With one child slot:

1. freeze pair start snapshot;
2. run first-return A; terminate after durable first return;
3. run fresh first-return B from exact same snapshot without seeing A; terminate;
4. compare first returns;
5. run fresh same-role cross-reviewer A against B; terminate;
6. run fresh same-role cross-reviewer B against A; terminate;
7. run a fresh same-role synthesis instance when specialist reconciliation is needed;
8. persist canonical artifact and resolve pair.

This is more contexts but preserves role purity and truthful independence under constrained concurrency.

If the host cannot preserve the frozen snapshot or hide A's first return from B, record pair independence as reduced/blocked; do not pretend full pairing occurred.

## Thinker waves

Thinkers use a separate micro-review contract:

```text
fresh Thinkers
-> one strongest question/clean each
-> parent deduplicates/routes
-> owners update canonical state
-> all Thinkers terminate
-> new fresh Thinkers when another wave is useful
```

Do not reuse a Thinker for a second question.

## Planning before execution

Pairing primarily applies to cognitive work: research, planning, design, architecture and review.

It does **not** require two writers editing the same unstable code.

Execution normally uses one coherent implementation owner per write surface, followed by fresh independent validation. Parallel writers require genuinely partitioned workstreams/contracts and explicit integration ownership.

## Exceptions

A pair may be skipped only for documented trivial/low-risk/fully specified work or when the runtime cannot provide genuine isolated contexts/snapshots.

Record the exception/reduced guarantee. Never claim independent dual perspective when it did not occur.

## Core principle

**Two independent first perspectives come from the same profession and same starting evidence. Cross-review and synthesis may use fresh same-role contexts when runtime constraints force the original pair to terminate; role purity and independence matter more than preserving agent identity.**