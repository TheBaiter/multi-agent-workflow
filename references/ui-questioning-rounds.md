# Intensive UI Questioning — Fresh Round Integration

## Purpose

This contract tells Morrison how to execute the external `intensive-ui-questioning` skill without weakening its fresh-review behavior or breaking atomic role ownership.

Canonical external source:

- Repository: `https://github.com/TheBaiter/intensive-ui-questioning`
- Entrypoint: `SKILL.md`
- Delegated audit contract: external `references/subagent-question-audit.md`
- Fresh-round contract: external `references/fresh-questioning-rounds.md`

Always read current external sources when activated. This local file owns only MAW organization/runtime integration.

## Activation

Activate for meaningful visible/perceptible UI/frontend work according to `references/skill-routing.md`.

For non-trivial delegated use, Morrison creates a dedicated `ui-question-auditor` workstream rather than attaching one audit pass to a planner and calling the skill complete.

## Atomic audit role

Stable Agent-Key:

`ui-question-auditor`

Profile:

`references/profiles/ui-question-auditor/PROFILE.md`

It owns:

- routed question/pack coverage;
- one-by-one question status;
- dependency/omission/contradiction discovery;
- evidence-boundary checks;
- route-closure reporting.

It does **not** own UX, IA, visual, interaction, accessibility, design-system, frontend architecture, product authority, implementation or final validation.

`Can-Spawn: NONE`. Missing evidence/owners are routed to Morrison rather than spawning another organization under the auditor.

## Fresh round budget

For ordinary non-trivial visible/perceptible work:

`Required-UI-Questioning-Rounds: 4`

Use 5 when one or more apply:

- broad redesign/new major surface;
- several specialized packs active;
- complex user-flow/state/accessibility interactions;
- high rework cost;
- known prior UI regressions/late missed questions;
- round 4 still produces a material new finding/change.

Four/five is a bounded quality gate, not an infinite loop.

A fundamental unresolved flaw in the final required round returns work to the owning premise/gate; do not manufacture PASS.

## Round identity invariant

Every **new round** uses entirely new concrete auditor identities/names.

Example first-return members:

```text
Round 1
- ui-question-auditor-r1-a
- ui-question-auditor-r1-b

Round 2
- ui-question-auditor-r2-a
- ui-question-auditor-r2-b
```

Never resume/recreate a terminated auditor under the same identity/name.

If the host cannot create genuinely fresh identities, record `Fresh-Round-Guarantee: REDUCED | BLOCKED` and do not claim normal closure.

## Pairing inside one round

Each non-trivial round normally starts with same-role independent first returns A+B:

- same Agent-Key;
- same round;
- same frozen current canonical revision;
- equivalent authority/evidence class;
- initial isolation;
- no visibility of the other's first return.

### >=2 child slots

Prefer concurrent first-return A+B.

If originals remain validly resumable, they may cross-review each other's first returns.

### one child slot / originals terminated

Use `references/paired-delegation.md` + `references/batched-delegation.md`:

```text
rN-a first return from frozen snapshot -> terminate
rN-b first return from same frozen snapshot, no A visibility -> terminate
comparison
fresh rN-xreview-a -> reviews B -> terminate
fresh rN-xreview-b -> reviews A -> terminate
fresh rN-synth when same-role reconciliation is needed -> round synthesis
round receipt
```

These fresh review/synthesis instances are still part of **Round N**; they are not Round N+1 and do not consume the next round's freshness budget.

Every such instance has a unique runtime identity/name and the same `ui-question-auditor` Agent-Key.

Do not pretend terminated `rN-a`/`rN-b` later performed cross-review.

## Context continuity without context reuse

Round N receives latest canonical state after earlier rounds:

- user objective/fixed product decisions;
- current product/UI/architecture/implementation artifact;
- current intensive-UI route/active packs;
- prior round findings;
- owner dispositions;
- changes caused by findings;
- unresolved owner questions;
- current source/rendered/runtime evidence;
- verification expectations.

Do **not** pass prior auditor hidden reasoning transcripts.

Continuity belongs to canonical artifacts/questions/evidence/receipts; skepticism belongs to fresh contexts.

## Round lifecycle

```text
CURRENT CANONICAL STATE
  -> create fresh first-return auditors for Round N
  -> read current intensive-UI sources
  -> process questions one by one
  -> collect two independent first returns
  -> compare
  -> same-role cross-review (original or fresh contexts)
  -> same-role synthesis if needed
  -> commit UI-QUESTIONING-ROUND receipt
  -> route findings to premise owners
  -> premise owners disposition/revise canonical artifact
  -> terminate all Round N contexts
  -> Round N+1 starts with entirely new identities against updated state
```

