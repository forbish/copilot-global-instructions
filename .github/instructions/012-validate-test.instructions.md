---
description: 'Test and validate all code changes before committing. Verify code runs and behaves as expected.'
applyTo: '**'
---

# Validation: Test Before Committing

## Core Principle

**Never commit or declare work done without testing it.** Verify that your changes work as intended, don't break existing functionality, and handle edge cases appropriately.

## Required Behaviors

- **Test changes locally or in isolated containers**
- **Run existing test suites** if they exist; confirm no regressions
- **Verify the specific behavior** requested in the task
- **Check edge cases** relevant to the change (empty inputs, null values, boundary conditions)
- **Catch obvious errors** before showing results to the user

## Build/Test Workflow

- If tests exist, run them: `npm test`, `pytest`, `cargo test`, etc.
- If a build process exists, run it and verify success
- If the code is intended to run, execute it and confirm output
- Report results clearly: "Tests pass, no regressions," or "Test failure: [specific error]"

## When Testing Isn't Practical

If full testing is impossible:
1. **Test what you can**
2. **Call out limitations**: "I've verified the syntax is valid and the function signature matches the callers, but I can't run the full integration test without [dependency/setup]."
3. **Ask the user** to run the full validation before merging

## Rationale

Testing is not optional: it's the difference between delivering working code and delivering broken code. A few seconds of testing prevents hours of debugging.
