# Idea Maturation / Product Discovery Protocol

## Purpose

Many expensive implementation mistakes begin before code exists.

A user can describe a valid feature narrowly while the actual product has broader users, ownership, persistence, permissions, journeys, quality, operations or future foundations.

Idea Maturation exposes those product-level needs early **without letting Product Planner or Thinkers become architects for every domain**.

The objective is reduced rework, not maximal specification.

## Core principle

Do not ask only:

> How do we build the feature the user just named?

Also ask:

> What outcome/product is the user actually trying to create, what product decisions must be intentional now, and which specialist decisions must be routed before implementation?

Discovery identifies/routs specialist needs; it does not silently answer them.

## Entry condition

Use Idea Maturation when one or more apply:

- new product/system/platform/feature family;
- major redesign;
- unclear boundaries/likely expansion;
- first feature implies identity/persistence/sharing/permissions/integrations/community behavior;
- implementation would establish long-lived foundations;
- prior work suffered avoidable redesign/rework;
- multiple plausible product directions exist.

Skip for tiny isolated work with mature product/technical contracts.

## Organizational ownership

Morrison owns the process/gate.

`product-planner` A+B owns the Product Brief and product-level decisions.

Fresh Thinkers expose one material unanswered question each. They do not become product planners, architects, security specialists or QA owners.

`researcher` resolves facts.

Specialist roles own specialist decisions after Morrison routes them.

Conceptual flow:

```text
USER IDEA
  ↓
MORRISON
  ↓
fresh one-question Thinkers as useful
  ↓
PRODUCT-PLANNER A+B
  ↓
PRODUCT BRIEF
  ├─ product decisions/classifications
  ├─ open user-authority decisions
  ├─ specialist decision backlog
  └─ capability gaps
  ↓
MORRISON ROUTER
  ├─ UI specialist pairs when needed
  ├─ frontend-architect A+B when needed
  ├─ backend-architect A+B when needed
  ├─ other contracted specialists
  └─ capability gaps for uncontracted specialties
  ↓
optional technical-planner A+B only if mature specialist technical plans need cross-specialty integration
```

No automatic `Product Planner -> Technical Planner` handoff exists.

## Thinker use during discovery

Thinkers follow `references/thinker-waves.md`:

**one Thinker = one strongest material question = terminate.**

A wave may be prompted to search for blind spots around users, ownership, journeys, permissions, rework, operations, etc., but each Thinker returns only one question.

A question like "what happens if content is private?" routes to Product Planner when it is a product visibility choice.

A question like "what authorization model enforces that?" routes to the relevant contracted technical/security owner or capability gap.

Finding a specialist question never transfers that specialty to the Thinker/Product Planner.

## Progressive product framing

### 1. Stated feature

Record what the user literally asked for.

### 2. User outcome

Clarify why users want it and what successful outcome looks like.

### 3. Product behavior

Identify product behaviors likely required for that outcome: create/own/save/share/search/manage/etc.

These are product needs, not yet technical designs.

### 4. Product foundations

Identify decisions likely expensive to discover late, such as:

- resource ownership/visibility lifecycle;
- identity need at product level;
- collaboration/public/private expectations;
- content lifecycle/version expectations;
- important cross-surface reuse expectations;
- compatibility/future-client constraints;
- security/privacy risk that requires specialist planning;
- operational/quality expectations.

The Product Brief records **what must be decided/supported**, not specialist implementation details.

### 5. Long-lived direction

Explore future directions only enough to distinguish:

- `NOW` — current product scope;
- `FOUNDATION` — current foundations must support/not block it;
- `DEFERRED` — intentionally later;
- `OPTION` — plausible future direction requiring later authority;
- `REJECTED` — considered and intentionally excluded.

Future ideas are not automatically requirements.

## Coverage matrix

Before a Product Brief is mature, Product Planner should inspect relevant dimensions and distinguish **product ownership** from **specialist routing**.

### Product/users/value — Product Planner owns

- primary users/actors;
- user problem/desire;
- primary success outcome;
- resources/actions users care about;
- product-level ownership/sharing expectations;
- current scope/non-goals;
- return value/retention intent where relevant.

### Product journeys — Product Planner frames, UX owns detailed design

Product Planner identifies required journeys/outcomes:

- first use;
- returning use;
- create/edit/delete/share/manage;
- permission-denied/recovery needs at product level.

Detailed journey/usability behavior routes to `ux-planner`.

Navigation/grouping routes to `information-architecture-planner`.

Visual treatment routes to `graphic-design-planner`.

