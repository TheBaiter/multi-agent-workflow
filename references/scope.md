# Backend Defect Specialization Scope

## Boundary

This file defines the scope of the **strict functional-backend-defect specialization** inside the broader multi-agent organization.

It is not the global scope of the whole skill.

The Orchestrator should load this contract only when it routes work into the backend-defect department.

## Primary target

This specialization is for **functional backend defects**.

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

The following are relevant to this specialization only when tied to a demonstrated functional defect:

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

"Service X has too many responsibilities" is not a backend functional defect.

"Because Service X commits state before required validation, callers can persist an impossible state" is a functional defect. The architecture may be part of the cause, but the Issue remains anchored to the functional failure.

Generic architecture, product discovery, feature planning, frontend work, and broad refactoring may still be valid work for the **general organization**; they simply do not enter this stricter department unless a functional backend defect is the governing problem.

## Out of specialization scope

Do not route into this strict workflow merely for:

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

These may be handled by other general roles/workflows when they are legitimate project objectives.

## Detective boundary

The Detective must not create a functional bug Issue simply because code looks suspicious.

A candidate needs:

1. an expected backend invariant or behavior;
2. evidence the implementation can violate it;
3. a plausible functional consequence.

If those cannot be established, mark the candidate DISCARDED, INCONCLUSIVE, or OUT_OF_SCOPE as appropriate.

## Scope expansion

If a later role discovers that the backend defect is broader than the current Issue:

- record the evidence;
- return the scope question to Analyzer;
- avoid silently expanding implementation;
- decide whether the same Issue remains coherent or a linked candidate Issue is needed according to repository policy.

If the work has actually become a broader product/architecture initiative rather than one coherent functional defect, return control to the Orchestrator so it can leave the specialization and choose the appropriate general workflow.

The backend specialization protects correctness; it does not define the limits of the overall organization.