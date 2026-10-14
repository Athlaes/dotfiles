---
name: javascript-front-code-review
description: >-
  Apply frontend JavaScript and TypeScript review checks to components, templates,
  and styles, including SCSS naming, atomic components, and display conditions.
  Use with global-code-review when reviewing frontend code. Do not use for
  backend-only JavaScript or TypeScript changes.
---

# JavaScript Frontend Code Review

Read [global-code-review](../global-code-review/SKILL.md) for the shared scope, workflow, severity levels, and findings format. If it has already been read during this review, reuse those instructions.

Apply the following checks only to relevant frontend JavaScript and TypeScript
changes and their associated templates and styles. Use the framework's native
syntax and preserve its reactivity model.

## Specific Focus

- If the project uses SCSS, avoid new BEM class names. Prefer simple, scoped
  classes and shallow nesting without requiring a rewrite of existing styles.
- Keep components as atomic as practical, with one responsibility and a small
  public API. Avoid artificial fragmentation and trivial wrappers.
- Prefer composition and reuse of existing components over duplicated UI logic.
- Put simple, cheap, side-effect-free display conditions directly in the template
  or JSX, without adding JS/TS variables, getters, computed values, or signals.
