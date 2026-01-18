# Copilot Global Instructions

A curated set of guardrails, behavioral rules, and operational guidance for GitHub Copilot across all projects.

## Usage

### VS Code

Place the `.github/instructions/` directory in your workspace root or at the global level. Add this to your VS Code settings to enable Copilot to load instructions:

```json
"chat.instructionsFilesLocations": {
  ".github/instructions": true,
  "~/.github/instructions": true
}
```

This configuration loads workspace-local instructions first (for project-specific guidance), then falls back to global instructions at `~/.github/instructions/` (e.g., via symlink to this repo).

See [VS Code documentation](https://code.visualstudio.com/docs/copilot/workspace-context#_custom-instructions-for-github-copilot) for details.

## Instruction Hierarchy

See [`.github/instructions/README.md`](.github/instructions/README.md) for the tier hierarchy and organization key.

## Philosophy

These instructions codify the principle: **Copilot is most useful when it operates with autonomy within clear, hard boundaries.** Rather than asking permission for every action, explicit rules enable trust-based collaboration.

Key themes:
- **Safety first**: Destructive operations require explicit approval; everything else defaults to "yes."
- **Understanding over speed**: Read context; make surgical changes; test before committing.
- **Operational discipline**: Docker isolation, local environments, version verification, clean git history.
- **Clear communication**: Explain the why; comment sparingly; keep documentation focused.
- **Security by default**: OWASP-aligned guidance for all code generation and review.

## ⚠️ Important Warnings

**Copilot is still unpredictable.** These instructions reduce—but do not eliminate—the risk of poor suggestions, hallucinations, or unintended consequences. They are guardrails, not guarantees.

- **Always maintain good backups** of critical code, configuration, and data. If something goes wrong, you want to recover quickly.
- **Review code before committing.** Even with these guardrails in place, read diffs carefully. AI makes mistakes.
- **Test before merging.** These instructions encourage testing, but you're ultimately responsible for validating changes.
- **Use your judgment.** If Copilot's suggestion feels wrong or risky, it probably is. Trust your instincts over convenience.

## Complementary Tool

Aligned with the philosophy of "clear boundaries, safe autonomy":

- **[shell-safe-rm](https://github.com/kaelzhang/shell-safe-rm)**: A drop-in replacement for `rm` that moves files to Trash instead of permanently deleting them. Recoverable by default; supports all standard `rm` flags and optional file protection rules.

## Contributing / Customizing

These files are intended to be **atomic and self-contained**. Each instruction covers a single domain and is independent of others (no cross-references).

If you fork or adapt:
- Keep the numbered tiers and kebab-case naming consistent
- Avoid adding cross-references between files
- Focus each file on a single, actionable principle

## License

MIT. Inspired by and adapted from [github/awesome-copilot](https://github.com/github/awesome-copilot).

## Feedback

If you find these instructions helpful or have suggestions, feel free to open an issue or discussion.
