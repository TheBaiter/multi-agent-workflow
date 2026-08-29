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
6 Executor / Reducer
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
- Executor cannot implement plan without changing contract -> Planner and possibly Analyzer;
- Validator finds code differs from plan -> Executor.

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
