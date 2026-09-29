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

### Preferred mode: concurrent pair

When at least two compatible slots exist, run A+B of the same role concurrently from the same canonical starting revision.

### Constrained mode: frozen-snapshot sequential pair

A host with fewer than two child slots must not make same-role pairing impossible.

If only one child slot is available, A and B may execute sequentially **only when independence is preserved**:

1. freeze one canonical input snapshot/revision for the pair;
2. run A from that snapshot;
3. seal/persist A's first return where B cannot see it;
4. do not apply A-derived changes to B's input state yet;
5. create a fresh B instance from the exact same frozen snapshot/authority/objective;
6. collect B's first return without exposing A's artifact/reasoning;
7. only after both first returns, enter comparison/cross-review;
8. then update canonical state.

Record:

```text
Pair-Execution-Mode: CONCURRENT | FROZEN_SNAPSHOT_SEQUENTIAL
Pair-Start-Revision: <same revision for A+B>
```

Do **not** run B later against a materially changed state and call it the independent pair for A.

If the runtime cannot preserve an equivalent frozen starting snapshot or isolate B from A's first return, record pairing as reduced/blocked rather than claiming full independence.

## Batch lifecycle

```text
QUEUED WORK
  -> select highest-value compatible items
  -> create batch
  -> spawn work within slot budget
  -> independent work / pair protocol
  -> collect returns
  -> commit canonical artifacts + findings + backlog
  -> terminate completed contexts
  -> free slots
  -> next batch
```

A batch is scheduling only; it never merges professions.

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
Queued-After: <backlog anchors>
State: QUEUED | ACTIVE | COLLECTING | COMMITTED | TERMINATED
```

`COMMITTED` means every material result required from the batch is durable elsewhere. Only then should completed contexts be discarded/reused.

## Scheduling priorities

Prefer scheduling that:

1. preserves same-role pair independence;
2. completes pair first returns before letting one member's conclusions alter the other's starting premises;
3. resolves blockers for multiple downstream roles;
4. runs truly independent departments from compatible canonical revisions;
5. avoids reviewers before their target artifact exists;
6. avoids competing implementation writers on the same unstable ownership;
7. frees contexts promptly after canonical commit.

## Planning in chunks

A large product may need many departments without keeping them alive simultaneously.

Example with four available slots:

```text
Batch 1
  Thinker 1 -> one question -> terminate
  Thinker 2 -> one question -> terminate
  Product Planner A+B
  -> commit questions + Product Brief
  -> terminate

Batch 2
  UX Planner A+B
  IA Planner A+B
  -> commit artifacts
  -> terminate

Batch 3
  Graphic Design Planner A+B
  Interaction Design Planner A+B
  -> commit artifacts
  -> terminate

Batch 4
  Frontend Architect A+B
  Backend Architect A+B
  -> commit artifacts
  -> terminate
```

With one available child slot, the same conceptual organization runs sequentially using frozen-snapshot A/B first-return scheduling.

Do not force a particular batch size when fewer children are useful.

## Durable organizational backlog

Work that does not fit the active batch belongs in durable state, not waiting-agent memory.

```text
ORGANIZATIONAL-BACKLOG-ITEM

Item-ID: ...
Required-Role: <contracted Agent-Key or capability gap>
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

A bounded parent/work owner may remain alive across batches only when active coordination materially benefits from continuity.

Children do not remain alive for memory.

Before even the parent terminates, checkpoint objective, current artifacts, fixed decisions, open questions, backlog and next action so a fresh owner can resume.

## Thinkers

Thinkers fit batching naturally:

- occupy one slot;
- return one strongest material question/clean;
- terminate;
- never wait for the answer;
- new questions use new contexts.

## Plan reopening

Review perspectives may run in sequential batches:

```text
fresh one-question Thinkers
-> Review Challenger A+B
-> Alternative Planner A+B
-> Risk Reviewer A+B when warranted
-> premise-owner revisions
```

Each stage commits its report before freeing slots.

Same-role A+B inside those stages follows the concurrent/frozen-snapshot rule above.

## Intensive UI rounds

Each intensive-UI questioning round uses fresh `ui-question-auditor` instances.

Prefer concurrent A+B. With one child slot, run the round's A and B sequentially from the same frozen round-start revision, without exposing A's first return to B. Comparison/cross-review happens only after both first returns.

Complete/persist/disposition the current round before starting the next round with entirely new instance identities.

## Anti-patterns

Do not:

- hard-code concurrency without evidence;
- keep completed agents alive as memory;
- exceed reliable slot capacity;
- run pair members from materially different starting revisions;
- expose A's first return to B before B's independent first return;
- call sequential work independent when the second member saw the first member's conclusions;
- lose findings when killing a batch;
- use idle agents instead of durable backlog;
- spawn every department at task start;
- leave stale backlog unreviewed after upstream changes.

## Core principle

**The organization can be larger than concurrent runtime capacity. Pair independence comes from equivalent isolated starting evidence—not from requiring simultaneous execution when the host cannot provide it.**