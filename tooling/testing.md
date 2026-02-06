# Tooling — Testing

This document defines the testing standards used across the ecosystem.  
Its purpose is to ensure correctness, prevent regressions, and support safe refactoring.

## Purpose

- Validate business behavior and edge cases
- Prevent regressions during refactors
- Enable confident changes and long-term maintainability
- Keep tests reliable, readable, and fast

## Scope

Testing applies to:
- Business logic
- Application services
- Integration boundaries
- Critical infrastructure behavior

Tests must be excluded from production builds.

## Testing Philosophy

### Test behavior, not implementation

- Focus on inputs and outputs.
- Avoid asserting internal state or private methods.
- Refactors should not require rewriting tests.

### Prefer fewer meaningful tests

- One good test is better than many shallow ones.
- Avoid tests that exist only to increase coverage.

### Tests are part of the codebase

- Tests must follow the same quality standards as production code.
- Readability matters more than clever setups.

## Test Types

### Unit Tests

- Test pure logic in isolation.
- No IO, no network, no filesystem.
- Fast and deterministic.

Use for:
- Domain rules
- Calculations
- Decision logic

### Integration Tests

- Test interaction between components.
- May involve:
  - Database
  - HTTP layer
  - External services (stubbed or sandboxed)

Rules:
- Keep boundaries explicit.
- Control external dependencies.

### End-to-End Tests

- Validate full flows from entry point to response.
- Use sparingly.
- Focus on critical paths only.

## Determinism

All tests must be deterministic:

- No dependency on:
  - Current time
  - Randomness
  - Network availability
- Use:
  - Fixed data
  - Controlled clocks
  - Explicit seeds

## Isolation and State

- Tests must not share state.
- Clean up after execution.
- Avoid relying on execution order.

## Test Data

- Prefer explicit fixtures.
- Avoid complex builders unless reused.
- Test data must be easy to reason about.

## Mocks and Stubs

- Prefer real implementations where cheap.
- Mock only:
  - Slow
  - Unreliable
  - External systems

Rules:
- Avoid deep mocking
- Avoid mocking what you don’t own
- Prefer stubs over spies

## Error Cases

- Test failure scenarios explicitly.
- Assert error types and messages where meaningful.
- Do not rely on generic error matching.

## Coverage

- Coverage is a **signal**, not a goal.
- Minimum thresholds may exist, but:
  - Coverage alone does not imply quality
  - Untestable code should be reconsidered

## Naming and Structure

- Test names must describe behavior.

```ts
it('returns 404 when user does not exist', () => {});
```

* Structure tests to clearly separate:
  * Arrange
  * Act
  * Assert

## Tooling

* Test runner choice is stack-dependent.
* Tests must be runnable via CLI.

Every repo must expose:

* `test` → runs all tests
* `test:ci` → CI-friendly execution
* `test:coverage` → runs tests with coverage
* `test:watch` → local development

## CI Policy

* All tests must run in CI.
* No flaky tests allowed.
* A failing test blocks merges.

## Documentation

* Non-obvious testing strategies must be documented at module level.
* Avoid inline explanations unless the behavior is genuinely unclear.

## Final Rule

If tests slow down development or fail randomly,the testing strategy is wrong.
