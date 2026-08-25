# Requirement and Ticket Providers

A ticket provider is optional but strongly recommended when the submitted change implements a tracked work item.

Agentic Craft does not depend on a specific issue tracker. The `code-review` skill treats Jira, GitHub Issues, GitLab Issues, Linear, Azure DevOps, specifications, and directly supplied requirements as alternative sources of functional intent.

## Jira

If your team uses Jira, configure a Jira integration or MCP server supported by your coding-agent harness and authenticate it with read access to the relevant projects.

Then provide the issue key or URL with the review request:

```text
Review this MR.

Work item: IVTS-101726
```

or:

```text
Review this MR.

Work item: https://jira.example.com/browse/IVTS-101726
```

The reviewer should retrieve the issue through the available integration before evaluating functional compliance.

If Jira cannot be reached or the issue is not authorized, the reviewer must not guess its content.

## GitHub Issues

When the harness can read GitHub Issues, provide an issue number or URL:

```text
Review this PR.

Work item: #142
```

The repository context should make the issue reference unambiguous. Use a full URL when it does not.

## GitLab, Linear, Azure DevOps, and other trackers

Use the tracker integration supported by your harness and provide a stable issue identifier or URL.

No provider-specific tool name is encoded in the skill. This keeps the review methodology portable as integrations evolve.

## Specification or requirement document

A ticket is not required when another authoritative requirement source exists:

```text
Review this change against docs/session-refresh.md.
```

The harness must be able to read the referenced document.

## Requirement supplied directly

For small changes, provide the requirement inline:

```text
Review this MR.

Requirement:
When an order is already cancelled, retrying the cancellation must be idempotent and must not issue another refund.
```

## No requirement source

The review can still proceed:

```text
Review this MR.

No work item is available.
```

In that situation, the reviewer should focus on technical correctness and behavior established by the repository while making clear that full functional compliance could not be verified.

## Integration checklist

Before relying on a ticket provider for reviews, verify that:

- the integration is available in the selected harness;
- authentication is configured;
- the agent has read access to the relevant project or repository;
- issue identifiers can be resolved unambiguously;
- the integration exposes enough issue content to read acceptance criteria and business context.
