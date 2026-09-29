# Intensive UI Questioning — Fresh Round Integration

## Purpose

This contract tells Morrison how to execute the external `intensive-ui-questioning` skill without weakening fresh-review behavior or breaking atomic role ownership.

Canonical external source:

- Repository: `https://github.com/TheBaiter/intensive-ui-questioning`
- Entrypoint: `SKILL.md`
- Delegated audit: external `references/subagent-question-audit.md`
- Fresh rounds: external `references/fresh-questioning-rounds.md`

This local file owns MAW scheduling/ownership integration only.

## Activation

Activate for meaningful visible/perceptible UI/frontend work according to `references/skill-routing.md`.

For non-trivial delegated use, create a dedicated `ui-question-auditor` workstream. Do not attach one pass to a planner and call the external skill complete.

## Atomic audit role

Agent-Key: `ui-question-auditor`

Profile: `references/profiles/ui-question-auditor/PROFILE.md`

Owns:

- question/route coverage;
- one-by-one question status;
- skipped/new dependency discovery;
- evidence-boundary checks;
- route-closure reporting.

Does not own product/design/architecture answers uncovered by those questions.

`Can-Spawn: NONE`; missing evidence/owners route upward.

## Round budget

For ordinary non-trivial delegated UI:

`Required-Rounds: 4`

Use 5 for broad redesign/new major surfaces, multiple active packs, high rework cost, accessibility/state complexity, known prior UI regressions, or when round 4 still produces a material finding/change.

Tiny deterministic visible work may use the external skill's documented lightweight exception when genuinely applicable.

## Every round has two distinct responsibilities

### 1. Independent first perspectives

Each round starts with fresh same-role first-return A+B from the same frozen current state.

Their job is to independently traverse/audit assigned coverage and expose omissions/questions/evidence gaps.

### 2. Complete coverage / synthesis ownership

Before a round receipt may claim route closure, one `ui-question-auditor` same-role synthesis owner must take explicit accountability for the **complete current intensive-UI route**.

That synthesis owner maps to the external skill's “main agent” accountability for the round and must:

- read current external `SKILL.md` completely;
- read current external `references/questions/INDEX.md` completely;
- reconcile A/B and any partitioned audit scopes;
- ensure every materially plausible route is ACTIVE or grounded NOT_ACTIVE when needed;
- ensure every active pack/source has complete owned coverage;
- ensure applicable questions were handled individually;
- follow dependencies until closure/block;
- inspect/re-read contested material sources when necessary;
- emit final round `ROUTE_CLOSURE` and coverage receipt.

Morrison schedules/records this owner but does not replace it.

A UI planner's local skill use never substitutes for this task-level coverage owner.

## Fresh identity invariant

Each **new round** uses new first-return auditor identities/names:

```text
Round 1: ui-question-auditor-r1-a / r1-b
Round 2: ui-question-auditor-r2-a / r2-b
...
```

A terminated auditor is never recreated/resumed under the same identity/name.

Fresh continuation contexts inside the **same round** (cross-review/synthesis) also use unique names, for example:

```text
ui-question-auditor-r1-xreview-a
ui-question-auditor-r1-xreview-b
ui-question-auditor-r1-synth
```

They remain part of Round 1; they do not consume Round 2's freshness budget.

## Pair mechanics inside a round

First-return A+B share:

- same Agent-Key;
- round number;
- frozen current canonical revision;
- objective/authority/evidence class;
- initial isolation.

Neither sees the peer's first return before its own exists.

### Concurrent-capable runtime

Prefer concurrent A+B.

If an original member remains legitimately resumable, same-role cross-review/synthesis may use it.

### One-slot / terminated-original runtime

Use:

```text
rN-a first return from frozen snapshot -> terminate
rN-b first return from same snapshot with no A visibility -> terminate
comparison
fresh rN-xreview-a -> reviews B -> terminate
fresh rN-xreview-b -> reviews A -> terminate
fresh rN-synth -> complete route reconciliation + synthesis + round receipt -> terminate
```

Do not pretend terminated A/B performed later review.

If an original member remains as synthesis owner instead of a fresh `rN-synth`, it must explicitly satisfy the same complete-coverage obligations above.

## Context continuity without context reuse

Round N receives current canonical state after earlier rounds:

- objective/fixed decisions;
- current product/UI/architecture/implementation artifact;
- active routes/packs;
- prior round findings/dispositions;
- changes caused by them;
- unresolved owner questions;
- current source/rendered/runtime evidence;
- verification expectations.

Do not pass hidden prior auditor reasoning.

Continuity belongs to canonical artifacts/receipts; skepticism belongs to fresh contexts.

## Round lifecycle

