# Frontend Planning Department

## Mission
Translate approved product/UI contracts into a frontend technical architecture before production implementation, while keeping frontend architecture separate from UX/design, backend/data ownership, implementation and validation.

## Activation
Activate `frontend-architect` when frontend work has material structural decisions: multiple surfaces, shared state, asynchronous data, routing/layout boundaries, rendering responsibilities, reusable behavior, or significant integration seams.

Do not activate merely because a task contains frontend code. Tiny fully specified changes may use the documented trivial exception.

## Atomic planning stage
For non-trivial frontend architecture:

1. create `frontend-architect` A+B;
2. give both the same canonical upstream artifacts and architecture objective;
3. keep initial work isolated;
4. require independent `FRONTEND-ARCHITECTURE-PLAN` returns;
5. compare unique findings and contradictions;
6. perform same-role cross-review;
7. route unresolved backend/API/data/security/performance questions to their owning roles rather than letting frontend architecture absorb them;
8. synthesize one canonical frontend architecture artifact.

Different specialties never replace A or B.

## Required upstream inputs
Use only applicable artifacts, but do not make frontend architecture invent missing material decisions:
- product scope;
- UX/IA/visual/interaction plans;
- design-system/accessibility constraints;
- existing frontend evidence;
- external API/data contracts sufficiently stable for the planned integration.

If a required upstream decision is material and missing, route it and hold the affected portion of the architecture.

## Gate
Pass when:
- same-role A+B pairing is satisfied or a valid trivial exception exists;
- module/component/state/data-flow/rendering boundaries are explicit enough for implementation;
- approved UI contracts are represented rather than silently reinterpreted;
- material external dependencies are stable or explicitly blocked/routed;
- contradictions are resolved/escalated;
- the canonical plan identifies implementation ownership seams;
- no frontend planner has written production code.

## Downstream
After the gate, create frontend implementation role(s) only for explicit, separable implementation ownership. Do not reactivate a planner as an implementer.

Implementation remains subject to independent review/validation and any required security, performance, QA or accessibility verification.

## Anti-patterns
Do not create a generic `frontend-expert` that owns UX, visual design, architecture, coding and validation. Do not let `frontend-architect` redesign backend/API/data contracts silently. Do not count an accessibility, backend or performance specialist as the second frontend architect. Do not use implementation to resolve architecture that should have been fixed at this gate.
