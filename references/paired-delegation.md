# Paired Delegation / Same-Role Dual-Perspective Protocol

## Purpose

A capable subagent can still stop at the first plausible framing. For non-trivial cognitive work, the organization therefore normally uses **at least two fresh independent instances of the same contracted role** before treating a material artifact as mature.

This is not voting and not permission to combine professions.

Read with `references/role-purity.md`.

## Core rule

For every non-trivial cognitive workstream:

- A and B use the **same Agent-Key**;
- they have the same professional responsibility;
- they receive the same objective, relevant canonical evidence and authority boundary;
- they work independently before seeing the peer artifact;
- they compare/cross-review only after first return;
- synthesis happens only after material differences are resolved, routed, rejected with evidence or escalated.

Two different specialties do **not** satisfy the pair requirement.

## Contracted-role rule

Pair examples are valid only for Agent-Keys that actually exist as stable profiles.

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

A conceptual capability such as API/security/performance planning does not become an Agent-Key merely because it would logically use A+B later. Until a stable role exists, record a capability gap.

Thinkers are not stable Agent-Key roles and follow `references/thinker-waves.md`; for non-trivial questioning, use multiple fresh one-question Thinkers when capacity permits.

## Phase 1 — independent construction

A and B receive:

- identical current objective;
- identical canonical inputs/evidence relevant to the role;
- identical authority boundary;
- identical role contract;
- identical expected artifact class;
- comparable reasoning capability when the host permits it.

They must not see the other agent's draft/reasoning before their first return.

Independence means different contexts, not different responsibilities.

## Phase 2 — comparison

The parent records:

- agreements;
- contradictions;
- unique findings from A;
- unique findings from B;
- assumptions made by only one side;
- evidence needed to resolve disagreements;
- questions that belong to another owner.

Do not count agreement as proof by itself.

## Phase 3 — same-role cross-review

After first returns:

- A receives B's material artifact;
- B receives A's material artifact;
- each critiques only through the profession it already owns.

A frontend architect critiques frontend architecture, not product strategy or backend ownership. A graphic-design planner critiques visual design, not UX research. A backend architect critiques backend domain/service architecture, not public API/data/security.

## Phase 4 — synthesis

One canonical role artifact is produced only after every material difference is:

- resolved with evidence;
- incorporated;
- rejected with explicit evidence by the proper owner/authority;
- routed to another role;
- or escalated.

No majority vote.

Morrison may coordinate synthesis but must not invent missing domain decisions.

For cross-specialty technical artifacts, `technical-planner` may later integrate already-mature specialist outputs; that integration pair does not replace the underlying specialist pairs.

## Pair manifest

Each pair records at minimum:

```text
Pair-Group: <stable id>
Pair-Role: <Agent-Key>
Member-A: <unique instance>
Member-B: <unique instance>
Pair-Position: A | B
Independence-Requirement: INITIAL_ISOLATION
Peer-Artifact-Visibility: NONE_UNTIL_FIRST_RETURN
Started-From: <same canonical revision/artifact set>
Expected-Return: <same artifact class>
```

Both instances must use the same `Pair-Role` / Agent-Key.

## Pair lifecycle

Recommended states:

```text
CREATED
-> INDEPENDENT_WORK
-> FIRST_RETURNS
-> COMPARISON
-> CROSS_REVIEW
-> SYNTHESIS
-> RESOLVED | BLOCKED | STALE
```

If an upstream premise changes materially, mark affected pair synthesis `STALE` and create fresh instances when rework is required. Do not revive old contexts merely because their previous draft exists.

## Batching / slot limits

Same-role pairing must coexist with `references/batched-delegation.md`.

Prefer keeping A+B in a compatible batch/revision so they receive equivalent premises.

If runtime capacity is constrained:

- reduce unrelated concurrent work;
- keep the pair logically aligned to the same starting revision;
- never replace B with a different specialty to save a slot;
- persist first returns before cross-review;
- terminate completed contexts after canonical commit.

## Thinker waves

For non-trivial question discovery:

```text
fresh Thinker instances
-> each returns one strongest question/clean
-> parent deduplicates/routes
-> owners update canonical state
-> all Thinkers terminate
-> new fresh instances if another questioning round is useful
```

Do not reuse a Thinker for a second question.

## Planning before execution

The default paired pattern is for cognitive work such as research, planning, design, architecture and review.

It does **not** imply two implementers should edit the same unstable code.

For execution, prefer one coherent implementation owner followed by independent review/validation. Parallel writers require genuinely partitioned workstreams/files/contracts and explicit integration ownership.

## Exceptions

A pair may be skipped only when work is trivial/low-risk/fully specified or the runtime cannot support real independent contexts.

Record the reason. Do not claim independent dual perspective if it did not occur.

## Core principle

**Two independent minds are useful only when they are independently doing the same profession against the same problem; different professions complement one another but never substitute for the required pair.**