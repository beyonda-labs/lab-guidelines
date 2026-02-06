# TypeScript Style Guide

## Purpose

This document defines the TypeScript coding style used across the laboratory.
Its goal is to ensure consistency, readability and maintainability across frontend applications, backend services and shared libraries.

## Scope

These guidelines apply to:
- All TypeScript code in the laboratory
- Frontend and backend projects
- Shared libraries and tooling

This document does not replace linting rules.
Linting and formatting are enforced through shared tooling where applicable.

## General Principles

### Prefer clarity over conciseness

Readable and explicit code is preferred over compact or clever constructs.
Code should optimize for understanding by future readers.

## Type System Usage

### Use `strict` mode

- All projects must enable TypeScript `strict` mode.
- Disabling strict checks is not allowed without explicit justification.

### Prefer `type` for unions and primitives

Use `type` aliases for unions, primitives and simple object shapes.

```ts
type DocumentId = string;
type PageSize = 'A4' | 'A5' | 'Letter';
```

### Prefer `interface` for public object contracts

Use `interface` when defining public APIs or extensible object shapes.

```ts
interface PdfRendererOptions {
  pageSize: PageSize;
  margins: number;
}
```

### Avoid `any`

* The `any` type must not be used.
* Use `unknown` when the type is not known and narrow it explicitly.

```ts
function parseInput(input: unknown): string {
  if (typeof input !== 'string') {
    throw new Error('Invalid input');
  }
  return input;
}
```

## Immutability

### Prefer `readonly`

* Use `readonly` for properties that should not change after initialization.
* Prefer immutable data structures where reasonable.

```ts
interface Page {
  readonly width: number;
  readonly height: number;
}
```

### Avoid mutating function parameters

Functions should not mutate their input arguments unless explicitly documented.

## Functions and Methods

### Prefer small, focused functions

* Functions should do one thing.
* Long functions should be decomposed into smaller units.

### Prefer named functions over anonymous ones

Named functions improve stack traces and readability.

```ts
function renderPage(page: Page): void {
  // ...
}
```

## Null and Undefined Handling

### Be explicit

* Prefer explicit checks for `null` and `undefined`.
* Avoid relying on truthy/falsy behavior for control flow when values are not boolean.

```ts
if (value === undefined) {
  return;
}
```

### Use nullish coalescing (`??`) intentionally

Use `??` only when `null` and `undefined` are valid absence values.

```ts
const margin = options.margin ?? DEFAULT_MARGIN;
```

## Enums and Constants

### Prefer union types over enums

Union types are preferred for simple value sets.

```ts
type Alignment = 'left' | 'center' | 'right';
```

#### When to use `enum`

Use `enum` only when a **runtime representation is required** and provides clear value.

Typical valid use cases include:

1. **Mapping values to behavior or configuration**
  When values are used as keys to map behavior, configuration or metadata.

```ts
enum PageSize {
  A4 = 'A4',
  A5 = 'A5',
}

const pageWidths: Record<PageSize, number> = {
  [PageSize.A4]: 210,
  [PageSize.A5]: 148,
};
```

2. **Shared contracts between frontend and backend**
    When values represent a shared contract exchanged through APIs or events.

```ts
enum OrderStatus {
  Pending = 'pending',
  Paid = 'paid',
  Cancelled = 'cancelled',
}
```

3. **Configuration and feature flags with a closed set of options**
   When a configuration parameter must be restricted to a known set of valid values.

```ts
enum LogLevel {
  Debug = 'debug',
  Info = 'info',
  Warn = 'warn',
  Error = 'error',
}
```

4. **Finite state modeling**
   When modeling explicit and finite states that are evaluated at runtime.

```ts
enum UploadState {
  Idle = 'idle',
  Uploading = 'uploading',
  Completed = 'completed',
  Failed = 'failed',
}
```

5. **Interoperability with external standards or protocols**
   When values correspond to well-known external constants or specifications.

```ts
enum HttpMethod {
  GET = 'GET',
  POST = 'POST',
  PUT = 'PUT',
  DELETE = 'DELETE',
}
```

#### When **not** to use `enum`

* When values are only needed for type checking
* When no runtime access or iteration is required
* When a union type can express the domain more simply

In these cases, prefer **union types** or `as const` objects.

### Constants

* Use `UPPER_SNAKE_CASE` for true constants.
* Avoid exporting constants unnecessarily.

```ts
const DEFAULT_PAGE_MARGIN = 40;
```

## Imports and Exports

### Prefer named exports

* Avoid default exports unless there is a strong reason.
* Named exports improve refactoring and auto-imports.

```ts
export function createRenderer() {}
```

### Avoid deep barrel exports

* Barrel files (`index.ts`) should be shallow and intentional.
* Avoid barrels that hide large internal structures.

## Error Handling

### Prefer explicit error types

* Throw meaningful errors.
* Avoid throwing generic `Error` when domain-specific errors make sense.

```ts
class InvalidTemplateError extends Error {}
```

## Documentation

### Public APIs must be documented

Public APIs represent contracts and must be documented to ensure correct usage and safe evolution.

Documentation should prioritize **module-level documentation** (e.g. a `README.md` within the module or package) including:
- Purpose and responsibilities
- Public surface area (what is considered API)
- Usage examples
- Constraints, guarantees and non-goals

Inline documentation (JSDoc or comments) is discouraged by default and should only be used when it provides essential clarity that cannot be expressed through naming and structure.

## Exceptions

### Exceptions should be self-explanatory

Exceptions to these guidelines should be avoided whenever possible.
If an exception is required, it must remain **self-explanatory through design**, meaning:
- clear naming
- explicit structure
- minimal and isolated impact

If additional context is needed, it must be documented in **module-level documentation** (e.g. `README.md`), not as inline code comments.

Exceptions must be local and must not be propagated as a general pattern.

## Summary

* Use strict TypeScript configuration
* Avoid `any`
* Prefer explicit and readable constructs
* Keep APIs clear and stable
* Consistency is more important than personal preference