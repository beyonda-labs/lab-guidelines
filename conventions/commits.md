# Commit Conventions

## Purpose

This document defines the commit message conventions used across the laboratory.
Consistent commit messages improve readability, enable automation (changelogs, releases) and provide a clear history of changes.

## Scope

These conventions apply to:
- All repositories within the laboratory
- Applications, libraries and tooling projects
- All commits

This document does not define branching strategies or release processes, which are covered separately.

## Commit Message Format

Commits must follow the **Conventional Commits** specification.

### Structure

`<type>(<scope>): <description>`

### Example

`feat(pdf-renderer): add support for page margins`

## Commit Types

### Primary Types

- **feat**: A new feature or capability
- **fix**: A bug fix
- **refactor**: Code change that neither fixes a bug nor adds a feature
- **perf**: Performance improvement
- **docs**: Documentation-only changes
- **test**: Adding or updating tests
- **chore**: Maintenance tasks (deps, configs, tooling)

### Optional Types (use sparingly)

- **build**: Build system or dependency changes
- **ci**: CI/CD configuration changes
- **style**: Code style changes with no functional impact

## Scope

### When to use a scope

- Use a scope when the change affects a **specific module, package or area**
- Omit the scope if the change is truly global

### Examples

- `feat(schema): add document layout validation`
- `fix(api): handle empty payload correctly`
- `refactor(logging): simplify logger initialization`
- `docs: update ecosystem overview`

### Scope naming rules

- Use `kebab-case`
- Match folder, package or domain names
- Avoid overly generic scopes like `core` unless well defined

## Description

### Rules

- Use the **imperative mood** (e.g. “add”, “fix”, “remove”)
- Keep it concise and descriptive
- Do not end with a period

### Examples

- `feat(schema): add document layout validation`
- `fix(api): handle empty payload correctly`
- `refactor(logging): simplify logger initialization`
- `docs: update ecosystem overview`

### Avoid

- fixed bug
- updated stuff
- changes

## Breaking Changes

Breaking changes must be **explicitly declared**.

### Syntax

`<type>(<scope>)!: <description>`

### Example

- `feat(api)!: change authentication token format`

### Description

- Breaking changes must be documented in the commit body or changelog
- They must result in a **major version bump** for libraries

## Commit Body (Optional)

Use the commit body to:
- Explain *why* a change was made
- Provide context not obvious from the diff
- Reference architectural decisions

### Example

```
feat(pdf-layout): support multi-column layout

This change introduces a new layout strategy to support
multi-column documents without affecting existing templates.
```

## Revert Commits

Reverts should use the standard Git revert format:

`revert: <original commit message>`

The body should explain the reason for the revert when relevant.

## Automation and Enforcement

- Commit message conventions are enforced via tooling (e.g. commitlint)
- Commits that do not follow these rules must not be merged
- Automation may rely on commit types to generate changelogs and releases

## Summary

- Conventional Commits are mandatory
- Clear types and scopes improve history and automation
- Breaking changes must be explicit
- Consistency is more important than personal preference