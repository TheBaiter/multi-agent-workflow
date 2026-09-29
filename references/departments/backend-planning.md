# Backend Planning Department

## Mission

Plan backend domain/service architecture before production implementation while keeping it separate from API, data/persistence, authentication, authorization, security, observability, performance, implementation, QA and the historical functional-backend-defect workflow.

## Activation

Activate `backend-architect` for material decisions about:

- domain/service responsibility boundaries;
- business workflows;
- domain invariants;
- transaction boundaries;
- concurrency/idempotency requirements;
- failure/recovery semantics;
- backend dependency direction.

Do not activate merely because a task touches backend code.

Functional backend defects that match the historical strict scope remain in the specialized defect department.

## Atomic planning stage

For non-trivial backend architecture:

1. create `backend-architect` A+B;
2. give both the same frozen canonical inputs/evidence/authority;
3. preserve initial isolation under pairing/batching rules;
4. require independent `BACKEND-ARCHITECTURE-PLAN` first returns;
5. compare agreements/contradictions/unique findings;
6. perform same-role cross-review;
7. route API/data/auth/security/observability/performance questions to stable contracted owners or capability gaps;
8. synthesize one canonical backend architecture artifact.

Different specialties never replace A or B.

## Gate

Pass when:

- domain/service/workflow boundaries are implementation-ready;
- material invariants and transaction boundaries are explicit;
- concurrency/idempotency requirements are explicit;
- failure/recovery responsibilities are explicit;
- adjacent specialty decisions are stable, routed or capability-gapped;
- contradictions are resolved/escalated;
- implementation ownership seams are identified;
- no planner wrote production code.

## Adjacent specialties

`backend-architect` does **not** own:

- public API/transport/versioning;
- persistence/data/schema/index/migration design;
- authentication;
- authorization;
- security/threat modeling;
- observability;
- performance;
- implementation;
- QA/final validation.

Activate an adjacent specialty only if its stable role contract exists. Otherwise record a capability gap; do not invent an Agent-Key and do not widen `backend-architect`.

## Downstream execution

Do **not** invent a `backend-implementer` Agent-Key.

Use the contracted `implementation-owner` with a backend-bounded manifest when the required plans are execution-ready:

```text
Agent-Key: implementation-owner
Assignment: <bounded backend implementation ownership>
Production-Write-Authority: YES
```

When multiple specialist technical artifacts must be reconciled before execution, route them through `technical-planner` **only for cross-specialty integration/sequencing**, not as a replacement for the missing specialty.

Use `quality-strategist` for verification strategy and `independent-validator` for final judgment.

## Historical defect boundary

This department is forward-looking general backend architecture.

It does not replace or alias the historical:

`detective -> analyzer -> planner -> challenger -> test-strategist -> executor -> validator`

workflow.

## Anti-patterns

Do not:

- create a generic backend expert owning domain + APIs + database + security + performance + coding + validation;
- invent `backend-implementer` without a profile;
- let `backend-architect` absorb an uncontracted specialty;
- count a data/security/API specialist as the second backend architect;
- use implementation to discover architecture that should have been fixed at this gate.

## Core principle

**Backend architecture owns domain/service structure deeply; adjacent specialties and production execution remain separately owned.**