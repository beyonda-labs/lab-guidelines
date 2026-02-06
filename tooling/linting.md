# Tooling — Linting

This document defines the linting standards used across the ecosystem.  
Its purpose is to keep code consistent, prevent common bugs, and reduce review noise.

## Purpose

- Enforce a consistent style across repositories
- Catch bugs early (unused vars, unsafe patterns, invalid imports, etc.)
- Keep formatting decisions automatic and out of PR discussions
- Provide a predictable developer experience locally and in CI

## Scope

Linting applies to:
- Source code (`src/**`)
- Tests (`test/**`, `__tests__/**`)
- Scripts (`scripts/**`)
- Configuration files when supported (JSON/YAML)

Generated files must be excluded (e.g. `dist/**`, `coverage/**`).

## Principles

### Linting must be deterministic

- The same code produces the same results locally and in CI.
- Avoid rules that depend on environment-specific paths or OS behavior.

### Formatting is not discussed

- Formatting is handled by a formatter (e.g. Prettier).
- ESLint rules must not fight the formatter.

### Prefer “safe by default” rules

- Turn on rules that prevent real issues (type safety, unreachable code, unsafe any, etc.).
- Avoid rules that are purely aesthetic or overly subjective.

## Baseline Rules

### Errors that should fail CI

- Syntax / parsing errors
- Type-aware rules violations (when TS is used)
- Unused variables/imports (with allowed patterns, see below)
- Invalid promise handling
- Unsafe or misleading constructs (fallthrough, shadowing, etc.)

### Allowed patterns

- Unused parameters allowed when explicitly prefixed:

```ts
function handler(_req, res) {
  res.sendStatus(204);
}
```

* Intentionally unused imports should be removed, not ignored.

## Configuration

### Single source of truth

Each repo must expose:

* A lint config (e.g. `.eslintrc.*` or `eslint.config.*`)
* A formatter config (e.g. `.prettierrc`)
* An ignore file (`.eslintignore` or config ignores)

Avoid duplicating rules across packages unless necessary.

### TypeScript (if applicable)

* Prefer type-aware linting for application code.
* If type-aware linting is too heavy for all files:

  * Enable it for `src/**`
  * Use lighter rules for configs/scripts

## Command Standard

Every repo must include:

* `lint` → checks only
* `lint:fix` → applies safe auto-fixes
* `format` → formats files
* `format:check` → verifies formatting in CI

Example (conceptual):

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier . --write",
    "format:check": "prettier . --check"
  }
}
```

## CI Policy

* CI must run `lint` and `format:check`.
* PRs must not be merged with lint errors.
* Auto-fix is a developer responsibility (run `lint:fix` + `format` before pushing).

## Ignoring and Exceptions

### Avoid inline disable comments

Inline suppressions should be rare.

Prefer:
* Refactor to comply
* Adjust the rule at the repo/module config level
* Document non-obvious exceptions in a module-level README

If a suppression is unavoidable:
* Keep it local (single line / single block)
* Use the smallest scope possible
* Never disable an entire category globally to fix one case

## Developer Experience

### Editor integration

* Enable “format on save”.
* Enable ESLint diagnostics on save.
* Do not rely on IDE-only behavior: CLI output is the source of truth.

### Fast feedback

* Lint should run in seconds for typical changes.
* If it becomes slow:

  * Scope type-aware linting
  * Cache results
  * Split config for tooling vs app code

## Versioning

* Pin tool versions in `package.json`.
* Upgrades must be intentional:
  * Update changelog/notes (repo-level)
  * Fix newly introduced rules in the same PR when possible

## Final Rule

If linting creates more noise than value, the configuration is wrong. Adjust rules to support development, not to punish it.
