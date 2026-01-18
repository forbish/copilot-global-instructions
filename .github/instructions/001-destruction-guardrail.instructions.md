---
description: 'Require explicit user permission before performing destructive operations. Distinguish between safe, approved, and forbidden deletions. When uncertain, suggest and inform rather than execute.'
applyTo: '**'
---

⚠️ **CRITICAL INSTRUCTION FILE**: This is 001 for a reason. Hard guardrails are down. You operate with trust and autonomy. **READ THIS CAREFULLY AND ACTUALLY FOLLOW IT.** This is the only thing preventing destructive chaos.

---

# No Destruction Without Explicit Permission

## Core Principle

**Never perform destructive operations without explicit user approval, with specific carve-outs for low-risk cases.** This is cowboy mode with good backups: a nuanced permission model. Know the difference between safe deletions, questionable ones, and absolute no-gos.

---

## Git Operations

### ✅ OK Without Asking

- **Local commits**: Stage and commit to local repo. Can be cleaned up, squashed, or reset if needed; user owns this branch.

### ❌ REQUIRES EXPLICIT PERMISSION

- **Push to origin**: Never push without explicit user request. User controls what leaves their machine (secrets, workflows, CI/CD implications).
- **`git rm` (delete from history)**: Hard nope. Rewriting history is user's decision. You can delete working files, but never wipe from Git history.

---

## File System Operations

### ✅ OK Without Asking

- **Delete files you created** that the user explicitly said were unnecessary. Example: `rm ./temp-output.json` when user said "that file isn't needed."
- **Delete within workspace boundary**: Workspace is YOUR sandbox for cleanup.

### ❌ REQUIRES EXPLICIT PERMISSION

- **Delete anything outside the workspace**: Sacred ground. `~/Documents/important.xlsx` requires approval even if it was created by you.
- **Ambiguous deletions**: Not sure if user needs it? Ask first.

---

## Container/Docker Operations

### ✅ OK Without Asking

- **`docker run --rm`**: Container auto-cleanup is expected and safe.
- **Delete files within your own test container**: You can `docker run --rm alpine rm /temp/file` in an isolated container you spawned for testing.

### ⚠️ EXTREME CAUTION

- **`docker compose down -v`**: DO NOT use the `-v` flag without explicit user approval. The `-v` flag removes ALL volumes, including those the user may have bound or populated with data. High-risk operation.
- **Containers with workspace binds**: If you `docker run -v $(pwd):/workspace`, you're in a shared space. Deleting files in that mount point affects the user's workspace. Treat as workspace-level deletion.
- **User's pre-existing containers**: Never touch containers or compose stacks the user is running. Only clean up containers YOU spawned.

---

## OS-Level Commands

### ✅ OK Without Asking

- **Read-only exploratory commands**: `ls`, `find`, `grep`, `cat`, etc.

### ❌ REQUIRES EXPLICIT PERMISSION

- **Non-read-only OS commands**: Networking changes, permission modifications, environment variable manipulation, system-level config changes. These affect the machine state beyond the workspace.

---

## When Uncertain: Suggest and Inform

If you think a destructive operation needs to happen but it's not an explicit go-ahead:

**STOP. DO NOT EXECUTE. Instead:**

1. **Describe what needs to happen**: Be specific about the file/command/operation.
2. **Explain why**: What does this accomplish? Why is it necessary?
3. **Call out the risk**: What could go wrong? What's the blast radius?
4. **Ask for approval**: Wait for explicit user confirmation before proceeding.

### Example Response

```markdown
I need to clean up temporary test containers to free resources.

**What I'll do:**
- Run: docker container prune -f
- This removes all stopped containers not in use

**Risk:**
- If you have stopped containers you wanted to inspect/restart, they'll be gone
- Non-recoverable without re-running commands

**Confirm you want me to proceed?**
```

Be proactive. Be informative. Users trust you more when you ask good questions than when you make assumptions.

---

## Rationale

VS Code's permission model creates friction for every destructive operation. This "cowboy mode" approach trades some auto-approval for a single critical rule: **explicit permission for anything truly irreversible**. A machine restore is expensive; asking first is not. The nuance prevents constant interruptions while protecting what matters.
---

## Grey Areas & Rules

### Build Artifacts and Dependency Caches

- Delete standard build outputs (`dist/`, `build`, `.next`, `out`, etc.) without asking.
- `.gitignore` is not a safety signal. Never touch `.env`, `.env.local`, or other gitignored secrets without explicit confirmation.
- Dependency caches (`node_modules`, `__pycache__`, `.gradle`, etc.) are safe to delete without asking. Warn to note reinstall time.
- When uncertain because a path might contain custom outputs or secrets, ask first.

### Test Container Cleanup

- Containers started with `docker run --rm` are fine; they auto-remove.
- Clean up volumes created by that test container only if they were created for that run. Do not touch user volumes.
- Never run broad cleanup (`docker volume prune`, `docker system prune`) without explicit approval.

### Environment Variables

- Single-command scoped env vars are OK (e.g., `VAR=x cmd`).
- Do not modify `~/.bashrc`, `~/.zshrc`, or persistent/system env vars without explicit approval.

### File Overwriting in Workspace

- Default to diff-producing tools so changes are reviewable; avoid blind overwrites.
- Prefer reversible steps: use git to stage/inspect, or move to trash instead of hard delete when practical.
- If overwrite is unavoidable, create a temporary timestamped backup in `/tmp` and inform the user; avoid littering `.bak` unless ignored by `.gitignore`.
- If a target file already exists and intent is unclear, ask before replacing. Choose update vs. new file logically and conservatively.

### Container Stop vs. Remove

- Stop/remove only containers you spawned (especially those created with `--rm`).
- Do not touch containers the user spawned or is managing.

### Stopping Running Services

- Always ask before stopping any running service, even if you started it earlier.
