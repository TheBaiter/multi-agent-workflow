# Batched Delegation / Agent Slot Protocol

## Purpose

A multi-agent organization must remain useful even when the host can run only a limited number of child agents concurrently.

The Orchestrator must therefore treat concurrent agent capacity as a **slot budget**, not as permission to keep an entire organization alive at once.

The organization advances in bounded batches. Each batch produces durable artifacts, returns them to its parent, terminates contexts that are no longer needed, and frees capacity for the next batch.

## Core rule

**Do not keep agents alive merely because later work may need their conclusions. Persist conclusions; terminate contexts.**

Canonical artifacts, question records, decisions, evidence anchors and backlog items are durable. Agent conversations are disposable execution contexts.

## Capacity discovery

The Orchestrator must not hard-code assumptions such as `8` or `10` concurrent children.

At task start, determine when possible:

- `Max-Concurrent-Children`: host/runtime limit;
- `Currently-Available-Slots`: usable capacity now;
- `Reserved-Capacity`: capacity intentionally left free for routing, urgent evidence work or required pair completion.

If the host does not expose a reliable limit, use a conservative working batch of **2 to 4 children** and adapt if the runtime reports saturation.

Same-role A/B pairs must fit completely in one batch. Do not run A now and B much later against a materially different state and call them an independent pair.

## Batch lifecycle

~~~text
QUEUED WORK
    ↓
select highest-value compatible items
    ↓
create BATCH
    ↓
spawn children within slot budget
    ↓
independent work / pair protocol
    ↓
collect returns
    ↓
write canonical artifacts + findings + backlog
    ↓
terminate completed children
    ↓
free slots
    ↓
next BATCH
~~~

A batch is organizational scheduling only. It does not merge professional roles.

## Batch contract

Record:

~~~text
DELEGATION-BATCH

Batch-ID: <stable id>
Parent: <orchestrator/delegated owner>
Started-From: <state revision>
Slot-Budget: <integer or UNKNOWN_CONSERVATIVE>
Active-Children: <instances>
Pair-Groups: <ids>
Objectives: <bounded objectives>
Expected-Returns: <artifacts>
Queued-After: <backlog anchors>
State: QUEUED | ACTIVE | COLLECTING | COMMITTED | TERMINATED
~~~

`COMMITTED` means all material outputs required from the batch have been persisted into canonical state/artifacts. Only after that should contexts be terminated and slots reused.

## Scheduling priorities

Prefer batches that:

1. complete a same-role pair rather than leave one half waiting;
2. resolve blockers for multiple downstream roles;
3. isolate independent departments that can safely work from the same canonical revision;
4. avoid spawning reviewers before the artifact they must review exists;
5. keep implementation writers from competing for the same unstable ownership;
6. free contexts promptly once their return is durable.

## Planning organization in chunks

A large product may need many departments, but they do not need to be alive simultaneously.

Example:

~~~text
Batch 1
  Thinker 1 -> one question -> terminate
  Thinker 2 -> one question -> terminate
  Product Planner A
  Product Planner B
        ↓
commit questions + Product Brief
terminate completed contexts

Batch 2
  UX Planner A
  UX Planner B
  IA Planner A
  IA Planner B
        ↓
commit UX + IA artifacts
terminate

Batch 3
  Graphic Design Planner A+B
  Interaction Design Planner A+B
        ↓
commit artifacts
terminate

Batch 4
  Frontend Architect A+B
  Backend Architect A+B
        ↓
...
~~~

The exact grouping depends on dependencies and available slots. Do not force four children when only two are useful.

## Durable backlog

Work that cannot fit in the current batch belongs in a durable organizational backlog, not in the memory of waiting agents.

Each item should record:

~~~text
ORGANIZATIONAL-BACKLOG-ITEM

Item-ID: ...
Required-Role: <Agent-Key>
Objective: ...
Depends-On: <artifact/question ids>
Priority: ...
Reason: ...
Expected-Return: ...
Status: QUEUED | READY | BLOCKED | DONE | DROPPED
~~~

When a batch finishes, re-evaluate queued items against the newest canonical state before spawning them. A downstream task may become unnecessary or need different inputs after upstream planning changes.

## Parent continuity

For a large delegated workstream, one parent owner may remain alive across multiple batches if active coordination genuinely benefits from continuity.

Its children should not remain alive for that reason.

If even the parent must terminate, its work must first be checkpointed so a fresh owner can reconstruct:

- objective;
- current canonical artifacts;
- open questions;
- queued work;
- decisions fixed;
- next batch.

## Interaction with Thinker Waves

Thinkers are especially suitable for slot-based batching because each instance is single-use.

A thinker occupies one slot, returns one material question, and terminates. New questions require new thinker instances, potentially in the next batch.

Do not keep a Thinker waiting while another role answers its question.

## Interaction with plan reopening

A mature plan may require several review specialties. Run them in sequential batches when capacity is limited:

~~~text
fresh one-question Thinkers
    ↓
Review Challenger A+B
    ↓
Alternative Planner A+B
    ↓
Risk Reviewer A+B when warranted
    ↓
plan owner revision
~~~

Each stage persists its report before freeing slots for the next.

## Anti-patterns

Do not:

- hard-code a host concurrency limit without evidence;
- keep completed agents alive as memory stores;
- spawn more children than the host can reliably support;
- split an A/B pair across incompatible canonical revisions;
- lose findings when terminating a batch;
- use queued agents as a substitute for a durable backlog;
- spawn every department at task start;
- leave stale queued work unreviewed after upstream plans change.

## Design principle

**The organization can be larger than the runtime's concurrent capacity because durable state carries work between batches.**

Scale breadth through sequential batches, not through an ever-growing set of live contexts.