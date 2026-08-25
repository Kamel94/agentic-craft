# Model Selection

Agentic Craft does not require or select a specific model. Choose the model and reasoning effort according to the risk and complexity of the change, not only its line count.

The categories below describe review depth. Model names are examples of a current routing preference, not dependencies of the skill.

## Standard review

Use for straightforward, low-risk changes such as:

- small local behavior changes;
- simple UI changes;
- routine CRUD work;
- narrow refactors with well-understood boundaries.

Current example:

- Sonnet 5, high effort

## Deep review

Use when understanding the change requires more cross-file or domain reasoning, for example:

- non-trivial business rules;
- significant refactoring;
- several interacting components;
- complex state or error handling;
- changes where regression risk is difficult to assess locally.

Current examples:

- Opus 5;
- Terra, medium or high effort depending on complexity.

## Critical review

Use for changes where a missed defect could have broad or severe consequences, for example:

- architecture boundaries;
- authentication or authorization;
- security-sensitive behavior;
- sensitive or critical data handling;
- concurrency and transactional invariants;
- high-impact infrastructure or migrations;
- broad compatibility changes.

Current example:

- Sol, medium or high effort.

A current cost-conscious alternative is:

- Kimi K3, high effort.

## Guidance, not a compatibility matrix

Model availability, names, pricing, limits, and reasoning-effort controls vary by harness and change over time. Treat these recommendations as a routing policy to revisit regularly.

A stronger model does not remove the need for good repository context, requirement access, or the validation rules in the `code-review` skill.
