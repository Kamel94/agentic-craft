# Usage

The `code-review` skill contains the review methodology. Your prompt should provide only the context specific to the change being reviewed.

## Minimal review

```text
Review this MR.

Work item: IVTS-101726
```

Depending on the harness, you can refer to a pull request, merge request, branch, commit, patch, or the currently checked-out change.

## Review without a work item

```text
Review this change.

No work item is available.
```

A work item improves functional validation but is not required. The reviewer should continue with technical review and avoid inventing undocumented product intent.

## Add review-specific context

Use the prompt for constraints that apply only to the current change:

```text
Review this MR.

Work item: IVTS-101726
Focus especially on backward compatibility with existing API consumers.
```

Do not repeat the full review methodology in every prompt. That is the purpose of the skill.

## Requirement text instead of an issue tracker

```text
Review this MR.

Requirement:
Users with an expired session must be redirected to login without losing the URL they originally requested.
```

The requirement source can be an issue tracker, a specification, a PR/MR description, or text supplied directly in the prompt.

## Skill activation

Agent Skills-compatible harnesses can activate a skill from its name and description when the request matches. Some harnesses also provide an explicit way to invoke a skill.

If automatic activation is uncertain, mention the skill directly:

```text
Use the code-review skill to review this MR.

Work item: IVTS-101726
```

## Expected review behavior

The reviewer should:

- understand the intended behavior before judging the implementation;
- inspect the diff and relevant surrounding code;
- retrieve requirement context through an available integration when a work item is provided;
- validate suspected issues with realistic failure scenarios;
- challenge whether the existing tests would catch plausible regressions;
- report only actionable findings;
- return `No actionable findings.` when nothing survives validation.

A missing or inaccessible work item should be reported as a limitation, not filled in by assumption.
