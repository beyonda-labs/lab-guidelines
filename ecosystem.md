# Ecosystem

## Purpose

This document describes the structure of the laboratory ecosystem, the types of projects it contains and the relationships between them.
Its goal is to provide a clear mental model of how applications, libraries and tooling coexist and interact.

## Overview

The laboratory ecosystem is composed of multiple independent repositories that fall into a small set of well-defined categories.
Each category has a specific purpose and clear rules regarding dependencies and releases.

At a high level, the ecosystem is organized around:
- Applications that deliver user-facing or service functionality
- Shared libraries that provide reusable components and logic
- Engineering tooling that enforces standards and consistency

## Project Types

### 1. Applications

Applications are deployable units that deliver concrete functionality.
They consume shared libraries but should not be consumed by other projects.

**Characteristics**
- Independently deployable
- Own runtime configuration and infrastructure
- Can depend on multiple shared libraries
- Have independent release cycles

**Dependency rules**
- Applications can depend on shared libraries.
- Applications must not depend on other applications.

### 2. Frontend Libraries

Frontend libraries provide reusable UI components or frontend-specific logic.

**Characteristics**
- Normally framework-specific (e.g. Angular)
- Published as versioned packages
- Designed for reuse across multiple applications

**Dependency rules**
- Frontend libraries can depend on lower-level frontend libraries.
- Frontend libraries must not depend on backend libraries.
- Frontend libraries must not depend on applications.

### 3. Backend Libraries

Backend libraries provide reusable server-side building blocks.

**Typical responsibilities**
- Logging and observability
- Configuration loading
- Error handling
- HTTP utilities
- Authentication or authorization helpers

**Characteristics**
- Normally framework-agnostic where possible
- Focused on infrastructure or domain-neutral concerns
- Versioned and released independently

**Dependency rules**
- Backend libraries can depend on lower-level backend libraries.
- Backend libraries must not depend on frontend libraries.
- Backend libraries must not depend on applications (except for packaging/deployment).

### 4. Domain or Cross-Cutting Libraries

Some libraries are domain-oriented or cross-cutting and can be shared across multiple contexts.

**Examples**
- Schema definitions
- Validation logic
- Shared data models
- Document generation engines (e.g. PDF generation)

**Characteristics**
- Independent from UI and delivery layers
- Strongly contract-driven
- Used by both frontend and backend when applicable

**Dependency rules**
- Domain libraries can depend on core utilities.
- Domain libraries must not depend on applications.

### 5. Engineering and Tooling Projects

Engineering projects define shared standards and development tooling.

Engineering projects define shared standards and tooling used across the ecosystem.

**Examples**
- ESLint configuration packages
- TypeScript base configurations
- Prettier configuration
- Hooks.
- Development scripts and generators

**Characteristics**
- No runtime logic
- Focused on development experience and consistency
- Consumed by all project types

**Dependency rules**
- Tooling must not depend on applications.
- Applications and libraries can depend on tooling.

## Dependency Direction

Dependencies across the ecosystem must follow a strict, one-directional flow:

Applications --> Frontend / Backend Libraries --> Domain / Core Libraries --> Engineering Tooling

## Release Strategy

Each project in the ecosystem is released independently.

- Libraries follow Semantic Versioning
- Applications manage their own release and deployment lifecycle
- Breaking changes in libraries must be explicit and documented

This approach allows applications to adopt new versions at their own pace while maintaining stability.

## Evolution of the Ecosystem

The ecosystem is expected to evolve over time.

- New project types may be introduced if clearly justified
- Existing categories may be refined
- Any structural change must preserve clarity and dependency direction

Structural decisions that affect multiple projects should be documented as architecture decisions.

## Summary

- The ecosystem is composed of independent repositories
- Responsibilities are clearly separated by project type
- Dependencies follow a strict, one-directional flow
- Releases are independent and controlled
- Shared standards ensure long-term consistency