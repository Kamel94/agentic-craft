# Code Review Methodology

Use this methodology to turn a code review into a focused risk assessment rather than a style audit.

## Review priorities

Evaluate concerns in this order unless the change clearly demands a different emphasis:

1. Correctness
2. Functional compliance
3. Security and privacy
4. Regression risk and compatibility
5. Architecture and design
6. Maintainability and operability
7. Performance and resource usage
8. Test effectiveness
9. Style

Style should rarely produce a finding unless it materially affects correctness, readability of critical logic, maintainability, or an established repository rule that is not already enforced automatically.

## Phase 1: Understand

Build the smallest accurate model of the intended change before judging the implementation.

Determine:

- the purpose of the change;
- the expected user or system behavior;
- relevant acceptance criteria and business rules;
- compatibility or migration constraints;
- important edge cases;
- explicit non-goals when documented.

Prefer authoritative sources in this order when available:

1. explicit user instructions for the review;
2. repository-specific instructions and architecture documentation;
3. referenced work item or specification;
4. pull request or merge request description;
5. behavior implied by the existing code and tests.

Never invent missing requirement context. If two sources conflict, identify the conflict and use the higher-authority source unless the repository explicitly defines another precedence.

## Phase 2: Inspect

Start with the change itself.

Inspect:

- changed lines and files;
- affected public interfaces and contracts;
- tests changed or added with the implementation;
- error paths and boundary conditions introduced by the change;
- state transitions, persistence, concurrency, and external calls when relevant.

Look for concrete mismatches between intended behavior and actual behavior.

## Phase 3: Expand

Read beyond the diff only when doing so can answer a specific review question.

Useful expansion targets include:

- callers of a changed function;
- implementations of a changed interface;
- consumers of a changed model or schema;
- existing validation or authorization layers;
- migrations and serialization contracts;
- configuration that changes runtime behavior;
- existing tests that document invariants.

Stop expanding when the suspected risk is confirmed, disproved, or no longer reasonably connected to the submitted change.

Do not audit unrelated pre-existing problems unless the submitted change makes them newly reachable, materially worse, or directly relevant to correctness of the change.

## Phase 4: Challenge every suspected finding

Before reporting a finding, answer all of the following:

1. **Where is the issue?** Identify the narrowest responsible code location.
2. **How is it triggered?** Describe a realistic input, state, call path, race, deployment condition, or user action.
3. **What happens?** Explain the incorrect observable behavior.
4. **Why does it matter?** Establish meaningful impact.
5. **Is it already prevented?** Check surrounding guards, framework guarantees, callers, types, tests, and configuration.
6. **Is it caused or exposed by this change?** Avoid reporting unrelated legacy issues as review findings.

Discard the concern when these questions cannot be answered with reasonable confidence.

### Confidence rule

Prefer omission over speculation. A plausible-sounding concern is not enough.

Qualify uncertainty only when the unresolved point itself is actionable, for example when correctness depends on an undocumented external contract that the change assumes.

## Phase 5: Evaluate tests

Review tests as executable evidence of intended behavior.

Ask:

- Do the tests cover the behavior that actually changed?
- Would they fail if the new logic were implemented incorrectly in a plausible way?
- Are failure paths, boundaries, authorization rules, or state transitions left unprotected?
- Are tests accidentally coupled to implementation details while missing externally observable behavior?
- Does a regression test reproduce the defect it claims to prevent?

Do not request tests generically. Name the missing behavior and the regression it would catch.

A lack of tests is not automatically a finding when the change is trivial or existing coverage already protects the behavior.

## Phase 6: Report

Report only actionable findings.

Each finding should communicate:

- **Problem:** what is wrong;
- **Evidence:** what in the change demonstrates it;
- **Impact:** the realistic consequence;
- **Recommendation:** a practical direction for fixing it.

The final comment can be concise; these four elements are a validation standard, not a requirement for four labeled paragraphs.

Order findings by severity. When multiple findings have the same root cause, prefer one clear finding over several repetitive comments.

## Common false positives to reject

Do not report these without concrete impact:

- personal naming or formatting preferences;
- alternative implementations that are merely different;
- hypothetical performance concerns without a credible scale or hot path;
- speculative concurrency issues with no possible concurrent execution;
- theoretical nullability failures prevented by types or upstream validation;
- missing checks already guaranteed by framework or repository invariants;
- pre-existing problems untouched by the change;
- requests to add comments or abstractions solely for taste;
- generic "add more tests" suggestions.

## Valid empty review

If no issue survives validation, return no findings.

A concise statement such as `No actionable findings.` is preferable to manufacturing feedback.
