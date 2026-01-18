---
description: 'Do not perform global/system-wide installs without explicit user permission; prefer project-local environments and scoped installs'
applyTo: '**'
---

# No Global Installs Without Permission

## Core Principle

Avoid changing the host system. **No global/system-wide installs or upgrades without explicit user approval.**

## Allowed Without Asking

- Project-local dependency and package management:
  - Python: Create and install into a project `.venv` / `venv` at workspace root if it doesn't exist. Use python environment tools to help set up or request generation if needed.
  - Node: project-level `npm install` / `npm ci` / `yarn install` (no `-g` flags)
  - Ruby: `bundle install` for Gemfile-managed dependencies
  - Go: project-scoped `go mod` commands, local dependency vendoring
  - Rust: `cargo` for project dependencies (no `cargo install --global`)
  - Other languages: Use project-local package managers (not global installs)
- Docker images pulled for isolated container runs when required by the task (cleanup with `--rm` and avoid leaving unused images/volumes).

## Requires Explicit Permission

- Any global/system install or upgrade: `brew install`, `brew upgrade`, `apt-get`, system package managers, kernel/drivers, Xcode CLTs
- Global language/runtime/package installs: `npm install -g`, `pip install --user`/global, `pipx install`, `go install` to GOPATH/bin, `cargo install` globally
- Modifying shell profiles: `~/.zshrc`, `~/.bashrc`, `~/.profile`, `~/.config` unless explicitly requested
- Installing new language toolchains, SDKs, CLIs, or system services

## If Installation Is Needed

1. **Propose first**: state the exact command(s), scope (global vs. project), and impact.
2. **Prefer local**: use project-local envs or containers to avoid host changes.
3. **Cleanup plan**: note how to remove/revert if approved.

## Rationale

Global installs can introduce conflicts, security risk, and require admin prompts. Localized, reversible installs keep the host clean and reproducible.
