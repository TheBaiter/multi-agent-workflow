# Consensus and Closure

## Principle

The Issue closes only on **unanimous, explicit, evidence-backed agreement** from every required role.

The last agent is not a dictator.

## Required roles

Unless the repository explicitly defines a narrower valid workflow, the required Agent-Keys are:

- detective;
- analyzer;
- planner;
- challenger;
- test-strategist;
- executor;
- validator.

## Closable condition

All of the following must be true:

1. every required role has exactly one valid state comment;
2. every required role is currently APPROVED;
3. every APPROVED state contains a non-empty reason;
4. every APPROVED state cites useful evidence/anchors;
5. no material directed question remains unresolved;
6. no blocking event remains unresolved;
7. no approval is known to be stale because a dependent premise changed;
8. Validator completed its current ten-pass cycle against the current implementation;
9. the implementation under review is the implementation described by Executor;
10. every material test case is documented with its validation mode (EXECUTED, DOCUMENTATION_BACKED, or MIXED), evidence, result, and limitations;
11. documentation-backed cases cite authoritative applicable anchors rather than claiming fictional execution;
12. closure reason can be explained without relying on hidden chat context.

APPROVED_WITH_RISK is not final consensus.

If a risk is acceptable, it must be explicitly resolved and the role must move to APPROVED with the acceptance reason recorded.

## Consensus snapshot

Before closure, create a permanent CONSENSUS event that records the current State-Revision of each required role.

Example:

~~~text
MAW-EVENT
Event-Type: CONSENSUS

detective: APPROVED @ revision 3
analyzer: APPROVED @ revision 9
planner: APPROVED @ revision 7
challenger: APPROVED @ revision 4
test-strategist: APPROVED @ revision 6
executor: APPROVED @ revision 5
validator: APPROVED @ revision 11

DECISION
Issue is closable.

REASON
...

EVIDENCE
- ...
~~~

This snapshot makes the exact agreement auditable without relying on mutable comments alone.

## Disagreement

If two roles disagree:

- do not average their confidence;
- do not let the later role override automatically;
- identify who owns the disputed premise;
- exchange QUESTION / ANSWER / CHALLENGE events;
- resolve through evidence;
- keep the Issue open while material disagreement remains.

## Silence

Silence never equals consensus.

IDLE, WAITING, BLOCKED, INCONCLUSIVE, REJECTED, REOPENED, QUESTIONING, STATE_CONFLICT, or APPROVED_WITH_RISK prevent closure.

## Reopen after consensus

If new material evidence appears after consensus but before closure, invalidate the consensus snapshot and reopen affected roles.

If the Issue is already closed and a real contradiction appears, follow repository policy to reopen or create a linked regression Issue; never hide the new evidence to preserve the prior conclusion.
