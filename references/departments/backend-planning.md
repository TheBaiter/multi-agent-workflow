# Backend Planning Department

## Mission
Plan backend domain/service architecture before production implementation while keeping it separate from API, data/persistence, authentication, authorization, security, observability, performance, implementation, QA and the historical functional-backend-defect workflow.

## Activation
Activate `backend-architect` for material domain/service boundaries, business workflows, invariants, transactions, concurrency/idempotency, failure semantics or backend dependency direction. Do not activate solely because a task touches backend code. In-scope functional backend defects remain in the historical strict department.

## Atomic planning stage
For non-trivial backend architecture:
1. create `backend-architect` A+B;
2. give both the same canonical inputs/evidence/authority;
3. keep first construction isolated;
4. require independent `BACKEND-ARCHITECTURE-PLAN` returns;
5. compare agreements, contradictions and unique findings;
6. perform same-role cross-review;
7. route API/data/auth/security/observability/performance questions to contracted owners, or record capability gaps when no stable role exists;
8. synthesize one canonical backend architecture artifact.

Different specialties never replace A or B.

## Gate
Pass when domain/service/workflow boundaries are implementation-ready; material invariants, transaction boundaries, concurrency/idempotency and failure semantics are explicit; adjacent specialty decisions are stable/routed/capability-gapped; contradictions are resolved/escalated; implementation seams are identified; and no planner wrote production code.

## Downstream
Activate separately contracted API/data/auth/security/observability/performance planning only when material. Backend implementation begins only after the combined relevant plan is execution-ready. Final validation remains independent.

## Historical defect boundary
This is forward-looking general backend architecture. It does not replace or alias the historical `detective/analyzer/planner/challenger/test-strategist/executor/validator` workflow.

## Anti-patterns
Do not create a generic backend expert owning domain architecture, APIs, database, security, performance, implementation and validation. Do not let `backend-architect` absorb adjacent specialty contracts. Do not count a data/security/API specialist as the second backend architect.
