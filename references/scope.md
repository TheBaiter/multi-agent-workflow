# Scope

## Primary target

This skill is for **functional backend defects**.

A candidate must involve an incorrect backend outcome, violated invariant, invalid state, broken contract, incorrect persistence behavior, or equivalent functional consequence.

## In scope

Typical examples:

- wrong business-rule result;
- state transition that should be impossible;
- missing/incorrect persistence;
- data integrity violation;
- transaction behavior that leaves inconsistent state;
- incorrect retries/idempotency with functional impact;
- migration that corrupts, drops, mis-shapes, or misinterprets data;
- schema/contract mismatch producing incorrect backend behavior;
- backend service integration that violates expected behavior;
- regression affecting backend functionality;
- concurrency/order behavior that changes functional correctness.

## Conditionally in scope

The following are relevant only when tied to a demonstrated functional defect:

- architecture;
- structural design;
- responsibility boundaries;
- performance;
- caching;
- error handling;
- dependency versions;
- migrations and schemas;
- technical debt.

Example:

"Service X has too many responsibilities" is not a defect.

"Because Service X commits state before required validation, callers can persist an impossible state" is a functional defect. The architecture may be part of the cause, but the Issue remains anchored to the functional failure.

## Out of scope

Do not use this workflow merely for:

- frontend/UI/CSS;
- visual regressions;
- code cleanup;
- simplification without correctness impact;
- generic refactoring;
- naming;
- formatting;
- lint/style concerns;
- duplicate code;
- complexity alone;
- architecture smell alone;
- speculative redesign;
- optimization without a demonstrated correctness failure.

## Detective boundary

The Detective must not create a functional bug Issue simply because code looks suspicious.

A candidate needs:

1. an expected backend invariant or behavior;
2. evidence the implementation can violate it;
3. a plausible functional consequence.

If those cannot be established, mark the candidate DISCARDED, INCONCLUSIVE, or OUT_OF_SCOPE as appropriate.

## Scope expansion

If a later role discovers that the problem is broader than the current Issue:

- record the evidence;
- return the scope question to Analyzer;
- avoid silently expanding implementation;
- decide whether the same Issue remains coherent or a linked candidate Issue is needed according to repository policy.

The workflow protects correctness, not Issue size for its own sake.
