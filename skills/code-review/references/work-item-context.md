# Requirement and Work-Item Context

Use requirement context to judge whether the implementation solves the intended problem, not only whether the code is internally consistent.

## Supported sources

Treat the requirement source generically. It may be:

- a Jira issue;
- a GitHub or GitLab issue;
- a Linear issue;
- an Azure DevOps work item;
- another issue tracker accessible through the current harness;
- a specification or design document;
- the pull request or merge request description;
- requirements supplied directly in the review request.

Do not hard-code assumptions about any specific provider.

## Retrieving referenced work items

When a work-item identifier or URL is provided:

1. use an available integration or tool that can read that source;
2. retrieve the item before evaluating functional compliance when possible;
3. do not ask the user to duplicate information that is already accessible through the harness;
4. do not invent content when the integration is unavailable, unauthorized, or incomplete.

If retrieval fails, continue the technical review when possible and explicitly state that functional compliance could not be fully verified.

## Extracting requirement context

From the available source, identify only information relevant to the submitted change:

- **Objective:** what outcome is required;
- **Acceptance criteria:** observable conditions for completion;
- **Business rules:** domain constraints the implementation must respect;
- **Constraints:** compatibility, technical, operational, regulatory, or rollout constraints;
- **Edge cases:** explicitly mentioned exceptions or boundary behavior;
- **Non-goals:** behavior explicitly excluded from the change.

Do not expand the review into unrelated requirements from the same epic, project, or backlog unless they constrain the submitted change.

## Handling ambiguity

When requirement wording is ambiguous:

- prefer explicit acceptance criteria over inferred intent;
- use repository behavior and tests as supporting evidence, not as invented product requirements;
- distinguish a confirmed implementation defect from a requirement ambiguity;
- avoid blocking findings that depend entirely on an interpretation that is not established by the available sources.

## Handling multiple sources

Use the most authoritative and specific source available.

If sources materially conflict, call out the conflict rather than silently choosing an interpretation that creates a finding.

## No work item available

A work item is helpful but optional.

The review can proceed from the diff, repository context, tests, and change description. In this mode, evaluate technical correctness and any functional behavior that can be established from those sources, while avoiding claims about undocumented product intent.
