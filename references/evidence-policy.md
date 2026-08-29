# Evidence and Test Validation Policy

## Principle

Execution is evidence, but it is not the only valid form of evidence.

**Do not execute a test on a machine merely to re-prove behavior that authoritative documentation already defines exactly enough for the question being evaluated.**

If authoritative documentation, a stable specification, an official contract, or an equivalent canonical source establishes how a function, language feature, database operation, protocol, library API, or system primitive behaves, that documented behavior may be used directly as validation evidence.

We should not expect a documented primitive to behave differently without evidence that the implementation, version, configuration, or environment under investigation changes that contract.

Example:

~~~text
SELECT * FROM ENT
~~~

If the question is only whether the documented SQL operation selects the table result without an explicit WHERE filter, there is no value in starting a local database solely to rediscover the documented SQL semantics. Cite the applicable database/version documentation and validate the reasoning against it.

This does **not** prove unrelated environmental assumptions such as row-level security, views, permissions, triggers, isolation effects, vendor-specific behavior, or application code around the query. Those must be validated when they are material to the Issue.

## When documentation is sufficient

Documentation-backed validation is acceptable when all of the following are true:

1. the source is authoritative for the behavior being relied on;
2. the applicable product/library/database/language version is known or compatibility is established;
3. the documentation answers the exact behavioral question needed by the test case;
4. no material repository-specific configuration overrides or changes that behavior;
5. the Issue is not specifically about a suspected divergence between documented and actual runtime behavior.

When those conditions hold, running a local reproduction only to confirm the same primitive semantics is unnecessary work.

## When execution is still required or materially stronger

Prefer or require execution when the result depends on:

- repository-specific business logic;
- several primitives interacting together;
- runtime configuration;
- environment variables;
- permissions or security policy;
- database data/state;
- migrations against real schema states;
- concurrency, timing, ordering, retries, or transactions;
- dependency/version ambiguity;
- undocumented behavior;
- implementation-specific behavior;
- a suspected mismatch between documentation and actual behavior;
- integration boundaries;
- evidence that existing tests/runtime behavior contradict the documentation.

Do not use documentation as an excuse to avoid a test whose uncertainty exists in the application rather than in the documented primitive.

## Documentation is evidence only when anchored

Do not write:

> "The docs say this works."

Record the exact useful anchor whenever possible:

- source/documentation owner;
- URL or repository path;
- section/API/function/contract;
- version;
- relevant documented guarantee;
- why that guarantee applies to this test case.

If the documentation is stale, ambiguous, unofficial, or version-mismatched, downgrade it to supporting evidence and continue validating.

## Every test case must be documented

Whether a test is executed or validated from documentation, **the test case itself must always be recorded**.

Each material test case must include:

- Test-Case-ID;
- purpose / hypothesis;
- preconditions;
- action or evaluated operation;
- expected backend result;
- failure signal;
- affected invariant;
- Validation-Mode: EXECUTED | DOCUMENTATION_BACKED | MIXED;
- evidence;
- result;
- limitations / what this case does not prove.

For DOCUMENTATION_BACKED validation, evidence must include the authoritative documentation anchor and the reasoning that connects it to the expected result.

For EXECUTED validation, evidence must include the command/test/suite or other reproducible execution anchor and the observed result.

For MIXED validation, distinguish what is guaranteed by documentation from what was actually exercised.

## No fictional execution

Never describe a documentation-backed case as executed.

Never fabricate test output, commands, environments, logs, or runtime observations to make validation look stronger.

A well-supported DOCUMENTATION_BACKED result is better than a fictional EXECUTED result.

## No redundant ritual

The workflow is deliberately expensive where independent scrutiny reduces uncertainty.

It should not be expensive through ceremonial execution that adds no information.

Ask:

> What uncertainty would this execution resolve that the current authoritative evidence does not already resolve?

If the answer is "none", document the test case and use the authoritative evidence.

## Interaction with agent-context-foundation

Following $agent-context-foundation:

- keep the per-Issue test chronology and evidence in the authoritative Issue/task record;
- preserve precise anchors rather than large copied documentation blocks;
- do not promote temporary test reasoning into durable repository context;
- promote only verified reusable conclusions after closure when they reduce future rediscovery.
