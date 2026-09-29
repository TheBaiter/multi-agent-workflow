# Batched Delegation / Agent Slot Protocol

## Purpose

A multi-agent organization must remain useful even when the host can run only a few child contexts concurrently.

Treat concurrency as a **slot budget**, not permission to keep the entire organization alive.

Canonical artifacts/questions/decisions/backlog are durable. Agent conversations are disposable execution contexts.

## Core rule

**Persist conclusions; terminate contexts. Do not keep completed agents alive merely because later work may need their conclusions.**

## Capacity discovery

At task start, determine when possible:

- `Max-Concurrent-Children`;
- `Currently-Available-Slots`;
- `Reserved-Capacity` when useful.

Never hard-code assumptions such as 8 or 10 children.

If the host exposes no reliable limit, start with a conservative working batch of roughly 2-4 children and adapt.

## Same-role pair scheduling

### Preferred mode — concurrent first returns

When at least two compatible slots exist, run first-return A+B concurrently from the same canonical starting revision.

If both contexts remain legitimately resumable for cross-review, use original-member cross-review. Otherwise switch to fresh same-role cross-review contexts under `references/paired-delegation.md`.

### Constrained mode — frozen-snapshot sequential first returns

A one-slot host must not make same-role pairing impossible.

If only one child slot is available:

1. freeze one canonical input snapshot/revision for the pair;
2. create/run first-return A from that snapshot;
3. persist A's first-return artifact and terminate A when the slot must be freed;
4. keep A's first return hidden from B;
5. do not apply A-derived changes to B's starting inputs;
6. create fresh first-return B from the exact same frozen snapshot/authority/objective;
7. persist B's first return and terminate B when appropriate;
8. only after both first returns, create the comparison record;
9. because original A/B may no longer exist, run **fresh same-role cross-reviewers** as needed:
   - fresh reviewer XR-A reviews B's first-return artifact;
   - fresh reviewer XR-B reviews A's first-return artifact;
10. if specialist reconciliation is still needed, run a fresh same-role synthesis instance using first returns + comparison + cross-review artifacts;
11. only then publish/update the canonical role artifact.

Do not resurrect terminated A/B merely to preserve naming symmetry.

Record:

```text
Pair-Execution-Mode: CONCURRENT | FROZEN_SNAPSHOT_SEQUENTIAL
Pair-Start-Revision: <same revision for first-return A+B>
Cross-Review-Mode: ORIGINAL_MEMBERS | FRESH_SAME_ROLE_REVIEWERS
Synthesis-Mode: ORIGINAL_MEMBER | FRESH_SAME_ROLE_SYNTHESIZER
```

If the runtime cannot preserve equivalent starting evidence or prevent B from seeing A's first return, full pair independence is reduced/blocked.

## Batch lifecycle

```text
QUEUED WORK
  -> select highest-value compatible items
  -> create batch
  -> spawn work within slot budget
  -> independent work / pair protocol
  -> collect returns
  -> persist artifacts + questions + comparison/review state + backlog
  -> terminate completed contexts
  -> free slots
  -> continue pair/review/synthesis or next work item
```

A batch is scheduling only; it never merges professions.

A logical pair group may span several physical one-child batches while still using one frozen `Pair-Start-Revision`.

## Batch contract

```text
DELEGATION-BATCH

Batch-ID: <stable id>
Parent: <orchestrator/delegated owner>
Started-From: <state revision>
Slot-Budget: <integer | UNKNOWN_CONSERVATIVE>
Active-Children: <instances>
Pair-Groups: <ids>
Objectives: <bounded objectives>
Expected-Returns: <artifacts>
Committed-Returns: <anchors>
Queued-After: <backlog anchors>
State: QUEUED | ACTIVE | COLLECTING | COMMITTED | TERMINATED
```

`COMMITTED` means every material output expected from that physical batch is durable. It does not necessarily mean its logical pair group has reached synthesis/resolution.

## Scheduling priorities

Prefer scheduling that:

1. preserves first-return pair independence;
2. completes both first returns before conclusions alter the shared start premise;
3. completes required cross-review/synthesis before calling the role artifact mature;
4. resolves blockers for multiple downstream roles;
5. runs independent departments from compatible revisions where useful;
6. avoids reviewers before their target artifact exists;
7. avoids competing implementation writers;
8. frees contexts promptly after durable return.

## Planning in chunks

Example with four available slots:

```text
Batch 1
  Thinker 1 -> one question -> terminate
  Thinker 2 -> one question -> terminate
  Product Planner A+B
  -> persist questions + Product Brief inputs/returns

Batch 2
  UX Planner A+B
  IA Planner A+B
  -> persist role artifacts

Batch 3
  Graphic Design Planner A+B
  Interaction Design Planner A+B
  -> persist artifacts

Batch 4
  Frontend Architect A+B
  Backend Architect A+B
  -> persist artifacts
```

With one child slot, the same conceptual work may require multiple physical batches per logical pair:

```text
P-A -> terminate
P-B from frozen snapshot -> terminate
P-XR-A -> terminate
P-XR-B -> terminate
P-SYNTH -> canonical artifact -> terminate
```

Use only the stages required by `references/paired-delegation.md`; do not add agents ceremonially when original-member cross-review remains genuinely available.

## Durable organizational backlog

```text
ORGANIZATIONAL-BACKLOG-ITEM

Item-ID: ...
Required-Role: <contracted Agent-Key | CAPABILITY_GAP:<specialty>>
Objective: ...
Depends-On: <artifact/question ids>
Priority: ...
Reason: ...
Expected-Return: ...
Status: QUEUED | READY | BLOCKED | DONE | DROPPED
Last-Revalidated-At: <state revision>
```

Revalidate queued work after upstream changes before spawning it.

## Parent continuity

A bounded parent may remain alive across batches only when active coordination materially benefits from continuity.

Children do not remain alive for memory.

Before even the parent terminates, checkpoint objective, current artifacts, fixed decisions, open questions, pair progress, backlog and next action.

## Thinkers

Thinkers occupy one slot, return one strongest question/clean, persist it through the parent, and terminate. New questions require fresh contexts.

## Plan reopening

Reopening stages may run sequentially:

```text
fresh Thinkers
-> Review Challenger pair
-> Alternative Planner pair
-> Risk Reviewer pair when warranted
-> premise-owner revision
```

Every role pair follows the same first-return/cross-review/synthesis rules, including fresh same-role fallback under one-slot constraints.

## Intensive UI rounds

Each intensive-UI questioning round uses new `ui-question-auditor` identities.

With >=2 slots, prefer concurrent round A+B.

With one slot:

- run round A then B from the same frozen round-start revision with first-return isolation;
- if A/B terminated, use fresh same-role round cross-reviewers rather than pretending the originals resumed;
- finalize one round receipt only after required comparison/cross-review is complete;
- terminate all round contexts;
- apply owner dispositions/revisions;
- start the next round using entirely new identities against the updated state.

## Anti-patterns

Do not:

- hard-code concurrency without evidence;
- keep completed agents alive as memory;
- exceed reliable slot capacity;
- run first-return pair members from different start revisions;
- expose A's first return to B before B's first return;
- pretend a terminated original member performed later cross-review;
- call sequential work independent when B saw A's conclusions;
- let Morrison invent specialist synthesis because all specialist contexts terminated;
- lose findings while killing batches;
- use idle agents instead of durable backlog;
- spawn every department at task start;
- leave stale backlog unreviewed after upstream changes.

## Core principle

**The organization can be larger than concurrent runtime capacity. Preserve independence with frozen starting evidence, and use fresh same-role review/synthesis contexts rather than pretending terminated agents can come back.**