# Idea Maturation / Product Discovery Protocol

## Purpose

Many expensive implementation mistakes begin before code exists.

A user can describe a valid idea at a narrow level — for example, "a page that creates 3D renders" — while the actual product they want is broader: accounts, identity, sharing, community, moderation, discovery, reusable content, future integrations, security, quality, extensibility, and operational concerns.

The organization must not treat the first concrete feature description as the complete product definition.

Before substantial architecture or implementation, mature the idea enough that likely near-term requirements are visible and expensive structural decisions are intentional.

This protocol exists to reduce avoidable rework, not to force every idea into a giant specification.

## Core principle

Do not ask only:

> How do we build what the user just said?

Also ask:

> What is the user actually trying to create, who is it for, what will it become, and what decisions will become expensive if discovered later?

## Entry condition

Use Idea Maturation when one or more of these are true:

- the user is describing a new product, system, feature family, workflow, platform, or major redesign;
- the request has unclear boundaries or likely future expansion;
- the first feature implies identity, persistence, sharing, permissions, integrations, or community behavior;
- implementation would create foundations that later features must inherit;
- prior work has already suffered from repeated redesign or discarded implementation;
- the user says they have an idea but not a complete specification;
- multiple plausible product directions exist.

Do not require this protocol for tiny isolated changes with well-established contracts.

## Organizational owner

The Orchestrator owns the maturation process but should delegate the substantive questioning.

A typical structure is:

~~~text
User
  ↓
Orchestrator
  ↓
Product/Scope Planner
  ├─ Thinker Wave: users + product value
  ├─ Thinker Wave: architecture + data
  ├─ Thinker Wave: security + abuse
  ├─ Thinker Wave: UX + flows
  ├─ Thinker Wave: quality + testing
  └─ Thinker Wave: extensibility + operations
  ↓
Synthesis
  ↓
User only for authority/product choices
  ↓
Technical Planner
~~~

The exact number of waves should match the task. The categories are coverage prompts, not mandatory separate agents.

## Progressive idea expansion

The organization should move through these levels:

### 1. Stated feature

What did the user literally ask for?

Example:

- create 3D renders from Minecraft-related content.

### 2. User outcome

Why does the user want it?

Examples:

- make creations easier to visualize;
- share work publicly;
- build a recognizable identity around creations;
- discover other builders' work.

### 3. Product behavior

What must exist for the outcome to work coherently?

Examples:

- accounts;
- profiles;
- ownership;
- project persistence;
- upload/import/export;
- browsing/search;
- sharing;
- permissions;
- community interactions;
- moderation.

### 4. Product system

What foundations will future behavior depend on?

Examples:

- identity model;
- content model;
- media/storage strategy;
- public/private visibility;
- authorization;
- versioning;
- APIs;
- plugin/addon/mod integration boundaries;
- event/audit history;
- abuse handling;
- observability.

### 5. Long-lived direction

What future direction would be expensive to support if the foundation ignores it today?

Examples:

- curated community creations becoming game content;
- Bedrock addon export;
- Java mod integration;
- reusable construction knowledge base;
- creator reputation;
- collaborative projects;
- discovery/recommendation;
- import/export standards.

Future ideas are not automatically requirements. The purpose is to distinguish:

- **must support now**;
- **must not block later**;
- **explicitly deferred**;
- **speculative / not worth designing for yet**.

## Coverage matrix

Before a non-trivial product plan is declared mature, the organization should inspect the relevant dimensions below.

### Product and user

- Who are the primary users?
- What problem or desire brings them here?
- What is the primary success path?
- What secondary user types may exist?
- What does the user create, own, publish, modify, delete, or share?
- What value keeps the user returning?
- What is intentionally out of scope?

### Experience and navigation

- What are the main entry points?
- What belongs in home, authenticated home, project workspace, profile, settings, community, and admin areas?
- What is visible before login?
- What actions require authentication?
- What information architecture/navigation will remain coherent as features grow?
- What empty, loading, error, permission-denied, and first-use states exist?

### Identity and permissions

- Is login actually needed?
- What identity data is required?
- Who owns each resource?
- Public, private, unlisted, draft, archived?
- Roles or moderation privileges?
- Can users collaborate?
- What happens when an account is deleted, banned, or compromised?

### Domain and data model

- What are the core entities?
- What relationships should be stable?
- Which data is canonical versus derived?
- What needs history/versioning?
- What can be regenerated?
- What must survive product expansion?
- What migration risks exist if this model changes later?

### Architecture and responsibility boundaries

- Which capabilities should be reusable modules/services rather than page-local logic?
- Which contracts must be explicit?
- Where can duplication emerge?
- Which responsibilities should not be coupled?
- What is likely to become shared across web, API, addon, mod, worker, or admin surfaces?
- What boundaries allow future replacement without rewriting the product?

### Security and abuse

- Authentication and session risks?
- Authorization on every owned resource?
- Upload/content validation?
- Injection/XSS/CSRF/SSRF/path traversal or equivalent relevant threats?
- Secrets and token handling?
- Rate limiting?
- Spam, harassment, malicious uploads, copyright/reporting, impersonation, or moderation concerns?
- Privacy expectations?
- Data deletion/export requirements?

Do not defer obvious structural security requirements until after feature completion.

### Quality and testing

- What behavior is critical enough to require automated tests?
- Unit, integration, contract, end-to-end, migration, visual, performance, security, or compatibility coverage?
- What acceptance criteria prove the feature is actually complete?
- What regressions would be expensive?
- What test fixtures/builders/helpers should prevent repetitive test code?

### Maintainability and reuse

