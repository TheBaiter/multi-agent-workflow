# GitHub Issue Protocol

## Purpose

The Issue is the authoritative shared case file for one defect investigation.

All subagents may authenticate through the same GitHub account. Therefore the GitHub author does not identify the logical agent.

## Minimum case record

Following $agent-context-foundation task-traceability principles, the Issue or repository-authoritative task record must preserve enough context for a new subagent to resume without private chat history.

Before substantial downstream work, ensure the record contains:

- goal / functional defect candidate;
- current status;
- accepted scope and explicit out-of-scope boundary;
- success criteria / backend invariant to restore;
- known constraints and assumptions;
- current handoff / owning Agent-Key;
- next useful action.

During the workflow, preserve material changes to plan, evidence, decisions, blockers, verification, and handoff.

Do not create a second planning/history system under Agent/ or elsewhere merely to mirror the Issue.

## State comment ownership

Each role owns exactly one editable state comment identified by Agent-Key.

Required header:

~~~text
Agente: <display name>
Agent-Key: <stable key>
Rol: <role>
Estado: <state>
Paso: <current pass>
Assessment-Maturity: <PROVISIONAL | FINAL>
State-Revision: <integer>
~~~

The display name is human-facing.

Agent-Key is protocol identity.

## Locating your state

Before editing:

1. read the Issue comments;
2. find comments containing exactly your Agent-Key declaration;
3. if zero exist, create your state comment;
4. if exactly one exists, read and update it;
5. if more than one exists, do not edit either; create a STATE_CONFLICT event and stop state mutation until duplication is resolved.

Do not depend on remembering comment_id between runs.

The implementation may use comment_id after locating the correct comment, but comment_id is not persistent agent identity.

## Edit boundary

An agent may:

- read all state comments;
- read all permanent events;
- quote or reference another agent;
- ask another agent a question;
- answer questions directed to itself.

An agent must **never edit another Agent-Key's state comment**.

## Progressive findings contract

Each role's editable state comment is a living cumulative report.

Every execution that learns something about the active Issue must update that same comment with a compact `FINDINGS SO FAR` section.

Rules:

1. Preserve the useful conclusions from earlier passes.
2. Add new evidence and explicitly mark earlier findings as CONFIRMED, MODIFIED, REJECTED, or STILL_UNCERTAIN when later passes change them.
3. Do not create a fresh state comment per pass.
4. Do not hide contradictions discovered later.
5. Keep exact evidence anchors for material findings.
6. Intermediate findings remain `Assessment-Maturity: PROVISIONAL`.
7. A role with N required passes may set `Assessment-Maturity: FINAL` only at N/N after synthesizing all passes.
8. Downstream roles may inspect provisional findings for context or raise a directed question, but they may not start their normal stage based on them.
9. A terminal role decision has workflow authority only when maturity is FINAL.
10. An early serious contradiction may be recorded and challenged immediately, but it does not become the role's final verdict until the configured pass requirement is completed, unless the workflow is externally BLOCKED and cannot physically continue.

The purpose is to make each comment increasingly valuable as evidence accumulates, while preventing a 1/N or 3/N snapshot from being mistaken for the role's completed judgment.

## Per-run checkpoint contract

The Issue is the continuity layer between executions and between chats.

Every execution that selects or inspects an active Issue must update the executing role's state comment before finishing, even if it cannot advance because another role owns the current stage.

This is a checkpoint, not approval and not a permanent event.

Recommended checkpoint fields:

~~~text
Last-Checkpoint: <ISO timestamp>
Workflow-Owner: <Agent-Key | MANUAL_OWNER | CLOSE_GATE>
Waiting-On: <Agent-Key | MANUAL_IMPLEMENTATION | NONE>
Next-Trigger: <specific condition that permits useful work>
~~~

Rules:

1. If the role has not started yet, create or maintain its state as WAITING with `Paso: 0/N`.
2. If the role is active, record the current pass and next useful action.
3. If the role is APPROVED and dormant, keep APPROVED but refresh Last-Checkpoint and record the current downstream owner.
4. If there is no change in decision/evidence/state/pass, do not create a permanent event just to report inactivity.
5. A pure checkpoint refresh does not need to increment State-Revision. Increment State-Revision when position, evidence, assumptions, decision, state, or pass materially changes.
6. Never overwrite another Agent-Key's checkpoint/state.
7. The checkpoint must be sufficient for a fresh execution in another chat to understand where this role stands without private conversation history.

