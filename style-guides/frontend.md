# Frontend Style Guide

## Purpose

This document defines general frontend development principles used across the laboratory.
It focuses on architectural and design guidelines that are independent of any specific framework.

## Scope

These guidelines apply to all frontend applications and frontend libraries developed within the laboratory,
regardless of the framework or rendering technology used.

## Frontend Philosophy

Frontend code is responsible for:
- Rendering user interfaces
- Managing user interaction
- Coordinating application state

It must not:
- Contain business rules
- Encode backend-specific logic
- Make architectural decisions beyond presentation concerns

## Separation of Responsibilities

Frontend code should be structured around clear responsibilities:

- **UI components**  
  Responsible only for presentation and user interaction.
- **Logic components or controllers**  
  Coordinate state and behavior but do not perform I/O directly.
- **Services or adapters**  
  Handle communication with external systems (APIs, storage, etc.).

Responsibilities must not be mixed.

## Component Design

Components should:
- Be small and focused
- Have a single responsibility
- Receive data through explicit inputs
- Emit events through explicit outputs

Components should not:
- Mutate external state implicitly
- Contain hidden side effects
- Depend on global state without clear boundaries

## State Management

- State must be explicit and predictable
- Avoid duplicated or derived state when possible
- Prefer lifting state up rather than synchronizing multiple sources
- Treat state as immutable by default

## Templates and Rendering

- Templates should remain simple and declarative
- Avoid embedding complex logic in rendering layers
- Data transformation should occur before rendering

## Communication with Backend Services

- Backend communication must be encapsulated in dedicated services or adapters
- Frontend components must not depend on raw backend responses
- Data mapping and normalization must be explicit

## Testing Guidelines

- Business logic must be testable independently of the UI
- UI tests should focus on behavior, not implementation details
- Avoid brittle tests tied to rendering internals

## Documentation

Frontend modules must provide module-level documentation describing:
- Purpose and responsibilities
- Public APIs
- Usage examples

Inline comments are discouraged in favor of clear structure and documentation.

## Exceptions

Exceptions must be rare and self-explanatory.
If additional context is required, it must be documented at module level.
