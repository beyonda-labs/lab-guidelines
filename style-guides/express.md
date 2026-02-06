# Express Backend Style Guide

This document defines **Express-specific conventions** for backend services.  
It complements the general `backend.md` style guide and **does not replace it**.

Express is treated as a **thin HTTP layer**, not as the core of the application.

## Purpose

- Use Express as a minimal and explicit HTTP adapter
- Keep business logic framework-agnostic
- Avoid Express-specific coupling outside entry points
- Ensure predictable request/response handling

## Role of Express in the Architecture

Express is responsible only for:
- HTTP routing
- Request/response adaptation
- Middleware orchestration
- Error translation to HTTP responses

Express **must not** contain:
- Business rules
- Domain decisions
- Persistence logic
- Cross-module state

## Layer Responsibilities

### Routes

- Routes only define:
  - HTTP method
  - Path
  - Associated handler
- No logic inside route definitions.

```ts
router.post('/users', createUserHandler);
```

### Handlers / Controllers

* Act as adapters between HTTP and application logic.
* Responsible for:
  * Extracting request data
  * Calling application services
  * Mapping results to HTTP responses

Rules:
* No business logic
* No direct database access
* No shared state

### Application / Services

* Express must never be imported here.
* Services receive plain data structures.
* Services return domain results or throw domain errors.

## Request Data Handling

* Validate input **before** calling application logic.
* Validation may live in:
  * Dedicated middleware
  * Handler-level validators

Rules:
* Never trust `req.body`, `req.query`, or `req.params`
* Normalize input early

## Response Handling

* Handlers are responsible for HTTP status codes.
* Domain services must not know about HTTP semantics.

Example mapping:
* ValidationError → 400
* NotFoundError → 404
* ConflictError → 409
* UnknownError → 500

## Error Handling

* Use a centralized error-handling middleware.
* Errors are:
  * Thrown in services
  * Translated to HTTP responses at the edge

Rules:

* Do not send raw errors to the client
* Do not swallow errors silently
* Avoid try/catch inside handlers unless translating errors

## Middleware Usage

Middleware should be:
* Small
* Single-purpose
* Explicitly ordered

Typical use cases:
* Authentication
* Authorization
* Validation
* Logging
* Request context enrichment

Avoid:
* Business logic in middleware
* Hidden mutations of `req` or `res`

## Request Context

* Avoid attaching arbitrary data to `req`.
* If context is required:
  * Use a well-defined `requestContext` object
  * Populate it in a single middleware

The shape of the context must be predictable.

## Async and Errors

* All async handlers must properly propagate errors.
* Avoid unhandled promise rejections.
* Prefer async/await for readability.

## Configuration

* Express configuration must be explicit:
  * body limits
  * timeouts
  * CORS
  * security headers

No configuration defaults should be assumed.

## Testing

* Express should be tested at:
  * Routing level
  * Integration boundaries

Business logic must be testable without Express.

## Documentation

* Express-specific decisions live here.
* Route behavior and API contracts live in:
  * OpenAPI specs
  * API documentation

Avoid documenting Express mechanics in code comments.

## Final Rule

If removing Express requires rewriting business logic, the architecture is wrong.
