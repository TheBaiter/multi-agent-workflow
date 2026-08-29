# State Machine

## Allowed states

| State | Meaning |
| --- | --- |
| IDLE | role has no current useful action |
| INVESTIGATING | role is performing its required work |
| QUESTIONING | role has raised a material question |
| WAITING | role cannot continue until a response/evidence arrives |
| WAITING_FOR_MANUAL_IMPLEMENTATION | automated workflow is paused until the manual owner provides an implementation handoff |
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
APPROVED(test-strategist) -> WAITING_FOR_MANUAL_IMPLEMENTATION
WAITING_FOR_MANUAL_IMPLEMENTATION -> INVESTIGATING(validator)
~~~

Do not transition directly from a material unanswered QUESTION to APPROVED.

## Maturity invariant

For any fixed-pass role:

- passes below N/N must remain `Assessment-Maturity: PROVISIONAL`;
- `APPROVED` is valid only at N/N with `Assessment-Maturity: FINAL`;
- `REJECTED`, `INCONCLUSIVE`, or `BLOCKED` may be discussed provisionally before N/N, but they acquire normal handoff/terminal authority only when FINAL, except when an external blocker makes completion physically impossible;
- downstream roles remain WAITING until the upstream role satisfies its configured final-pass gate.

A project-specific orchestration that raises the pass count also raises the maturity gate. For example, if Analyzer is configured for 16 passes, 8/16 is not final even though the base profile normally has 8 passes.

## Maturity transition guard

For fixed-pass roles, `APPROVED` is valid only when:

- the configured pass count is complete at N/N;
- `Assessment-Maturity: FINAL`;
- the final synthesis exists;
- the terminal decision includes reason and evidence.

`PROVISIONAL -> APPROVED` before N/N is an invalid transition.

A role may expose strong provisional findings or raise blocking questions before N/N, but those findings do not create downstream handoff authority.

If a role cannot complete the required passes because of a real external constraint, use BLOCKED rather than manufacturing FINAL approval.

## Approval dormancy

APPROVED means the role is done **for the current evidence** and its Assessment-Maturity is FINAL.

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


## Manual implementation transition

When `Execution-Mode: MANUAL_OWNER`, Test Strategist approval does not activate an Executor agent.

The workflow enters `WAITING_FOR_MANUAL_IMPLEMENTATION`.

It may leave that state only when a valid `MANUAL_IMPLEMENTATION` event identifies the implementation anchor and declares `READY_FOR_VALIDATOR: YES`.

The next active agent is Validator.

If the manual handoff changes a material plan premise, reopen the responsible upstream role instead of advancing directly to validation.
