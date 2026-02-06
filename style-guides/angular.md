# Angular Style Guide

## Purpose

This document defines Angular-specific guidelines used to implement the general frontend principles
described in the frontend style guide.

## Scope

These rules apply to all Angular applications and Angular-based frontend libraries in the laboratory.

## Component Types

Angular components are categorized as:

- **Presentational components**
  - No direct API calls
  - No business logic
  - Receive data via `@Input`
  - Emit events via `@Output`

- **Container components**
  - Coordinate state and behavior
  - Interact with services
  - Pass data down to presentational components

## Change Detection

- Use `ChangeDetectionStrategy.OnPush` by default
- Default change detection must be justified explicitly
- Inputs should be treated as immutable

## State and Reactivity

- Prefer signals or observables for reactive state
- Avoid subscribing manually in components when possible
- Side effects must be isolated in services

## Services

- Services encapsulate:
  - HTTP communication
  - State coordination
  - Cross-component logic
- Components must not perform HTTP calls directly

## Templates

- Templates should remain declarative
- Avoid calling methods with side effects from templates
- Prefer pipes or precomputed values

## Module and File Structure

- Prefer standalone components where applicable
- Group files by feature rather than by type
- Avoid deep or fragmented module hierarchies

## Testing

- Components are tested with mocked services
- Logic-heavy code should be tested outside components
- Avoid snapshot-heavy or DOM-fragile tests

## Documentation

Angular modules or feature areas must include a README describing:
- Feature purpose
- Public components and services
- Usage examples
