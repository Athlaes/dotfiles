---
name: global-code-review
description: >-
  Review code changes, branches, pull requests, commits, or selected files in any
  programming language. Define the shared review scope, validation rules,
  severity levels, and findings format. Use when a code review is requested;
  combine with a language-specific review skill when applicable.
---

# Global Code Review

## Review Scope

Review the changes explicitly requested by the user: a branch, diff, pull request,
commit, or selected files. Establish the review target and comparison base from
the request and repository context. Ask for clarification if material ambiguity
remains.

### In Scope

- Changed production code and associated tests.
- Related configuration and dependency changes that affect application behavior.
- Direct callers, implementations, and consumers needed to assess compatibility.
- Correctness, regressions, exception propagation, and error reporting.
- Resource management, concurrency, timeouts, and retry behavior.
- Input validation, sensitive data exposure, and security boundaries.
- API and message contracts, including serialization and backward compatibility.
- Test coverage for changed behavior, failure paths, and edge cases.
- Maintainability issues with a concrete impact on correctness or future changes.

### Review Boundaries

Read surrounding code as needed to verify a finding, but keep findings tied
to the review target or regressions caused by it.

Do not modify source files unless the user explicitly requests fixes.

Apply language-specific guidance only to the relevant code. For Java changes,
also read [java-code-review](../java-code-review/SKILL.md). Do not apply that
skill to non-Java applications.

## Review Workflow

- Inspect the requested changes and relevant repository instructions.
- Trace affected callers and consumers to confirm suspected regressions.
- Check tests for the changed behavior and run relevant validation when feasible.
- Prioritize integration tests over unit tests. Reserve unit tests for edge
  cases or business methods with many conditional branches that are not worth
  covering through integration tests.
- Report confirmed, actionable findings and state any validation limitations.

## Findings Format

List findings first, ordered by severity. Report actionable issues introduced
by the reviewed changes, not personal style preferences or speculative risks.

For each finding, use this format:

### [P2] Short, actionable title

- **Location:** A clickable file link and the smallest relevant line range.
- **Issue:** Explain what is wrong and under which conditions it occurs.
- **Impact:** Describe the concrete consequence.
- **Suggested fix:** Recommend the smallest reasonable correction.

### Severity Levels

- **P0 — Critical:** Blocks release or causes widespread failure, data loss,
  or a severe security breach. Requires immediate action.
- **P1 — High:** Causes significant incorrect behavior or a serious regression
  in a supported scenario. Should be fixed before merging.
- **P2 — Medium:** A concrete bug or maintainability issue with limited impact.
  Should be addressed, but is not an emergency.
- **P3 — Low:** A minor, actionable improvement. Non-blocking.

Assign severity based on demonstrated impact and likelihood, not on the type
of code involved.

### Reporting Rules

- Keep each finding focused on one distinct issue.
- Reference the smallest relevant line range, preferably within the diff.
- Explain the triggering conditions and support claims with code evidence.
- Check surrounding code before reporting missing validation or error handling.
- Do not report existing issues unless the changes introduce a new regression.
- Put unresolved questions in a separate **Open Questions** section rather
  than presenting assumptions as confirmed findings.
- Keep optional suggestions separate from defects.
- If no actionable issues are found, state: **No actionable findings.**
- End with a brief **Validation** section stating what was checked, which
  tests were run, and any remaining coverage gaps. Never imply that tests
  passed unless they were actually executed successfully.
