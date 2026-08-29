# State Machine

## Allowed states

| State | Meaning |
| --- | --- |
| IDLE | role has no current useful action |
| INVESTIGATING | role is performing its required work |
| QUESTIONING | role has raised a material question |
| WAITING | role cannot continue until a response/evidence arrives |
| APPROVED | role explicitly accepts its owned responsibility |
| APPROVED_WITH_RISK | role accepts direction but a known risk remains unresolved for final consensus |
| REJECTED | role found a blocking contradiction or invalid premise |
| REOPENED | previously completed work became active due to new evidence/question |
| INCONCLUSIVE | evidence is insufficient for a defensible conclusion |
| BLOCKED | external constraint prevents useful progress |
| STATE_CONFLICT | duplicate logical state comments or equivalent ownership conflict detected |

## Transitions

Typical transitions:

~~~text
IDLE -> INVESTIGATING
INVESTIGATING -> APPROVED
INVESTIGATING -> REJECTED
INVESTIGATING -> INCONCLUSIVE
INVESTIGATING -> BLOCKED
APPROVED -> REOPENED
REOPENED -> INVESTIGATING
QUESTIONING -> WAITING
WAITING -> INVESTIGATING
~~~

Do not transition directly from a material unanswered QUESTION to APPROVED.

## Approval dormancy

APPROVED means the role is done **for the current evidence**.

After approval, do not keep producing commentary.

The role becomes logically dormant until a wake trigger occurs.

## Wake triggers

- direct question to Agent-Key;
- new evidence that affects owned assumptions;
- downstream rejection;
- failed test;
- implementation divergence;
- explicit RETURN event;
- final Validator challenge.

## Return targets

Return to the role that owns the failed premise rather than automatically blaming Executor.

Examples:

| Failure | Return target |
| --- | --- |
| original behavior may be intentional | detective / analyzer |
| cause wrong | analyzer |
| scope incomplete | analyzer |
| repair incomplete | planner |
| challenge procedure incomplete | challenger |
| verification strategy insufficient | test-strategist |
| code differs from plan | executor |

## Stale approvals

A prior APPROVED state becomes stale when a material premise it depended on changes.

The affected role should move to REOPENED and explicitly re-approve or reject after reviewing the new evidence.

Downstream roles that depended on the changed decision may also need reopening.

## Step 8 rollback

The close gate is not irreversible.

If final consensus review reveals a problem, return to any required earlier role, including Detective.

The workflow may discard the entire prior chain when the original candidate is disproven.
