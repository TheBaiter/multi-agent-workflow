# External Skill Routing

## Purpose

Roles define **who owns a decision**. Skills define **procedures the owner/audit workstream must follow**.

Loading a skill never grants another profession's authority, changes `Production-Write-Authority`, or creates an undocumented Agent-Key.

Morrison resolves/install-checks skill dependencies and attaches them to manifests. The role/audit owner executes the procedure inside its authority.

Read `references/installation-and-dependencies.md` first.

## Manifest skill contract

Every stable child manifest exposes:

```text
Required-Skills:
- Skill: <name>
  Source: <resolved current source | NONE>
  Status: AVAILABLE | MISSING | BLOCKED
  Coverage: <FULL_ENTRYPOINT | ROUTED_SUBSET | assignment-specific rule>

Conditional-Skills:
- Skill: <name>
  Source: <resolved current source | NONE>
  Status: ACTIVE | NOT_ACTIVE | MISSING | BLOCKED
  Activate-When: <condition>
  Coverage-Anchor: <receipt/artifact | NONE>

Context-Checkpoint-Target: <canonical owner/anchor>
```

At task level preserve:

`Skill-Dependency-Mode: FULL | REDUCED | BLOCKED`

A repository URL/profile mention/remembered summary is provenance, not proof that a current procedure is readable.

## Spawn-time preflight

Before a stable child starts:

1. select atomic role/assignment;
2. resolve inherited required skills;
3. evaluate conditional activation;
4. verify actual current source availability;
5. record `AVAILABLE | MISSING | BLOCKED | NOT_REQUIRED` semantics;
6. write skill fields + checkpoint target to manifest;
7. only then spawn.

A child cannot silently downgrade a required dependency after spawn.

If a required current source is unavailable, mark the dependent path reduced/blocked and do not reconstruct it from memory.

# Organization-wide baseline — `agent-context-foundation`

Canonical source:

- Repository: `https://github.com/TheBaiter/agent-context-foundation`
- Entrypoint: `SKILL.md`

For full-mode operation, every stable role requires the current canonical skill.

It governs context/memory discipline such as:

- minimum viable context / progressive disclosure;
- authoritative task traceability for meaningful work;
- one canonical owner for durable knowledge;
- separation of active task history from reusable memory;
- `discovered -> candidate -> verified -> durable` promotion;
- stale/superseded memory retirement;
- exact source/test/owner/handoff anchors;
- issue/task-first handling for meaningful discovered defects when a tracker exists;
- distinct discovery/planning/implementation/revalidation checkpoints;
- resumable handoffs;
- no secrets/private customer data in reusable memory.

## Active duty

A stable child with this skill `AVAILABLE` must actively apply the relevant subset:

1. load only context needed for its bounded assignment;
2. keep active chronology/progress in the authoritative task/state;
3. preserve evidence/owner/handoff anchors;
4. distinguish temporary hypotheses from verified reusable findings;
5. promote reusable knowledge only after verification and to one canonical owner;
6. retire/supersede stale knowledge;
7. checkpoint material results before return;
8. terminate rather than remain alive as memory.

Morrison owns organization-wide orchestration state. Role owners own only their authoritative task/artifact surface.

Thinkers are disposable and do not maintain durable memory; their parent decides how a returned question/finding is persisted.

If `agent-context-foundation` is missing/blocked, follow `references/installation-and-dependencies.md` and do not claim its guarantees.

# UI procedure — `intensive-ui-questioning`

Canonical source:

- Repository: `https://github.com/TheBaiter/intensive-ui-questioning`
- Entrypoint: `SKILL.md`
- Delegated audit procedure: external `references/subagent-question-audit.md`
- Fresh-round procedure: external `references/fresh-questioning-rounds.md`
- MAW integration: local `references/ui-questioning-rounds.md`

Activate for meaningful visible/perceptible UI/frontend work. Do not activate for purely backend/data work with no visible/perceptible consequence.

This is a live procedure, not remembered UI advice.

## Two layers of UI skill responsibility

### Layer 1 — role-local responsibility

UI/product/frontend/quality/implementation/validation roles may have `intensive-ui-questioning` active for their assignment.

Each such role:

- reads the current entrypoint/procedure necessary for its assignment;
- answers only decisions/evidence inside its profession;
- routes every neighboring profession's decision;
- preserves skill-derived findings/checkpoints;
- never claims whole-task route closure merely because its local subset is complete.

Commonly activated roles include:

- `ux-planner`;
- `information-architecture-planner`;
- `graphic-design-planner`;
- `interaction-design-planner`;
- `design-system-planner`;
- `accessibility-planner`;
- `frontend-architect` when visible behavior is structurally affected;
- `implementation-owner` for visible frontend execution;
- `quality-strategist` for UI verification strategy;
- `independent-validator` for visible UI validation;
- reopening reviewers when their target is UI-facing.

### Layer 2 — task-level complete coverage owner

