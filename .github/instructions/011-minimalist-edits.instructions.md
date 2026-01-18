---
description: 'Make minimal, surgical changes focused on the task at hand. Do not refactor, optimize, or extend beyond what was requested.'
applyTo: '**'
---

# Minimalist Focus: Surgical Edits Only

## Core Principle

**Do only what you're asked to do. Make the minimum necessary changes to accomplish the task.** Do not refactor unexpectedly, optimize prematurely, add "nice-to-haves," or reorganize code you weren't asked to touch.

## Required Behaviors

- **Task-focused**: Solve the exact problem stated. Nothing more.
- **Surgical edits**: Change only the lines/functions/files needed. Preserve surrounding code structure and style.
- **No unsolicited refactoring**: Do not reorganize, rename, or restructure code unless explicitly requested.
- **No feature creep**: Do not add error handling, logging, or features "while you're at it."
- **No style fixes**: Do not apply formatting, linting, or code cleanup outside the task scope.
- **Preserve convention**: Match the existing code style, patterns, and organizational approach of the file/project.

## When Refactoring is Necessary

If the task requires refactoring or cleanup:
1. **Ask first**: Explain what needs changing and why
2. **Scope it**: Be specific about what you'll touch
3. **Keep it focused**: Don't fix unrelated issues in the same PR

## Example

**Bad**: User asks to "add a function to calculate tax." You add the function, reorganize file structure, refactor variable names, add logging, and improve error handling.

**Good**: You add the requested function in the existing file, matching the style and conventions already present. Done.

## Rationale

Minimal changes reduce review burden, lower merge conflicts, and keep history clean. They also respect the user's autonomy: if they wanted a refactor, they'll ask for it explicitly.
