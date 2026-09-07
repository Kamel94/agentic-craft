# Targeted Risk Areas

Use this reference only when the submitted change touches one or more of the areas below. Apply the relevant section and ignore the rest.

The purpose is to surface concrete, high-impact regressions without turning every review into a generic checklist exercise.

## Authentication and authorization

Check whether the change can:

- bypass or weaken an existing authentication boundary;
- authorize based on client-controlled identifiers instead of the authenticated principal;
- introduce role/permission inconsistencies between read and write paths;
- expose data across users, tenants, organizations, or other isolation boundaries;
- trust a token/session/cookie without the validation the surrounding system requires.

Report only when you can identify a realistic path to incorrect access or denial.

## Persistence, migrations, and transactions

Check whether the change can:

- create invalid or partially written state when one operation fails;
- violate uniqueness, foreign-key, ordering, or lifecycle invariants;
- make a migration unsafe for existing rows or active consumers;
- lose, duplicate, or reinterpret existing data;
- rely on atomicity that the chosen persistence mechanism does not provide.

Prefer concrete state-transition examples over generic requests for transactions.

## Concurrency and idempotency

Check whether realistic concurrent or retried execution can:

- create duplicate side effects;
- lose updates;
- observe or publish partially updated state;
- process the same command/event/job more than once incorrectly;
- break a uniqueness or ordering guarantee.

Do not report concurrency concerns when no plausible concurrent or retried execution path exists.

## Caching

Check whether the change can:

- serve stale data beyond the documented tolerance;
- leak cached data across users or isolation boundaries;
- fail to invalidate or vary on a field that affects correctness;
- make cache and source-of-truth state disagree in a way users can observe.

Avoid theoretical cache-performance comments unless the submitted change creates a concrete correctness or operability issue.

## Public contracts and serialization

Check whether the change can:

- break an existing API, event, persisted format, CLI, or configuration contract;
- change nullability, defaults, enum values, field names, ordering, or validation in a backward-incompatible way;
- cause old and new producers/consumers to interpret the same payload differently;
- accept inputs that later code cannot safely handle.

Establish which active consumer or compatibility guarantee is affected before reporting compatibility findings.

## Deployment and infrastructure

Check whether the change can:

- make deploy/rollback order unsafe;
- require a secret, binding, permission, environment variable, or resource that is not provisioned;
- introduce a startup/runtime dependency that can fail the service broadly;
- make a migration or infrastructure rollout non-reversible when rollback is expected;
- behave differently across environments because required configuration is missing or inconsistent.

Report deployability findings only when the failure mode follows from the submitted change and realistic environment assumptions.