Interaction mechanics route to `interaction-design-planner`.

Accessibility requirements route to `accessibility-planner`.

### Identity/ownership/permissions

Product Planner owns product-level choices such as:

- whether identity/account behavior is required;
- who may own/see/share/collaborate on resources;
- public/private/unlisted/draft/archive expectations;
- product/business roles/moderation expectations.

Detailed authn/authz/security implementation/policy design routes to stable specialists when contracted, otherwise capability gaps.

### Domain/data foundations

Product Planner identifies product concepts/lifecycle requirements that must exist.

It does **not** own:

- database schema/index/storage design;
- migrations;
- API contracts;
- backend service/domain architecture.

Backend domain/service decisions route to `backend-architect` when applicable. Other uncontracted technical specialties become capability gaps.

### Architecture/reuse/extensibility

Product Planner may state foundation requirements such as:

- capability should be reusable across future clients;
- must not couple ownership to one UI screen;
- external integration is likely/required;
- future export/import compatibility matters.

Detailed frontend/backend/API/data architecture belongs to technical specialists.

### Security/privacy/abuse

Product Planner identifies product-level risk/requirements such as:

- private user content;
- moderation/reporting needs;
- account/resource abuse concerns;
- privacy/deletion/export expectations.

Threat modeling/control design is a specialist responsibility, not a Product Planner responsibility.

### Quality/acceptance

Product Planner defines product-level success/acceptance intent.

`quality-strategist` later turns approved artifacts into falsifiable verification coverage.

### Operations/observability/performance

Product Planner identifies material product/operational expectations (availability, latency sensitivity, recovery expectations, usage scale assumptions) when they affect scope/foundations.

Detailed observability/performance/deployment plans require their own stable role when contracted, otherwise capability gaps.

## Product Brief contract

The canonical Product Brief should contain:

```text
PRODUCT-BRIEF

Objective / Problem:
...

Primary Users / Actors:
- ...

Value / Success:
- ...

Core Product Outcomes / Journeys:
- ...

Current Scope (NOW):
- ...

Foundations (FOUNDATION):
- ...

Deferred:
- ...

Options:
- ...

Rejected / Non-Goals:
- ...

Product-Level Ownership / Visibility / Permission Decisions:
- ...

Product Acceptance Intent:
- ...

User-Authority Decisions:
- ...

Specialist Decision Backlog:
- Decision family: ...
  Why needed: ...
  Suggested department/role: <contracted role | CAPABILITY_GAP>
  Depends on: ...

Evidence / Assumptions:
- ...

Rework Risks if Wrong:
- ...

Checkpoint Anchor:
- ...
```

## Maturity gate

A Product Brief is mature when:

- users/problem/value are coherent;
- scope/non-goals are explicit;
- product-level journeys/outcomes are known enough for specialist routing;
- expensive product foundations were considered/classified;
- product choices are separated from specialist implementation decisions;
- specialist needs/capability gaps are explicit;
- material user-authority questions are resolved or explicitly blocking/deferred;
- same-role Product Planner A+B differences are resolved/routed/escalated;
- fresh questioning no longer exposes an unowned product-level gap that would predictably invalidate downstream foundations.

Maturity does **not** mean detailed architecture is complete.

## After the Product Brief

Morrison routes each specialist backlog item to the lowest contracted owner.

Examples:

- journeys/usability -> `ux-planner` A+B;
- IA -> `information-architecture-planner` A+B;
- visual -> `graphic-design-planner` A+B;
- interaction -> `interaction-design-planner` A+B;
- design system -> `design-system-planner` A+B;
- accessibility -> `accessibility-planner` A+B;
- frontend structure -> `frontend-architect` A+B;
- backend domain/service structure -> `backend-architect` A+B;
- verification strategy -> `quality-strategist` A+B when planning reaches appropriate maturity;
- uncontracted API/data/security/performance/etc. -> capability gap until deliberately contracted.

Only after two or more mature specialist technical artifacts need integration/sequencing should Morrison use `technical-planner` A+B.

## Anti-patterns

Do not:

- jump directly from first feature wording to implementation;
- treat Product Planner as architect/security/data/QA expert;
- give one Thinker a domain checklist and let it plan the solution;
- make every possible future feature current scope;
- invent Agent-Keys from coverage-matrix headings;
- route every mature Product Brief automatically to `technical-planner`;
- convert a capability gap into a duty of the nearest broad role;
- ask the user technical questions another role/evidence can resolve.

## Core principle

**Product discovery decides what product/foundations matter; Morrison then routes how each specialty should realize them.**