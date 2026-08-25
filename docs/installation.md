# Installation

Agentic Craft uses the open Agent Skills format. The `code-review` skill lives at `skills/code-review/` and can be installed in any compatible coding agent.

There is no single preferred installation path. Choose the option that fits your harness and whether you want the skill available for one project or for all projects.

## GitHub CLI

GitHub CLI 2.90.0 or later provides `gh skill` commands for discovering and installing Agent Skills. The feature is currently in preview.

Preview the skill before installing it:

```bash
gh skill preview Kamel94/agentic-craft code-review
```

### GitHub Copilot

Project scope:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent github-copilot \
  --scope project
```

User scope:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent github-copilot \
  --scope user
```

### Claude Code

Project scope:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent claude-code \
  --scope project
```

User scope:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent claude-code \
  --scope user
```

### Codex

Project scope:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent codex \
  --scope project
```

User scope:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent codex \
  --scope user
```

GitHub CLI supports additional coding agents as well. Use `gh skill install --help` for the current list of `--agent` values.

## Project scope or user scope?

Choose **project scope** when:

- the team wants the repository to have an explicit, reproducible skill installation;
- different projects should use different skill versions;
- you want changes isolated to the current repository.

Choose **user scope** when:

- you want the reviewer available across many repositories;
- you are evaluating Agentic Craft personally before adopting it at team level;
- you prefer to manage your coding-agent skills centrally.

With `gh skill install`, `project` is currently the default scope when a scope is not specified.

## Install from a local clone

For development or testing before publishing a release:

```bash
git clone https://github.com/Kamel94/agentic-craft.git
cd agentic-craft

gh skill install . code-review \
  --from-local \
  --agent github-copilot \
  --scope project
```

Change `--agent` and `--scope` to match your environment.

## Other Agent Skills-compatible harnesses

If your harness supports Agent Skills but is not covered above, install or copy the `skills/code-review/` directory using that harness's documented skill mechanism.

The skill itself does not depend on Copilot, Claude Code, Codex, or any harness-specific tool name.

## Pinning a version

For stable team usage, pin a released version:

```bash
gh skill install Kamel94/agentic-craft code-review \
  --agent github-copilot \
  --scope project \
  --pin v0.1.0
```

Use an available release tag or commit SHA.

## Updating

Update one installed skill:

```bash
gh skill update code-review
```

Or update all skills managed by `gh skill`:

```bash
gh skill update --all
```
