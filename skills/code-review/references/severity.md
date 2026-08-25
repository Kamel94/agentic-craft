# Finding Severity

Assign severity based on realistic impact and likelihood, not on how strongly the reviewer feels about the code.

## CRITICAL

Use for a highly consequential defect that can reasonably cause severe harm if merged.

Typical examples:

- exploitable security vulnerability with major impact;
- data loss or corruption affecting a broad or critical data set;
- exposure of secrets or highly sensitive data;
- reliable outage of a critical production path;
- violation of a safety- or business-critical invariant with severe consequences.

CRITICAL should be rare. Do not use it merely because a finding concerns security or architecture.

## HIGH

Use for a concrete defect likely to cause significant production impact or break an important requirement.

Typical examples:

- common user flow is broken;
- important acceptance criterion is not implemented;
- authorization or validation can be bypassed with meaningful impact;
- backward compatibility is broken for active consumers;
- significant race condition or transactional defect can occur under realistic conditions;
- deployment or migration can fail in a way that seriously affects service availability.

A HIGH finding should normally be considered blocking before merge.

## MEDIUM

Use for a real defect or design problem with limited scope, lower likelihood, or recoverable impact.

Typical examples:

- edge case produces incorrect behavior;
- a meaningful failure path is mishandled;
- resource or performance degradation matters under plausible conditions but is not catastrophic;
- the change introduces concrete maintainability risk that is likely to cause defects or operational difficulty;
- important regression coverage is missing for a behavior that is easy to break.

MEDIUM is not a bucket for uncertain findings. Confidence requirements remain the same as for higher severities.

## LOW

Use sparingly for an actionable, non-blocking issue with small but concrete impact.

Typical examples:

- a minor behavior defect with an easy workaround;
- a small observability or diagnostic problem that would materially hinder troubleshooting;
- a repository convention violation that creates a real maintenance cost and is not automatically enforced.

Do not use LOW for:

- subjective style preferences;
- optional refactors;
- "I would write it differently" comments;
- formatter or linter output;
- praise or informational notes.

If the concern has no meaningful impact, omit it rather than assigning LOW.

## Severity calibration

When choosing between two levels, consider:

- impact radius;
- likelihood of occurrence;
- ease of recovery;
- whether the defect violates a central requirement or invariant;
- whether users, data, security, availability, or downstream consumers are affected.

Severity describes the defect, not the complexity of the fix.
