---
description: 'Do not create documentation or summary files in the workspace when information is already being communicated in the chat interface'
applyTo: '**'
---

# Stop Making Useless Markdown Files

## Core Principle

**Do not create workspace files to document, summarize, or report information when you're already talking to the user in chat.** It creates clutter and defeats the purpose of direct communication.

## What NOT to Create

- **Summary files**: "CHANGES.md", "SUMMARY.md", "PROGRESS.md"
- **Documentation files**: "README.md" for tasks, "NOTES.md" for implementation details
- **Report files**: Status reports, checklists, or audit trails
- **Navigation files**: Index files or file maps for reference
- **Temporary notes**: Working notes or scratch pads

## What IS Acceptable to Create

- **Project files**: Code, configuration, test files that are part of the actual project
- **Required documentation**: README, CONTRIBUTING, API docs that are part of the deliverable
- **Actual implementation files**: Source files, utilities, modules that serve a real purpose

## Documentation Timing

Documentation is technical debt if created too early. **Focus on code first, documentation last.** During development:

- Do not create README files prematurely
- Do not write comprehensive API docs before the API is stable
- Do not document features that are still in flux
- Save documentation effort for when the project is mature and ready to be explained

Documentation written during active development often becomes stale and requires constant updating. Create it when the code is settled and you can write accurate, durable explanations.

## Why This Matters

Every file you create:

1. Clutters the workspace
2. Creates noise in version control
3. Requires the user to review unnecessary content
4. Duplicates information already in chat
5. Makes the actual project harder to navigate

You're already explaining everything to the user in this chat. Use that channel. Don't make a file that says the same thing.

## Implementation

When you want to communicate status, findings, or next steps:

✅ **DO**: Tell the user directly in chat
- "I've completed the refactor and run the tests. They all pass."
- "Found three issues: [list them]"
- "Next step is to update the config file."

❌ **DON'T**: Create a file like `PROGRESS.md` containing this information

## Exception

Create documentation only if:

- It's a required deliverable (part of the actual project)
- It's code-adjacent documentation that serves the codebase
- The user explicitly asks you to document something in a file
