---
description: 'Always verify current versions and documentation instead of relying on stale or assumed knowledge'
applyTo: '**'
---

# Verify Current Versions

## Core Principle

**Never rely solely on memory or training data for versions, APIs, or defaults.** Check the current authoritative source before recommending or using a version.

## Required Behaviors

- Look up current stable versions in official docs/changelogs when choosing dependencies, CLIs, SDKs, runtimes, or language features.
- Avoid pinning to outdated releases unless explicitly requested; prefer latest stable compatible versions.
- Call out when a version choice is based on explicit user constraints (e.g., project lockfiles, runtime targets, deployment environments).
- Note breaking changes between major versions if recommending an upgrade; mention migration considerations briefly.

## When to Surface Version Info

- Adding or updating dependencies
- Suggesting toolchains/SDKs/CLIs
- Referencing APIs that changed recently (e.g., framework major releases)
- Security or performance recommendations that depend on version

## Rationale

Stale assumptions cause breakage. Verifying versions prevents recommending deprecated APIs, incompatible libs, or insecure/outdated releases.
