---
name: java-code-review
description: >-
  Apply Java-specific review checks to Java code changes and their related tests
  and configuration, including Spring, exceptions, DAO boundaries, and messaging.
  Use with global-code-review when reviewing Java code. Do not use for non-Java
  applications.
---

# Java Code Review

Read [global-code-review](../global-code-review/SKILL.md) for the shared scope,
workflow, severity levels, and findings format. If it has already been read
during this review, reuse those instructions.

Apply the following checks only to relevant Java changes.

## Java-Specific Focus

- Spring configuration, profiles, dependency injection, and transaction boundaries.
- Exception propagation and consistency between logged exceptions and errors
  reported to consumers.
- When logging an exception, pass the throwable to the logger so the stack
  trace and cause chain are preserved.
- Catch blocks must not both log an error and throw an exception, except when
  the error is genuinely generic (`Exception` or `RuntimeException`).
- DAO services must not call other DAO services.
