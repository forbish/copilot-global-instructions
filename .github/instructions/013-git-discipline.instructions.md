---
description: 'Follow disciplined Git workflows: atomic commits, meaningful messages, clean history. Rebase/squash before merging.'
applyTo: '**'
---

# Git Workflow Discipline

## Core Principle

**Use Git intentionally.** Make commits that are atomic, meaningful, and easy to review. Keep history clean and understandable.

## Commit Discipline

- **Atomic commits**: Each commit should do one logical thing (fix one bug, add one feature, refactor one function).
- **Meaningful messages**: Write commit messages that explain the "why," not the "what."
  - Bad: `fix bug`, `update code`, `working now`
  - Good: `Fix null pointer in user validation when email is empty`, `Refactor auth handler for readability`
- **One feature per commit**: Don't mix unrelated changes.
- **No "work in progress" commits**: Commits should represent working, complete changes.

## Before Committing

- Run tests before committing
- Review your own changes: does the diff tell a clear story?
- Check for debug code, commented-out logic, or accidental changes

## Branching Strategy

- Create feature branches for non-trivial work (ask user for branch name/strategy if unclear)
- Keep branches focused on one feature or fix
- Delete branches after merging

## Rebase and Squash

- If a branch has multiple commits related to the same feature, squash them before merging
- Rebase onto main/develop before merging to avoid merge commits (unless user prefers merge commits)
- Keep history linear when practical

## Push and Publishing

- Never push to origin without explicit user approval
- Always ask before publishing a branch

## Rationale

Clean Git history is a form of documentation. Future developers (including AI agents) use commits to understand why changes were made, not just what changed. Disciplined workflows prevent merge conflicts and make rollbacks straightforward.