```text
CURRENT CANONICAL STATE
  -> spawn fresh Round N first-return A+B
  -> independent audit first returns
  -> compare
  -> same-role cross-review (original or fresh)
  -> same-role complete-coverage synthesis owner
     -> re-read full entrypoint + routing inventory
     -> reconcile delegated coverage
     -> close or block current routes
  -> persist UI-QUESTIONING-ROUND receipt
  -> route findings to premise owners
  -> premise owners disposition/revise current artifact
  -> terminate all Round N contexts
  -> Round N+1 starts with entirely new first-return identities against updated state
```

Next round must not start until the prior round's receipt and required owner dispositions are durable.

## Question granularity

Every applicable question gets an individual status:

- `ANSWERED`;
- `NOT_APPLICABLE: <grounded reason>`;
- `OWNER_REQUIRED: <smallest unresolved decision>`;
- `FAILED_INTEGRITY: <evidence>`;
- `BLOCKED: <reason>`.

Do not compress checks into generic conclusions.

Out-of-role decision questions route to premise owners.

## Progressive repetition

Later rounds inspect the **updated** artifact:

- Round 1 establishes initial complete coverage/gaps;
- Round 2 re-questions after dispositions/revisions;
- Round 3 tests consequences/new routes/redundancy/ownership;
- Round 4 challenges the now-mature state;
- Round 5, when required, challenges the final changed/high-risk state.

Every round synthesis owner performs full current routing-inventory accountability, so newly activated packs cannot disappear between delegated scopes.

## Canonical state / round receipt

Task state records:

```text
UI-QUESTIONING
Status: ACTIVE | COMPLETE | BLOCKED | STALE
Required-Rounds: 4 | 5
Completed-Rounds: <0..5>
Fresh-Round-Guarantee: FULL | REDUCED | BLOCKED
Current-Round: <1..5 | NONE>
Current-Artifact: <anchor/revision>
Round-Receipts: <anchors>
Open-Question-IDs: <ids>
Last-Material-Change: <anchor/revision>
Final-Route-Closure: COMPLETE | OPEN_DEPENDENCIES | BLOCKED | NOT_REACHED
```

Each receipt records at least:

```text
UI-QUESTIONING-ROUND

Round: <n>
Pair-Group: <id>
Pair-Execution-Mode: CONCURRENT | FROZEN_SNAPSHOT_SEQUENTIAL
Pair-Start-Revision: <revision>
First-Return-Instances: <A,B>
Cross-Review-Mode: ORIGINAL_MEMBERS | FRESH_SAME_ROLE_REVIEWERS
Cross-Review-Instances: <ids | NOT_REQUIRED>
Coverage-Owner-Instance: <same-role synthesis/original instance>
Coverage-Owner-Entrypoint-Read: COMPLETE | BLOCKED
Coverage-Owner-Router-Inventory-Read: COMPLETE | BLOCKED
Synthesis-Mode: ORIGINAL_MEMBER | FRESH_SAME_ROLE_SYNTHESIZER
All-Round-Agent-Instances: <unique ids>
Coverage-Scope: ...
Route-Inventory-Disposition: <anchor>
Questions-Processed: <anchor/count>
Delegated-Coverage-Reconciled: YES | NO | BLOCKED
New-Findings: ...
Rechecked-Prior-Findings: ...
Newly-Activated-Routes: ...
Owner-Questions: ...
Artifact-Changes: ...
Route-Closure: COMPLETE | OPEN_DEPENDENCIES | BLOCKED
Evidence-Limits: ...
```

## Interaction with premise owners

Auditors question/route. Atomic owners decide.

Example:

```text
Round finds keyboard/focus gap
  -> Accessibility Planner owns requirement
  -> accessibility artifact updated
  -> current UI artifact/state updated
  -> next fresh round re-evaluates current route
```

The round coverage owner does not decide accessibility merely because it discovered/reconciled the route.

## Later phases

The external skill remains active while visible/perceptible work continues through architecture, implementation, verification and validation.

Material implementation changes can stale earlier coverage. Reopen affected UI routes/required fresh rounds rather than treating planning-time closure as permanent validation.

Four/five questioning rounds do not replace final independent validation.

## Completion

Normal delegated intensive-UI questioning is complete only when:

- required 4/5 rounds are complete;
- every round began with fresh first-return identities;
- any fresh cross-review/synthesis contexts are recorded truthfully;
- each round had an explicit complete-coverage owner;
- that owner completely read the current external entrypoint + routing inventory;
- delegated coverage was reconciled;
- applicable questions were handled individually;
- findings were owner-routed/dispositioned;
- later rounds consumed updated canonical state, not old hidden context;
- final required round reports complete route closure;
- no material dependency remains silently unowned;
- late material changes received another required fresh audit;
- evidence limitations remain explicit.

## Core rule

**Distributed UI questioning may delegate packs, but complete route closure always has one explicit same-role audit owner per fresh round.**