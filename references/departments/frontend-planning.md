# Frontend Planning Department

## Mission

Translate approved product/UI contracts into frontend technical architecture before production implementation, while keeping frontend architecture separate from UX/design, backend/data ownership, implementation and validation.

## Activation

Activate `frontend-architect` when frontend work has material structural decisions such as:

- multiple surfaces/modules/components;
- shared/local/server state ownership;
- asynchronous data flows;
- routing/layout/rendering boundaries;
- reusable frontend behavior;
- loading/empty/error integration;
- significant external integration seams.

Do not activate merely because a task touches frontend code. Tiny fully specified structural changes may use the documented trivial exception.

## Skill routing

All stable roles require `agent-context-foundation` for full-mode operation.

When architecture materially affects visible/perceptible behavior, also activate `intensive-ui-questioning` according to `references/skill-routing.md` and `references/ui-questioning-rounds.md`.

The UI skill is a procedure, not permission for `frontend-architect` to absorb UX, IA, visual, interaction, design-system or accessibility ownership.

## Atomic planning stage

For non-trivial frontend architecture:

1. create `frontend-architect` A+B;
2. give both the same canonical starting revision, upstream artifacts, objective and authority;
3. preserve initial isolation under `references/paired-delegation.md` and `references/batched-delegation.md`;
4. require independent `FRONTEND-ARCHITECTURE-PLAN` first returns;
5. compare agreements/contradictions/unique findings;
6. perform same-role cross-review;
7. route UX/IA/visual/interaction/accessibility/backend/API/data/security/performance questions to their actual owner or capability gap;
8. synthesize one canonical frontend architecture artifact.

Different specialties never substitute for A or B.

## Required upstream inputs

Use only applicable mature artifacts, but do not make frontend architecture invent missing material premises:

- product scope;
- applicable UX/IA/visual/interaction/design-system/accessibility artifacts;
- current frontend evidence;
- external contracts sufficiently stable for planned integration;
- runtime/framework/platform constraints.

If a required premise is material and missing, route it and block only the affected architecture portion.

## Intensive UI questioning integration

When active, use the current canonical external skill and repeated fresh-auditor protocol.

Within frontend-architecture authority, pressure-test:

- canonical UI/state ownership;
- loading/empty/error/result derivation;
- duplicate representations/actions;
- routing/navigation consequences at architecture level;
- responsive capability/component ownership;
- async feedback/blocking scope;
- reuse of existing primitives/components;
- overlay/layer/scroll ownership when architectural;
- rendered-state evidence obligations downstream.

A question owned by UX/IA/visual/interaction/accessibility/product/backend/etc. becomes a routed dependency, not a frontend-architect decision.

Material architecture changes can stale prior UI-questioning coverage; reopen only affected routes.

## Gate

Pass when:

- same-role A+B pairing is satisfied or a valid exception exists;
- module/component/state/data-flow/routing/rendering boundaries are explicit enough for implementation;
- approved upstream UI contracts are represented rather than reinterpreted;
- skill routes are complete/owner-routed/blocked as appropriate;
- external dependencies are stable or explicitly owned/blocked;
- contradictions are resolved/escalated;
- implementation ownership seams are explicit;
- no planner wrote production code.

## Downstream execution

Do **not** invent `frontend-implementer` or another ad-hoc Agent-Key.

Use the contracted `implementation-owner` role with a frontend-bounded manifest when production frontend work is ready:

```text
Agent-Key: implementation-owner
Assignment: <bounded frontend implementation ownership>
Production-Write-Authority: YES
```

Parallel implementation owners require genuinely separated workstreams/files/contracts and explicit integration ownership.

For visible/perceptible frontend implementation, quality and validation, keep `intensive-ui-questioning` active when required.

Use `quality-strategist` for verification strategy and `independent-validator` for final validation. Any missing security/performance/other specialty remains a capability gap until a stable profile exists; do not invent a role from the department text.

## Anti-patterns

Do not:

- create a generic `frontend-expert` owning UX + design + architecture + coding + validation;
- invent `frontend-implementer` without a stable profile;
- let frontend architecture silently redesign backend/API/data;
- count accessibility/backend/performance as the second frontend architect;
- resolve architecture during implementation because planning skipped it;
- use `intensive-ui-questioning` as permission to merge professions.

## Core principle

**Frontend architecture owns frontend structure; execution belongs to an explicit implementation owner, and adjacent specialties remain separately owned.**