The next round must not start before the current round's required audit artifacts and owner dispositions are durably represented.

## Question granularity

Every applicable distinct question remains observable as one of:

- `ANSWERED`;
- `NOT_APPLICABLE: <grounded reason>`;
- `OWNER_REQUIRED: <smallest decision>`;
- `FAILED_INTEGRITY: <evidence>`;
- `BLOCKED: <reason>`.

Do not replace multiple questions with a generic statement such as `UX looks correct`.

A question outside auditor authority routes to its premise owner.

## Progressive repetition

Rounds inspect a progressively changed artifact:

- Round 1 establishes current route coverage and obvious gaps.
- Round 2 re-questions the artifact after Round-1 dispositions/revisions.
- Round 3 inspects consequences/new routes/redundancy/ownership created by earlier changes.
- Round 4 is another fresh challenge of the now-mature state.
- Round 5, when required, challenges the final changed/high-risk state.

Every round re-traverses enough of the current external router to detect newly activated routes.

A later round may preserve earlier decisions but must independently re-evaluate them against current state.

## Canonical state

Persist:

```text
UI-QUESTIONING

Skill: intensive-ui-questioning
Status: ACTIVE | COMPLETE | BLOCKED | STALE
Required-Rounds: 4 | 5
Completed-Rounds: <0..5>
Fresh-Round-Guarantee: FULL | REDUCED | BLOCKED
Current-Round: <1..5 | NONE>
Current-Artifact: <anchor/revision>
Round-Receipts:
- <anchors>
Open-Question-IDs:
- <ids>
Last-Material-Change: <anchor/revision>
Final-Route-Closure: COMPLETE | OPEN_DEPENDENCIES | BLOCKED | NOT_REACHED
```

Each round receipt preserves:

```text
UI-QUESTIONING-ROUND

Round: <n>
Pair-Group: <id>
Pair-Execution-Mode: CONCURRENT | FROZEN_SNAPSHOT_SEQUENTIAL
Pair-Start-Revision: <revision>
First-Return-Instances:
- <A>
- <B>
Cross-Review-Mode: ORIGINAL_MEMBERS | FRESH_SAME_ROLE_REVIEWERS
Cross-Review-Instances:
- <ids | NOT_REQUIRED>
Synthesis-Mode: ORIGINAL_MEMBER | FRESH_SAME_ROLE_SYNTHESIZER
Synthesis-Instance: <id>
All-Round-Agent-Instances:
- <unique ids/names>
Coverage-Scope: ...
Questions-Processed: ...
New-Findings: ...
Rechecked-Prior-Findings: ...
Newly-Activated-Routes: ...
Owner-Questions: ...
Artifact-Changes: ...
Route-Closure: COMPLETE | OPEN_DEPENDENCIES | BLOCKED
Evidence-Limits: ...
```

## Interaction with premise owners

Auditors question/route; atomic planners/owners decide within their profession.

Example:

```text
UX Planner A+B -> UX plan
  -> UI Questioning Round 1
     -> UX finding -> UX premise owner
     -> accessibility finding -> Accessibility Planner
     -> IA finding -> IA Planner
  -> owner dispositions/revisions
  -> UI Questioning Round 2 (all new identities)
```

## Later phases

The external skill remains active when visible/perceptible work continues through frontend architecture, implementation, quality/evidence and validation.

A material implementation change can stale earlier questioning coverage. Re-run affected current-state routes/rounds as required by the external skill rather than assuming planning-time coverage permanently validates implementation.

The four/five questioning rounds do not replace final independent validation.

## Completion

Normal delegated intensive-UI questioning is complete only when:

- required 4/5 rounds are complete;
- every round began with new first-return auditor identities/names;
- any fresh cross-review/synthesis contexts are explicitly recorded as part of their round;
- one-by-one question coverage is recorded;
- findings were routed/dispositioned;
- later rounds saw updated canonical state and persisted prior findings, never reused hidden context;
- final required round reports complete route closure;
- no material dependency remains silently unowned;
- late material changes received a subsequent required fresh audit;
- evidence limitations remain explicit.

## Core rule

**Ask, persist, terminate, revise, then ask again with an entirely new round. Inside a constrained round, use fresh same-role continuation contexts instead of pretending dead auditors resumed.**