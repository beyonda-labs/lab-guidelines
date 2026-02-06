# Versioning

## Purpose

This document defines the versioning strategy used across the laboratory.
A consistent versioning model ensures predictable releases, controlled evolution and safe adoption of changes across independent applications and shared libraries.

## Scope

These rules apply to:
- All shared libraries published as versioned packages
- Applications that expose versioned APIs or public artifacts

This document does not define deployment strategies or environment-specific versioning.

## Versioning Scheme

All versioned artifacts follow **Semantic Versioning (SemVer)**:

`MAJOR.MINOR.PATCH`

### Definitions

- **MAJOR**: Incompatible or breaking changes
- **MINOR**: Backward-compatible new features
- **PATCH**: Backward-compatible bug fixes

## Libraries

### General Rules

- Libraries must be versioned and released independently.
- Each release must correspond to a published artifact.
- Versions must be immutable once published.

### Version Bumps

- **MAJOR** version is incremented when a breaking change is introduced.
- **MINOR** version is incremented when new backward-compatible functionality is added.
- **PATCH** version is incremented for bug fixes or internal improvements.

### Breaking Changes

Breaking changes include (but are not limited to):
- Changes to public APIs or exported types
- Removal or renaming of public functions, classes or configuration options
- Behavior changes that alter expected outcomes

Breaking changes must:
- Be explicitly marked in commits
- Be documented in release notes
- Result in a MAJOR version bump

## Applications

### Versioning Strategy

Applications may follow SemVer or an alternative scheme depending on deployment needs.

Typical approaches:
- SemVer for public-facing applications or APIs
- Build-based or date-based versions for internal applications

Regardless of the scheme:
- Application versions are independent from library versions
- Applications should explicitly control dependency upgrades

## Pre-1.0 Versions

Versions below `1.0.0` indicate experimental or evolving APIs.

### Rules

- Breaking changes are allowed in MINOR versions
- APIs may change more frequently
- Releases should remain explicit and documented

Reaching `1.0.0` signals a stable and supported API.

## Dependency Management

- Applications and libraries must declare version ranges explicitly.
- Wide ranges (`*`, `latest`) are discouraged.
- Prefer controlled ranges (e.g. `^1.4.0`) with intentional upgrades.

Dependency upgrades must be treated as deliberate changes, not automatic updates.

## Release Responsibility

- Library maintainers are responsible for version correctness.
- Releases must reflect actual changes introduced.
- Automation may assist releases but must not obscure version intent.

## Deprecation Policy

- Deprecated features must be clearly documented.
- Deprecations should be announced at least one MINOR version before removal.
- Removal of deprecated features requires a MAJOR version bump.

## Summary

- Semantic Versioning is mandatory for shared libraries
- Breaking changes are explicit and intentional
- Libraries and applications evolve independently
- Versioning supports safe and predictable adoption
