---
description: 'Maintain project-specific `.github/copilot-instructions.md` files to guide AI agents with workspace-specific patterns, workflows, and architecture'
applyTo: '**'
---

# Maintain Copilot Instructions for Projects

## Core Principle

**Each project should have a `.github/copilot-instructions.md` file documenting codebase-specific patterns and workflows.** This captures the "how we do things here" for a particular workspace.

## What Goes In

Focus on discoverable, project-specific knowledge:

- **Big Picture Architecture**: Major components, service boundaries, data flows, reasoning behind structural decisions (requires reading multiple files to understand)
- **Critical Developer Workflows**: Build commands, test patterns, debugging approaches, especially non-obvious commands not discoverable from file inspection alone
- **Code Conventions**: Naming patterns, file organization, architectural patterns unique to this codebase
- **Integration Points**: External dependencies, APIs, cross-component communication
- **Critical Patterns**: Exemplified with actual file/directory references from the project

## Maintaining These Files

- **Merge intelligently** if `.github/copilot-instructions.md` exists: preserve valuable content, update outdated sections
- Update incrementally as you discover patterns during work
- When a file/pattern exemplifies a core concept, add a reference with context
- Keep it concise (~20-50 lines; longer only if warranted)
- Avoid over-documenting; focus on what makes the next agent immediately productive

## When to Create/Update

- During initial project exploration or onboarding
- When discovering non-obvious workflows or patterns
- When architecture or conventions shift
- Not every session: only when genuinely new or important patterns emerge

## Rationale

Project-specific instructions make AI agents immediately productive by providing context that can't be discovered by code inspection alone. They capture the "why" behind structural decisions and workflows.
