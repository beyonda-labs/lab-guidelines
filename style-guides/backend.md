# Backend Style Guide

General style guide and principles for backend development within the project ecosystem.  
These rules are **language- and framework-agnostic** and aim to ensure consistency, maintainability, and predictability.

## Purpose

- Provide code that is easy to read and reason about
- Ensure predictable behavior
- Minimize implicit magic
- Enforce clear separation of responsibilities
- Support long-term evolution and refactoring

## General Principles

### Clarity over brevity

- Prefer explicit code over “clever” solutions.
- Slightly longer but clear code is better than short but cryptic code.

### Single responsibility per unit

- A class, service, or module should have one clear responsibility.
- If it is hard to explain its purpose in one sentence, it likely does too much.

### Avoid hidden side effects

- Functions must make it clear if they:
  - Mutate data
  - Perform IO
  - Depend on external state

## Project Structure

- Clearly separate:
  - **Domain / business logic**
  - **Infrastructure** (database, HTTP, filesystem, external APIs)
  - **Entry points** (controllers, handlers, resolvers)
- The domain layer **must not depend** on infrastructure details.

Conceptual example:

```md

/domain
/application
/infrastructure
/interfaces

```

## Immutability and Mutation

* By default, **do not mutate input data**.
* If a function mutates a received object:
  * It must be obvious from the name or context.
  * Never mutate implicitly or accidentally.

```ts
// Unexpected mutation
function normalize(user) {
  user.name = user.name.trim();
}

// Explicit return
function normalize(user) {
  return { ...user, name: user.name.trim() };
}
```

## Error Handling

* Use typed errors or specific error classes.
* Avoid throwing strings or generic errors.

```ts
throw new ValidationError('Invalid email format');
```

* Do not catch errors just to ignore them.
* Each layer decides whether to:
  * Propagate
  * Transform
  * Log

## Logging

* Logging must be:
  * Structured
  * Consistent
  * Useful for diagnostics

Avoid:

* Duplicate logs
* Logs inside critical loops
* Logging sensitive information

## Configuration

* All external configuration must come from:
  * Environment variables
  * Configuration files
* Avoid magic values in code.

```ts
// wrong
const timeout = 5000;

// correct
const timeout = config.requestTimeout;
```

## Dependencies

* Inject dependencies whenever possible.
* Avoid hidden singletons or imports with side effects.
* Make testing possible without complex mocks.

## Testing

* Prioritize tests for:
  * Business logic
  * Edge cases
* A test must:
  * Be deterministic
  * Not depend on execution order
  * Not share state

## Documentation

* Code should be **self-explanatory**.
* Avoid redundant comments that restate the obvious.
* Decisions, exceptions, or non-obvious rules should live in:
  * Module-level README files
  * ADRs
  * Internal project documentation

## Exceptions to the Guide

* Exceptions must be:
  * Local
  * Explicit
  * Obvious from context

If a rule does not apply to a specific module:

* Justify it in the module documentation.
* Do not “patch” the code with defensive comments.

## Final Rule

If a decision repeatedly raises questions when reading the code,
the decision is probably wrong.
