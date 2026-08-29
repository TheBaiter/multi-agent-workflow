# Workflow

## Normal direction

~~~text
1 Detective
    ↓
2 Analyzer
    ↓
3 Planner
    ↓
4 Challenger
    ↓
5 Test Strategist
    ↓
6 Implementation
    ├─ AGENT_EXECUTOR -> Executor / Reducer
    └─ MANUAL_OWNER  -> Human / repository owner
    ↓
7 Final Validator
    ↓
8 Consensus / Close
~~~

This is a normal direction, not a linear guarantee.

## Core rule

Every downstream output is allowed to question upstream conclusions.

Previous approval is evidence of prior review, not immunity from new evidence.

## Pass semantics

Pass counts mean distinct investigation purposes.

They do not mean:

- repeat the same prompt;
- restate the same conclusion;
- search the same files eight times;
- force APPROVED after the final number.

A role may finish its required passes and still conclude REJECTED, INCONCLUSIVE, or BLOCKED.

## Dormancy

When a role finishes and sets APPROVED, it becomes dormant for that Issue.

A dormant role should not keep commenting or recomputing merely because another agent is working.

Wake it only when:

- a directed question targets its Agent-Key;
- material new evidence affects one of its decisions;
- a test fails against its premise;
- implementation diverges from its owned decision;
- a later role explicitly returns the case.

## Backward return

Any later stage can return to the owner of a failed premise.

Examples:

- Validator discovers the original behavior is documented as intentional -> Detective/Analyzer;
- Test Strategist discovers scope not modeled -> Analyzer;
- Challenger finds an unhandled repair branch -> Planner;
- Agent Executor cannot implement plan without changing contract -> Planner and possibly Analyzer;
- Manual owner reports that the plan cannot be implemented as written -> Planner and possibly Analyzer;
- Validator finds code differs from plan -> Executor when AGENT_EXECUTOR, or manual implementation handoff/owner when MANUAL_OWNER.

Returning backward invalidates downstream conclusions that depended on the changed premise.

Those roles must be re-evaluated before closure.

## Cost principle

Do not continue a wrong path because it was expensive.

Tokens spent, number of passes completed, implemented lines, or prior approvals are not evidence.

## Efficiency principle

The workflow is expensive by design, but should avoid waste:

- load only the current role profile;
- reuse Issue evidence rather than rediscovering everything;
- run differentiated passes;
- keep state comments compact;
- use permanent events only for material transitions;
- reactivate only affected roles.


## Manual implementation mode

When `Execution-Mode: MANUAL_OWNER`:

1. Test Strategist finishes and APPROVES the verification contract.
2. The automated workflow enters `WAITING_FOR_MANUAL_IMPLEMENTATION`.
3. No agent edits source code on behalf of the Executor role.
4. The repository owner implements the change.
5. The Issue receives a durable `MANUAL_IMPLEMENTATION` handoff identifying the exact code state to validate.
6. Validator wakes and validates that implementation.
7. If Validator finds an implementation-only defect, it returns to the manual owner through a permanent event rather than waking Executor.
8. If the implementation exposes a plan/scope/test defect, return to the responsible agent role normally.

Manual ownership removes automated implementation; it does not remove evidence, test, or validation requirements.


## Cross-chat continuity

Do not assume the next execution shares the current chat context.

The authoritative Issue must therefore expose the current position of every automation/role that has inspected the active case.

Each execution refreshes its own state comment checkpoint, including while WAITING or dormant. This makes the workflow reconstructable from GitHub alone.

Waiting is a real state and should be visible. Silence between executions must not be used as the only representation of waiting.
