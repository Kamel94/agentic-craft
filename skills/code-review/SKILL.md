---
name: code-review
description: Review pull requests, merge requests, commits, patches, diffs, and proposed code changes with a rigorous, low-noise methodology focused on correctness, functional intent, regressions, security, design, maintainability, and test effectiveness. Use when asked to review code changes or assess whether an implementation is safe and correct.
license: MIT
---

# Code Review

Perform a senior-level code review of the requested change. Optimize for useful signal, not comment volume.

## Core principles

- Correctness and real-world impact matter more than stylistic preference.
- A review with no actionable findings is a valid successful outcome.
- Never fabricate unavailable requirements, ticket content, repository conventions, or runtime behavior.
- Do not report an issue unless you can identify the problematic code, a realistic failure scenario, and meaningful impact.
- Uncertainty alone is not a finding. Report uncertainty only when the missing or ambiguous information itself creates a concrete merge risk that cannot be resolved from available context.
- Do not report subjective style preferences or issues already enforced reliably by the project's formatter, linter, compiler, or equivalent tooling unless they create a concrete defect.
- Stay focused on the requested change. Explore outside the diff only when needed to confirm or reject a concrete risk.
- Treat repository-specific instructions and documented conventions as authoritative when they are available.

## Review workflow

1. **Understand the change**
   - Identify what changed and why.
   - Use the change description, work item, specification, or other requirement source when available.
   - If a work-item reference is provided, retrieve it through any available integration before judging functional compliance.
   - If requirement context is unavailable, state that limitation rather than guessing.

2. **Inspect the implementation**
   - Read the diff and changed files.
   - Inspect relevant tests and directly adjacent code.
   - Identify behavioral changes, invariants, external contracts, data-flow changes, and failure paths.
   - Explicitly consider regressions: identify behavior that worked before the change and can now fail because of the submitted diff.

3. **Apply targeted risk checks when relevant**
   - If the change touches authentication/authorization, persistence or migrations, transactions, concurrency/idempotency, caching, public contracts/serialization, or deployment/infrastructure, read `references/risk-areas.md`.
   - Apply only the sections relevant to the submitted change. Do not turn the review into a generic checklist audit.

4. **Expand only when justified**
   - Follow callers, interfaces, implementations, models, configuration, migrations, or existing tests only when they can confirm or disprove a risk introduced by the change.
   - Do not turn a scoped review into an unrelated repository-wide audit.

5. **Challenge suspected findings**
   - For every potential issue, establish the responsible code, a realistic trigger or execution path, and the resulting impact.
   - Check whether surrounding code, existing guards, framework behavior, or tests already prevent the problem.
   - Discard speculative or non-actionable concerns.

6. **Evaluate tests**
   - Do not merely check that tests exist.
   - Ask which plausible regressions or incorrect implementations would still pass the current tests.
   - Report missing coverage only when you can name the behavior that needs protection and why it matters.

7. **Report findings**
   - Prioritize correctness, functional compliance, security, regression risk, architecture/design, maintainability, performance, tests, then style.
   - Assign severity using `references/severity.md`.
   - Make each finding concise and actionable.
   - Each finding must establish: location, problem, realistic trigger, impact, recommendation, and confidence.
   - The final prose does not need to expose those as six labeled fields when a natural concise comment communicates them clearly.
   - Prefer a few high-confidence findings over a long list of weak observations.

## Required references

Read `references/methodology.md` before completing the review.
Read `references/severity.md` before assigning any severity.
If a work item, ticket, issue, specification, or requirement source is available or referenced, also read `references/work-item-context.md`.
If the change touches a high-risk area listed in workflow step 3, also read `references/risk-areas.md`.

## Output expectations

- Lead with actionable findings, ordered by severity.
- Anchor findings to the narrowest relevant code location when the harness supports it.
- Do not add praise, summaries of obvious changes, or filler unless explicitly requested.
- If there are no actionable findings, say so clearly.
- If functional compliance could not be verified because requirement context was unavailable, mention that limitation separately from the findings.
- Do not convert unresolved questions into findings unless the uncertainty itself creates a concrete merge risk.
