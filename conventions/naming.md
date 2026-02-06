# Naming Conventions

## Purpose

This document defines naming conventions used across the laboratory to improve consistency, readability and discoverability.
It provides global rules and context-specific rules for different project types.

## Scope

These rules apply to:
- GitHub repositories
- npm packages
- folders and files
- TypeScript/JavaScript code (frontend and backend)

This document does not cover:
- code formatting (handled by Prettier)
- linting rules (handled by ESLint configs)

## Global Rules

### 1. Use consistent English names

- Use English for identifiers, file names, folder names and documentation titles.
- Avoid mixing languages within the same project.

### 2. Prefer descriptive names over abbreviations

- Use abbreviations only when they are universally understood (e.g., `id`, `url`, `api`).
- Avoid internal slang or unclear acronyms.

### 3. Match naming to responsibility

- Names should reflect what a thing *does* and its *role* (e.g., `InvoiceParser`, `PdfLayoutEngine`).
- Avoid overly generic names like `Utils`, `Common`, `Helper` unless scoped to a very specific domain.

## Repository Naming (GitHub)

### Pattern

Use `kebab-case` for repositories.

**Recommended**
- `pdf-generator`
- `lab-guidelines`
- `backend-components`
- `angular-ui-components`

**Avoid**
- `PdfGenerator` (mixed casing)
- `backendComponents` (camelCase)
- `repo1` (non-descriptive)

### Optional prefixes (only when needed)

Use prefixes only to disambiguate large ecosystems:
- `<app-name>-<project-type>` for applications (e.g., `pdf-generator-service` or `pdf-generator-frontend`)
- `<scope>-<type>` for libraries (e.g., `angular-components` or `backend-models`)
- `<tool-name>-tool` for tooling (e.g., `eslint-config-tool`)

If prefixes are used, they must be used consistently across the ecosystem.

## Package Naming (npm)

### Pattern

Use scoped packages: `@beyonda-labs/<package-name>` where `<package-name>` is `kebab-case`.

**Examples**
- `@beyonda-labs/pdf-generator-service`
- `@beyonda-labs/backend-models`
- `@beyonda-labs/angular-components`
- `@beyonda-labs/eslint-config-tool`

### Package naming rules

- Avoid generic names like `core`, `common`, `shared` unless they represent a real, stable foundation.
- Prefer names that describe the capability: `pdf-layout`, `schema-validation`, `http-client`.

## Folder and File Naming

### General

- Use `kebab-case` for folders and file names.
- Group by feature or domain rather than by technical type whenever it improves clarity.

**Examples**
- `invoice-parser.ts`
- `pdf-layout-engine.ts`
- `render-pipeline/`
- `schema/`

### Index files

- Use `index.ts` only for module entry points and well-defined barrels.
- Avoid deep barrel exports that hide structure and create circular dependencies.

## TypeScript / JavaScript Naming

### Identifiers

- `camelCase` for variables, functions and methods
- `PascalCase` for types, classes and enums
- `UPPER_SNAKE_CASE` for constants (only for true constants)

**Examples**
- `createRenderer()`
- `renderDocument()`
- `PdfRenderer`
- `PdfLayoutOptions`
- `DEFAULT_PAGE_SIZE`

### Booleans

- Use `is/has/can/should` prefixes.

**Examples**
- `isEnabled`
- `hasSelection`
- `canRetry`
- `shouldCache`

### Collections

- Use plural names for arrays/lists.

**Examples**
- `pages`, `items`, `rules`

## Context-Specific Rules

### Frontend (Angular)

- Component classes: `PascalCase` ending with `Component`
  - `InvoiceFormComponent`
- Service classes: `PascalCase` ending with `Service`
  - `PdfExportService`
- Directive classes: `...Directive`
- Pipe classes: `...Pipe`

**Files**
- Components: `kebab-case.component.ts`
- Services: `kebab-case.service.ts`
- Directives: `kebab-case.directive.ts`
- Pipes: `kebab-case.pipe.ts`

**Selectors**
- Use a consistent prefix: `bey-` for components of libraries or `<app>-` for components of applications
  - `bey-modal`, `app-home`

### Backend (Node / APIs)

- Prefer naming by domain capability:
  - `request-context`, `error-handler`, `config-loader`
- Avoid framework-specific suffixes unless required:
  - Use `middleware` when it is actually Express middleware.

**Files**
- Use `*.middleware.ts`, `*.controller.ts`, `*.route.ts` only when the architecture requires those layers.

## Naming for “Core” and “Shared” Modules

Use `core` only for foundational modules that are:
- stable
- widely used across projects
- low-level and dependency-light

Prefer capability-based naming:
- `errors` instead of `common-errors`
- `logging` instead of `shared-logger`

## Exceptions

If a rule must be broken:
- document the reason in the project README (short note)
- keep the exception local (do not propagate the pattern)

## Summary

- Repositories and packages use `kebab-case`
- Code follows TypeScript conventions (`camelCase` / `PascalCase`)
- Context-specific suffixes exist for Angular and backend layers
- Avoid vague names and uncontrolled “shared/common” buckets
