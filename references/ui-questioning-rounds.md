# Intensive UI Questioning — Fresh Round Integration

## Purpose

This contract tells Morrison how to execute the external `intensive-ui-questioning` skill inside the multi-agent organization without weakening its required fresh-review behavior or breaking atomic role ownership.

Canonical external source:

- Repository: `https://github.com/TheBaiter/intensive-ui-questioning`
- Entrypoint: `SKILL.md`
- Delegated audit contract: `references/subagent-question-audit.md`
- Fresh-round contract: `references/fresh-questioning-rounds.md`

Always read the current external sources when activated. This local contract defines organization/runtime integration only.

## Activation

Activate for meaningful visible/perceptible UI/frontend work according to `references/skill-routing.md`.

For non-trivial delegated use, Morrison must not treat `intensive-ui-questioning` as one pass attached to a planner. It creates a dedicated question-audit workstream.

## Atomic audit role

Use stable Agent-Key:

`ui-question-auditor`

Profile:

`references/profiles/ui-question-auditor/PROFILE.md`

The auditor owns only:

- intensive-UI route/question coverage;
- one-by-one question status;
- dependency discovery;
- contradiction/omission detection;
- evidence-boundary checks;
- round closure reporting.

It does not own UX, IA, visual design, interaction design, accessibility policy, frontend architecture, implementation or final product authority. Findings are routed to those owners.

## Fresh round budget

For ordinary non-trivial visible/perceptible work:

- `Required-UI-Questioning-Rounds: 4`.

Use:

- `Required-UI-Questioning-Rounds: 5`

when one or more are true:

- broad redesign or new major surface;
- several specialized question packs are active;
- user flow/state/accessibility interactions are complex;
- rework would be expensive;
- previous UI work showed late regressions or missed questions;
- round 4 still creates a material new finding or plan change.

Do not use unlimited loops. A fundamental unresolved flaw found in round 5 returns work to the owning planner/decision gate instead of manufacturing a PASS.

## Fresh identity invariant

Every round creates completely new runtime instances.

Example:

```text
Round 1
- ui-question-auditor-r1-a
- ui-question-auditor-r1-b

Round 2
- ui-question-auditor-r2-a
- ui-question-auditor-r2-b

Round 3
- ui-question-auditor-r3-a
- ui-question-auditor-r3-b

Round 4
- ui-question-auditor-r4-a
- ui-question-auditor-r4-b
```

The stable Agent-Key remains `ui-question-auditor`; the concrete `Agent-Instance` and `Instance-Name` must be unique.

Never:

- resume a terminated round auditor;
- reuse its runtime ID;
- recreate a later auditor under the same instance name;
- retain an auditor merely to preserve memory.

If the host cannot provide new identities, record `Fresh-Round-Guarantee: REDUCED | BLOCKED` and do not claim the normal independent-round contract was satisfied.

## Pairing inside a round

The organization's same-role pairing rule still applies.

For non-trivial work, normally create `ui-question-auditor` A+B in each round with:

- same Agent-Key;
- same current canonical starting revision;
- same round number;
- comparable reasoning class;
- initial isolation.

When a large route requires more coverage, add more fresh auditors in the same round and partition by stage/pack/component/evidence responsibility. Do not create one overloaded auditor merely to save slots.

Slot constraints are handled through `references/batched-delegation.md`. The organization may run the auditors in bounded compatible batches, but every round's outputs must be committed before its contexts are terminated and the next round starts.

## Context continuity without context reuse

Round N receives the latest canonical state produced after earlier rounds:

- objective and fixed user/product decisions;
- current UI/product/architecture plan;
- current implementation when auditing implemented work;
- current intensive-UI route and active packs;
- prior round question IDs/findings;
- owner dispositions;
- changes caused by those findings;
- unresolved owner questions;
- source/rendered/runtime evidence anchors;
- current verification expectations.

Do not give the next round hidden reasoning transcripts from earlier auditors.

Continuity is carried by canonical questions, decisions, evidence, artifacts and round receipts under `agent-context-foundation`, not by reusing an old conversation.

## Round lifecycle

```text
CURRENT CANONICAL STATE
        ↓
Morrison creates fresh ui-question-auditor A+B
        ↓
auditors load current intensive-ui-questioning sources
        ↓
questions are processed ONE BY ONE
        ↓
A/B returns + same-role comparison/cross-review
        ↓
UI-QUESTIONING-ROUND receipt committed
        ↓
findings routed to owning planners/roles
        ↓
owners disposition / revise canonical artifact
        ↓
all round auditor contexts TERMINATED
        ↓
next round starts with NEW identities
```

## Question granularity

Every applicable question remains individually observable.

Use states compatible with the external skill:

- `ANSWERED`;
- `NOT_APPLICABLE: <grounded reason>`;
- `OWNER_REQUIRED: <decision>`;
- `FAILED_INTEGRITY: <evidence>`;
- `BLOCKED: <reason>`.

Do not replace several questions with a summary such as `UX looks correct`.

When a question discovers another specialty, route it. The auditor does not become that specialist.

## Progressive repetition

The rounds are not identical copies.

Round 1 establishes current route coverage.

Round 2 receives the plan revised from round 1 and questions the new state.

Round 3 reviews the consequences of round-2 additions/removals/decisions and searches for newly activated routes, ownership conflicts and unnecessary complexity.

Round 4 is another fresh pass over the now-mature artifact and must be capable of rejecting decisions that survived merely through shared framing.

Round 5, when required, is the final fresh challenge of the changed/high-risk state.

Each round re-traverses the external router sufficiently to detect routes that became active because earlier rounds changed the artifact.

## Canonical state record

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

Each round receipt should preserve:

```text
UI-QUESTIONING-ROUND
Round: <n>
Fresh-Agent-Instances: <unique names/ids>
Started-From: <canonical revision>
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

## Interaction with planners

UI planning roles still own the decisions in their professions.

Example:

```text
UX Planner A+B
      ↓
UX plan draft
      ↓
UI Question Audit Round 1 A+B
      ↓
UX-owned findings -> UX Planner/owner
Accessibility finding -> Accessibility Planner
IA finding -> IA Planner
      ↓
canonical revisions
      ↓
UI Question Audit Round 2 NEW A+B
```

The auditor questions and routes; it does not redesign everything itself.

## Interaction with later phases

`intensive-ui-questioning` remains active when the work stays visible/perceptible through frontend architecture, implementation, QA and validation.

A material implementation change can make previous questioning coverage stale. Re-run the affected current-state questioning rounds as required by the external skill rather than assuming planning-time coverage permanently validates implementation.

Do not confuse the four/five questioning rounds with final independent validation. Final validation remains a separate role/gate.

## Completion

Normal delegated intensive-UI questioning is complete only when:

- the required four/five fresh rounds are complete;
- every round used new unique runtime identities/names;
- one-by-one question coverage is recorded;
- findings were routed and dispositioned;
- later rounds saw the updated canonical artifact and prior persisted findings;
- the final required round reports complete route closure;
- no material new dependency is silently unowned;
- any late material plan change received a subsequent fresh audit;
- evidence limitations remain explicit.

## Core rule

**Do not ask once and remember. Ask, persist, terminate, revise, then ask again with a different agent. Repeat four or five times against the progressively improved artifact.**