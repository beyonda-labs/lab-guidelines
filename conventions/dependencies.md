# Dependencies

## Purpose

This document defines general policies for managing dependencies across the laboratory.
The goal is to ensure reproducible builds, predictable behavior and controlled upgrades during early and evolving stages of the ecosystem.

## Scope

These policies apply to:
- Applications and shared libraries
- Runtime and development dependencies
- Internal and external packages

This document does not define approved or forbidden dependencies.
Specific dependency choices remain project-specific.

## Version Pinning Policy

### Fixed Versions Only

- Dependencies must be declared using fixed, explicit versions.
- Version ranges (`^`, `~`, `*`, `latest`) must not be used.

### Example

`"lodash": "4.17.21"`

This ensures that builds are reproducible and not affected by upstream changes.

## Dependency Upgrades

- Dependency upgrades are explicit, intentional actions.
- Upgrades must be reviewed and tested before being merged.
- Multiple dependency upgrades should not be bundled with unrelated changes.

## Internal Dependencies

- Shared libraries must be consumed via published, versioned packages.
- Applications must explicitly update internal dependencies.
- Local linking or implicit coupling is discouraged outside development or experimentation contexts.

## Pre-1.0 Dependencies

- Dependencies below `1.0.0` are considered unstable.
- Even patch or minor updates may introduce breaking changes.
- Upgrading pre-1.0 dependencies requires extra caution and validation.

## Peer Dependencies

- Libraries must declare peer dependencies when required for compatibility with a host framework or runtime.
- Peer dependency versions should also be pinned when possible.

## Rationale

Version pinning prioritizes:
- Reproducibility across environments
- Predictable behavior in CI and production
- Clear visibility of dependency changes

This approach favors stability and explicit decision-making over automatic updates.

## Evolution

This policy may evolve as the ecosystem matures.
Relaxing version pinning must be an explicit and documented decision.

## Summary

- All dependencies use fixed versions
- Version ranges are not allowed
- Upgrades are deliberate and reviewed
- Stability and predictability are prioritized

