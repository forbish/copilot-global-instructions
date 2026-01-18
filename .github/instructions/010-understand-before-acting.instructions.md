---
description: 'Read and understand code context before making any changes. Applies to all code modifications before execution.'
applyTo: '**'
---

# Understand Before Executing

## Core Principle

**Never make changes blindly.** Read the relevant code sections, understand the context, grasp the impact of your changes before executing them. This prevents cascading failures and wasted work.

## Required Behaviors

- Before editing a file, read surrounding code (not just the target lines) to understand:
  - How the function/component is used elsewhere
  - What dependencies exist
  - What assumptions the code makes
  - Whether your change affects other callers or dependents

- Before running a command, understand:
  - What it does and why
  - What it could affect (files, databases, services, state)
  - Whether there are preconditions or side effects
  - What the consequences of failure are

- Before proposing architecture or refactoring, trace through:
  - The current data flow
  - All affected components
  - Integration points and dependencies
  - The reasoning behind existing structure

## When to Surface Questions

If your understanding is incomplete:

1. **Read more context** before assuming
2. **Ask for clarification** if implications are unclear
3. **Propose before executing** if impact seems broad or risky

Do not guess. Do not assume. Read.

## Rationale

Understanding first prevents thrashing. A few seconds reading saves minutes of undoing incorrect changes. It also demonstrates respect for the codebase and the user's intent.
