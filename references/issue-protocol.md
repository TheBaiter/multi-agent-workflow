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

## State comment content

Recommended compact form:

~~~text
Agente: V
Agent-Key: planner
Rol: Planner
Estado: INVESTIGATING
Paso: 3/5
State-Revision: 6

POSITION
...

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
