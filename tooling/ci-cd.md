# Tooling — CI / CD

This document defines the CI/CD standards used across the ecosystem.  
Its purpose is to ensure reliability, consistency, and safe delivery without adding unnecessary friction.

## Purpose

- Validate code quality automatically
- Prevent regressions from reaching main branches
- Ensure reproducible builds
- Enable safe and predictable deployments
- Reduce manual and error-prone steps

## Scope

CI/CD applies to:

- Code validation (linting, testing, quality gates, builds)
- Artifact generation
- Releases and deployments (when applicable)

Local developer workflows must mirror CI behavior as closely as possible.

## Core Principles

### CI is the source of truth

- If CI fails, the change is not ready.
- CI results override local assumptions or IDE behavior.

### Fast feedback over completeness

- CI must provide feedback quickly.
- Prefer incremental pipelines over slow monolithic jobs.

### Deterministic and repeatable

- Same input must produce the same output.
- No hidden state, cached assumptions, or environment magic.

## Continuous Integration (CI)

### Mandatory checks

Every repository must run at least:

- Dependency installation
- Linting
- Tests
- Quality gates
- Build (if applicable)

Failures must stop the pipeline immediately.

### Branch policy

- CI must run on:
  - Pull requests
  - Main branches
- Direct pushes to protected branches must be blocked or discouraged.

### Environment parity

- CI must use explicit versions for:
  - Runtime (Node, Java, etc.)
  - Package manager
- Avoid “latest” tags unless explicitly intended.

## Continuous Delivery / Deployment (CD)

### Optional but explicit

- CD is optional and repo-dependent.
- If enabled, it must be:
  - Explicit
  - Auditable
  - Reversible

### Deployment rules

- Deployments must originate from a clean CI run.
- Never deploy untested or locally built artifacts.
- Deployment steps must be automated.

### Environments

- Clearly separate environments:
  - Development
  - Staging
  - Production

Rules:
- No manual configuration drift
- No environment-specific logic inside the codebase

## Secrets and Credentials

- Secrets must never be committed to the repository.
- Use CI-provided secret stores.
- Rotate credentials regularly.

Rules:
- Do not log secrets
- Do not expose secrets in artifacts
- Fail fast if required secrets are missing

## Artifacts

- Artifacts must be:
  - Versioned
  - Immutable
  - Traceable to a commit or tag

Examples:
- Build outputs
- Docker images
- Packages
- PDFs or generated assets

## Versioning and Releases

- Releases must be intentional.
- Prefer semantic versioning when applicable.
- Tags must be created by automation, not manually.

## Observability and Logs

- CI logs must be:
  - Readable
  - Structured
  - Sufficient for debugging failures

Avoid:
- Excessive verbosity
- Silent failures
- Ignored exit codes

## Failure Policy

- A failing pipeline blocks merges and releases.
- Flaky pipelines are treated as defects.
- Temporary bypasses must be:
  - Explicit
  - Time-limited
  - Documented

## Documentation

- CI/CD behavior must be discoverable.
- Non-obvious workflows or decisions must be documented:
  - In this file
  - Or in a repo-level README

Avoid documenting CI logic in code comments.

## Final Rule

If CI/CD feels fragile, slow, or unpredictable, the pipeline is wrong—not the developers.
