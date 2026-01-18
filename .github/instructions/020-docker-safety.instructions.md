---
description: 'Use Docker containers for testing state-changing commands to maintain a safe, isolated environment. Automatically clean up containers and images after testing'
applyTo: '**'
---

# Docker Testing Regime

## Core Principle

**For any command that changes system state, prefer testing in an isolated Docker container rather than locally.** This provides safety without sacrificing convenience.

## Commands Requiring Docker Testing

These operation categories should use containers for testing:

- **Package Management**: Installing, upgrading, or removing dependencies
- **Environment Setup**: Configuring new tools, runtimes, or language versions
- **System State Changes**: Modifications that affect the local environment
- **Build Operations**: Compilation, bundling, or build processes for unfamiliar projects
- **Database Operations**: Running migrations, seed scripts, or data transformations
- **Infrastructure Changes**: Deploying, configuring, or modifying services

## When Local Testing is Acceptable

- Simple file edits with no system impact
- Read-only operations
- Code reviews and analysis
- Working with established, well-tested projects in your normal workflow

## Docker Testing Workflow

### 1. Run in Container

```bash
docker run --rm -v $(pwd):/workspace -w /workspace [image] [command]
```

Use `--rm` flag to automatically clean up after execution.

### 2. Automatic Cleanup

After every container-based test:

```bash
docker rm [container_id]  # If not using --rm
docker image prune -f     # Clean orphaned images
```

**Non-negotiable**: Use `--rm` flag or explicitly clean up containers. Do not leave dangling containers or unused images.

### 3. Verify Success

- Confirm the test output
- Check that cleanup was successful
- Report results back to user

## Container Selection

Choose appropriate base images:

- **Node projects**: `node:[version]`
- **Python projects**: `python:[version]`
- **Go projects**: `golang:[version]`
- **General purpose**: `ubuntu:latest`, `alpine:latest`

## Benefits

- **Safety**: No impact on local environment
- **Isolation**: Each test runs in a clean state
- **Reproducibility**: Same image each time
- **Easy Cleanup**: `--rm` handles everything

## Non-negotiable Rule

**Clean as you go.** Every container or image created must be explicitly removed or created with `--rm`. Do not leave messes for the user to clean up later. This is your responsibility.

## Volume and Data Safety

### ❌ NEVER DO THIS

- Bind a production volume directly to a test container. Production data is sacred.
- Example: `docker run -v production_db:/data test-container` → **STOP.**

### ✅ DO THIS INSTEAD

- Copy or clone the volume for testing:
  ```bash
  docker volume create test_volume_copy
  docker run --rm -v source_vol:/src -v test_volume_copy:/dst alpine cp -r /src/* /dst/
  docker run --rm -v test_volume_copy:/data [image] [test-command]
  ```
- Or use a backup/snapshot if the data store supports it (e.g., database dump → restore to test db).
- After testing, clean up the test volume:
  ```bash
  docker volume rm test_volume_copy
  ```

### Risk

Accidental data corruption, deletes, or modifications to production data. Irreversible and catastrophic.

## Exception

Local testing is acceptable only when:

- The user explicitly prefers local testing
- The operation is read-only (no state change)
- The project is in your daily workflow with proven safety