An execution must not end with "no useful work" while leaving no durable indication of where the role is waiting on an active workflow Issue.

## State comment content

Recommended compact form:

~~~text
Agente: V
Agent-Key: planner
Rol: Planner
Estado: INVESTIGATING
Paso: 3/5
Assessment-Maturity: PROVISIONAL
State-Revision: 6
Last-Checkpoint: 2026-08-29T19:00:00-03:00
Workflow-Owner: analyzer
Waiting-On: analyzer
Next-Trigger: analyzer APPROVED or directed question

POSITION
...

FINDINGS SO FAR
- ...

EVIDENCE
- ...

ASSUMPTIONS
- ...

OPEN QUESTIONS
- ...

LAST DECISION
...

REASON
...

NEXT
...
~~~

Increment State-Revision on every material state update.

### Same-agent collision guard

Before overwriting its own state comment, an agent should re-read that comment and confirm its current State-Revision still matches the revision it based its work on.

If the revision changed:

- do not overwrite the newer state;
- re-read the Issue and new evidence;
- reconsider the pending update;
- then write a new revision only if still valid.

This protects two concurrent executions of the **same Agent-Key** from silently overwriting one another.

Do not use the state comment as an exhaustive command log.

## Permanent events

Use a new comment for a material event that must remain traceable:

- directed QUESTION;
- ANSWER;
- CHALLENGE;
- REJECTION;
- NEW_EVIDENCE;
- RETURN;
- REOPEN;
- RESOLUTION;
- CONSENSUS snapshot;
- STATE_CONFLICT.

Do not rewrite permanent event comments.

## Event contract

Recommended form:

~~~text
MAW-EVENT
Event-Type: QUESTION
From-Agent: validator
To-Agent: planner
In-Reply-To: <event key if applicable>

DECISION / QUESTION
...

REASON
...

EVIDENCE
- ...

IMPACT
...
~~~

Use a unique Event-Key when the host can safely create one. When not practical, the event comment URL itself is sufficient as the durable event identity.

## Directed questions

A directed question targets a single owning Agent-Key whenever possible.

The recipient must:

1. wake from dormancy;
2. read the question and cited evidence;
3. update its own state to REOPENED, INVESTIGATING, or QUESTIONING as appropriate;
4. re-check the owned premise;
5. answer through a permanent event;
6. state whether its previous approval survives.

Possible answers include:

- CONFIRMED: prior decision survives, with evidence;
- MODIFIED: conclusion changes but stage can still approve after re-evaluation;
- REJECTED: prior decision was wrong;
- INCONCLUSIVE: insufficient evidence.

## No approval by silence

No response, timeout, inactivity, or absence of objection counts as approval.

A directed material question remains blocking until explicitly resolved.

## Traceability rule

State tells **where an agent stands now**.

Events tell **how the case changed over time**.

Do not sacrifice either layer.


## Manual implementation handoff

An Issue may declare:

~~~text
Execution-Mode: MANUAL_OWNER
Implementation-Owner: repository owner / human
~~~

In this mode, `executor` is not an active required Agent-Key.

After Test Strategist approval, automated roles must wait. No agent may implement the planned source change unless the execution mode is explicitly changed.

When the human implementation is ready for validation, add a permanent event:

~~~text
MAW-EVENT
Event-Type: MANUAL_IMPLEMENTATION

Execution-Mode: MANUAL_OWNER
Implementation-Ref: <commit SHA, PR, branch+SHA, or other immutable repository anchor>

CHANGE SUMMARY
- ...

PLAN DEVIATIONS
- NONE
  or
- ...

VERIFICATION ALREADY PERFORMED
- ...

KNOWN LIMITATIONS
- ...

READY_FOR_VALIDATOR
YES
~~~

`Implementation-Ref` must identify the exact repository state Trish should validate. A vague statement such as "I fixed it" is insufficient.

Validator must not begin implementation-sensitive passes until `READY_FOR_VALIDATOR: YES` and a usable implementation anchor exist.

If Validator finds an implementation-only defect in MANUAL_OWNER mode, create a permanent return/question event addressed to the manual implementation owner. Do not create or edit an executor state comment.

If the manual implementation changes the approved plan materially, Planner and any dependent roles become stale and must be reopened before validation can continue.