- What code is likely to repeat if implemented feature-by-feature?
- What common UI/domain/data primitives should exist?
- Which abstractions are justified now and which would be premature?
- Are responsibilities clear enough that future agents/developers can find the owner of behavior?
- Are there obvious monolith components/services accumulating unrelated concerns?

Reducing code is not a goal by itself. Reducing duplicated responsibility and repeated behavior is.

### Extensibility and integrations

- What future clients might consume the same data/capability?
- Does this imply an API or stable internal contract?
- What should remain client-agnostic?
- Could a Bedrock addon, Java mod, CLI, desktop tool, worker, or external integration need this later?
- What must be versioned?
- What must not be hardcoded into one UI implementation?

### Operations and lifecycle

- Deployment environment?
- Storage growth?
- Backups/recovery?
- Observability/logging?
- Background jobs?
- Content processing?
- Cost-sensitive operations?
- Feature flags or staged rollout?
- Migration/rollback strategy?

### Accessibility and compatibility

When relevant:

- keyboard/accessibility semantics;
- responsive/mobile behavior;
- browser/device constraints;
- localization;
- reduced-motion/contrast concerns;
- game/version compatibility.

## Requirement classification

Every material discovered requirement should be classified instead of silently becoming scope.

Use:

- `NOW`: required for the current deliverable;
- `FOUNDATION`: may not be user-visible now, but current architecture must support it to avoid likely expensive rework;
- `DEFERRED`: known future work, explicitly excluded from current delivery;
- `OPTION`: plausible direction requiring later product choice;
- `REJECTED`: considered and intentionally not supported.

This is critical. Good discovery should reduce blind spots without turning every possible future feature into immediate implementation.

## Decision ledger

Record material decisions with:

~~~text
DECISION
Topic: <decision>
Classification: NOW | FOUNDATION | DEFERRED | OPTION | REJECTED
Reason: <why>
Evidence/Context: <supporting source>
Consequences: <what this enables or prevents>
Revisit-When: <trigger if applicable>
Owner: <who may change this>
~~~

## Product brief output

Before handing a broad new idea to the Technical Planner, produce a canonical Product Brief containing at least:

1. Problem / opportunity
2. Product vision
3. Primary users
4. Primary user journeys
5. Core capabilities
6. NOW scope
7. FOUNDATION decisions
8. Explicit DEFERRED / OUT-OF-SCOPE items
9. Domain/data concepts
10. Identity/permissions model when relevant
11. UX/navigation model
12. Security/abuse considerations
13. Quality/testing expectations
14. Reuse/maintainability expectations
15. Extensibility/integration boundaries
16. Operational constraints
17. Acceptance criteria
18. Open product decisions requiring user authority
19. Risks and unknowns
20. Evidence/links

The brief may be large. The goal is not brevity; the goal is to give later agents a coherent source of truth.

## Thinker-wave strategy for idea maturation

Fresh thinkers are especially useful here because early product framing is vulnerable to anchoring.

Useful independent prompts include:

- What would a first-time user expect that this idea has not mentioned?
- What does a returning user need?
- What will require identity or ownership?
- What would become painful after 1,000 users or 100,000 resources?
- What security/abuse problem appears once content is public?
- What is likely to be duplicated if each feature is built independently?
- What future client/integration would force a rewrite of today's design?
- What data decision is hardest to migrate later?
- What user journey is missing between landing and value delivery?
- What happens when things fail, are deleted, revoked, banned, retried, or partially complete?
- What tests would have exposed a wrong design before implementation?

Terminate the wave after delivery. Apply the answers to the canonical brief. Then, if needed, create another fresh wave against the updated brief.

## Maturity gate

Do not hand a broad idea into substantial implementation until:

- the requested outcome is clear;
- main user journeys are explicit;
- NOW versus FOUNDATION versus DEFERRED is classified;
- likely expensive-to-change foundations have been examined;
- material security/data/permission concerns are visible;
- acceptance and validation strategy exist;
- a fresh questioning pass discovers no new material gap that would change the current architecture or scope;
- unresolved user-authority decisions are either answered or explicitly marked blocking/deferred.

For high-rework-risk products, require two fresh questioning passes with no new architectural/scope-changing gap.

## Anti-patterns

Do not:

- equate the first requested screen with the whole product;
- begin database/auth architecture from one page mockup without examining ownership and future use;
- add login merely because "apps have login" without defining what identity enables;
- create a home page before defining the product's navigation/information architecture;
- build community features without moderation/abuse/visibility thinking;
- postpone all security to a final cleanup phase;
- let every discovered future idea enter current scope;
- over-engineer speculative futures with no plausible path;
- implement repeated local solutions when a shared domain capability is obvious;
- allow one planner to declare its own coverage complete without fresh questioning.

## Example: Minecraft creation platform

A narrow starting statement such as:

> "Create a web page to generate 3D renders for Minecraft builds"

should trigger questions that can reveal a broader coherent product:

- Are renders transient or saved as projects?
- Who owns them?
- Can creators publish them?
- Is there a profile or portfolio?
- Can other users discover, like, comment, save, remix, or report them?
- Does a community feed/search/tagging system exist?
- Are construction files or metadata stored alongside renders?
- Could published builds become a searchable construction knowledge base?
- Could curated builds later be exported/included in Bedrock addons or Java mods?
- Which content model should be client-agnostic so web and game integrations can share it?
- What permissions/moderation/copyright/security constraints appear once uploads become public?
- Which capabilities need reusable APIs instead of page-local implementation?

The correct outcome is not necessarily "build all of that now".

The correct outcome is to know which parts are NOW, which foundations must not block the likely direction, and which ideas are consciously deferred before expensive code hardens the wrong shape.

## Design principle

Implementation quality cannot compensate for an incomplete product frame.

The organization should spend cheap reasoning early to avoid expensive rewriting later.