For **non-trivial delegated intensive-UI work**, MAW must have one explicit task-level coverage owner per round.

That responsibility belongs to the `ui-question-auditor` Pair-Group's **same-role synthesis owner** (`Pair-Position: SYNTHESIS`, or an original same-role member legitimately acting as synthesis owner).

The round coverage owner must satisfy the external skill's “main agent” accountability for that round:

1. read the current external `SKILL.md` entrypoint completely;
2. read the current external `references/questions/INDEX.md` routing inventory completely;
3. verify every materially plausible route is classified `ACTIVE` or grounded `NOT_ACTIVE` when ambiguity would otherwise remain;
4. reconcile all delegated/scoped auditor outputs;
5. verify every activated pack/source has an explicit owner and complete delegated/read receipt;
6. ensure each applicable question is individually dispositioned;
7. follow newly activated dependencies until route closure or explicit block;
8. inspect/re-read any contested/material source needed to resolve coverage disputes;
9. emit the canonical round receipt and `ROUTE_CLOSURE` result.

Morrison schedules and records this work but **does not** substitute itself for the UI coverage owner or invent UI decisions.

Individual planners/auditors may cover routed subsets. Only the designated round synthesis owner may claim task-level complete route coverage for that round.

## Fresh questioning rounds

For non-trivial delegated UI work:

- 4 fresh rounds by default;
- 5 for broad/high-risk/rework-prone work or when round 4 still introduces a material change/finding;
- each round starts with new first-return auditor identities/names;
- questions are processed one by one;
- prior continuity comes from canonical findings/dispositions, never hidden prior auditor context;
- each round gets its own complete-coverage synthesis owner/receipt;
- all round contexts terminate before the next round begins;
- Round N+1 audits the updated artifact, not the previous artifact.

Use `references/ui-questioning-rounds.md` for slot/pair mechanics.

Do not claim full delegated IUQ coverage from one pass or from several local planners whose outputs were never reconciled by a complete coverage owner.

## Role-purity interaction

The external UI skill spans many question domains; that breadth is a routing surface, not a composite profession.

Examples:

- UX owns journey/usability decisions;
- IA owns hierarchy/navigation/findability;
- Graphic Design owns visual communication;
- Interaction owns control/state mechanics;
- Accessibility owns accessibility requirements;
- Frontend Architect owns frontend structure;
- UI Question Auditor owns question/route/evidence coverage only.

A discovered keyboard/focus issue routes to Accessibility Planner; finding it does not give another role accessibility authority.

## Skill routing by task surface

```text
Task / artifact
  -> select atomic role
  -> dependency availability preflight
  -> activate relevant procedural skills
  -> if non-trivial intensive UI:
       create/continue fresh ui-question-auditor round workstream
       designate same-role round coverage/synthesis owner
  -> build manifest + checkpoint target
  -> execute in slot-safe batches
```

Skills may activate later if evidence changes task shape. Update canonical state/manifests and rerun only affected work/routes.

## Conflict / authority rules

External skills do not silently change:

- user objective;
- role ownership;
- same-role pairing requirements;
- production-write authority;
- department routing;
- validation gates;
- user-vs-agent authority.

If a skill exposes a decision outside the current role, route it. If it conflicts with higher authority/project-specific instructions, record the conflict and escalate through Morrison rather than improvising.

## Profile inheritance model

```text
ALL STABLE PROFILES
  -> REQUIRED FOR FULL MODE: agent-context-foundation

VISIBLE/PERCEPTIBLE UI ASSIGNMENT
  -> CONDITIONAL/ACTIVE: intensive-ui-questioning

NON-TRIVIAL DELEGATED INTENSIVE UI
  -> REQUIRED WORKSTREAM: ui-question-auditor fresh rounds
  -> REQUIRED PER ROUND: explicit same-role complete coverage/synthesis owner
```

Profiles need not copy these full policies. Strong recurring use may add a compact Skill References section pointing here.

## Completion check

Before terminating a stable child, verify:

- dependency states are resolved;
- required skills were actually loaded/applied or path is explicitly reduced/blocked;
- conditional activation was correct;
- out-of-role questions were routed;
- material findings are checkpointed;
- reusable knowledge promotion/retirement follows ACF when available;
- exact evidence/owner/handoff anchors survive;
- context is not being retained merely as memory.

For non-trivial delegated intensive UI, task-level completion additionally requires:

- required round budget recorded/completed;
- unique fresh identities per round;
- round Pair-Groups/receipts persisted;
- complete entrypoint + complete routing-inventory accountability for each round;
- delegated pack coverage reconciled by the round synthesis owner;
- questions individually processed;
- premise owners disposition material findings;
- final required round reaches complete route closure or work remains open/blocked;
- late material changes are audited by a later required fresh round.

## Core principle

**Roles own decisions; skills own procedure. ACF keeps durable context trustworthy. Intensive UI Questioning gets one explicit same-role coverage owner per fresh round so distributed specialist work never turns “everyone checked their part” into a false claim of complete route closure.**