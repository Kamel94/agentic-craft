# Agentic Craft

Portable engineering skills for AI coding agents.

Agentic Craft packages reusable software-engineering practices as harness-agnostic [Agent Skills](https://agentskills.io/). The goal is to make coding agents more consistent, rigorous, and useful without locking the methodology to a specific model, issue tracker, or coding harness.

> **Status:** early preview. The first skill is being validated on real-world code reviews before the methodology is considered stable.

## Skills

### `code-review`

A low-noise code-review methodology focused on correctness, functional intent, real-world impact, regressions, security, design, maintainability, and test effectiveness.

The reviewer is explicitly instructed to validate suspected findings before reporting them and to prefer `No actionable findings.` over speculative feedback.

## Install

The repository follows the standard `skills/*/SKILL.md` layout. Install the skill using the mechanism supported by your coding agent.

With GitHub CLI 2.90.0 or later, for example:

```bash
# GitHub Copilot
gh skill install Kamel94/agentic-craft code-review --agent github-copilot --scope project

# Claude Code
gh skill install Kamel94/agentic-craft code-review --agent claude-code --scope project

# Codex
gh skill install Kamel94/agentic-craft code-review --agent codex --scope project
```

Use `--scope user` instead when you want the skill available across your repositories.

You can inspect the skill before installing it:

```bash
gh skill preview Kamel94/agentic-craft code-review
```

See [Installation](docs/installation.md) for project scope, user scope, local installation, pinning, and updates.

## Use

Once the skill is available to your agent, keep review prompts focused on the current change:

```text
Review this MR.

Work item: IVTS-101726
```

No Jira dependency is required. The work item can come from Jira, GitHub Issues, GitLab, Linear, Azure DevOps, a specification, the PR/MR description, or requirements supplied directly in the prompt.

If automatic skill activation is uncertain:

```text
Use the code-review skill to review this MR.

Work item: IVTS-101726
```

See [Usage](docs/usage.md) for more examples.

## Review philosophy

Agentic Craft treats code review as risk assessment, not a contest to produce comments.

The `code-review` skill prioritizes:

1. correctness;
2. functional compliance;
3. security and privacy;
4. regression risk and compatibility;
5. architecture and design;
6. maintainability and operability;
7. performance and resource usage;
8. test effectiveness;
9. style.

A finding must identify a concrete problem, a realistic way to trigger it, and meaningful impact. Subjective preferences and generic "add more tests" comments do not qualify.

## Requirement context

When a change implements a tracked work item, giving the reviewer access to that source improves functional review.

For Jira, configure a Jira integration or MCP server supported by your harness and give it read access to the relevant issues. Other ticket systems can be used through their corresponding integrations.

See [Requirement and Ticket Providers](docs/ticket-providers.md).

## Model selection

The skill is model-agnostic. Choose review depth based on risk and complexity rather than only change size.

The documentation groups reviews into **Standard**, **Deep**, and **Critical** levels and keeps current model suggestions outside the skill so they can evolve independently.

See [Model Selection](docs/model-selection.md).

## Repository structure

```text
agentic-craft/
├── .github/
│   └── workflows/
│       └── validate-skills.yml
├── README.md
├── LICENSE
├── skills/
│   └── code-review/
│       ├── SKILL.md
│       └── references/
│           ├── methodology.md
│           ├── severity.md
│           └── work-item-context.md
└── docs/
    ├── installation.md
    ├── usage.md
    ├── model-selection.md
    └── ticket-providers.md
```

Future skills should remain independently installable and follow the same principle: core engineering methodology in the skill, operational guidance in documentation, and harness-specific integrations only when they are actually necessary.

## Validation

Pull requests and updates to `main` run the official GitHub CLI Agent Skills validation:

```bash
gh skill publish --dry-run
```

This validates discovered skills against the Agent Skills specification without publishing a release.

## License

[MIT](LICENSE)
