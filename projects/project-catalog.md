# Project Catalog

Concise catalog of the ecosystem projects and their boundaries.
This is a scope map, not a roadmap.

## Purpose

- Provide a minimal, clear overview of what exists
- Define ownership and boundaries per project
- Make reuse and dependencies explicit

## Conventions

### Maturity

- **Idea** — not implemented / exploratory
- **Active** — under development and used
- **Stable** — safe to reuse, API considered stable
- **Deprecated** — kept only for compatibility

### Structure

- **Project** = top-level repository or product
- **Subproject** = independently buildable deliverable inside a project
- **Module** = reusable internal package within a project

## Catalog

### Back Components (Active)

**Type**  
Backend shared utilities

**Purpose**  
Provide reusable backend building blocks shared across services.

**Contains**  
- **Module: json-validator**
  - Validates structured JSON inputs used by services
  - Provides reusable validation rules and semantic checks

### Angular Components (Active)

**Type**  
Frontend shared library

**Purpose**  
Provide reusable Angular UI components and frontend utilities shared across applications.

**Owns**  
- Reusable UI components
- Styling and theming conventions
- Common frontend interaction patterns

**Does not own**  
- Application-specific business logic
- Backend communication rules
- Product-specific workflows

### PdfGenerator (Active)

**Type**  
Product / solution

**Purpose**  
Generate PDFs from structured definitions with predictable output and strong validation.

**Subprojects**  
- **Service (backend)**
  - PDF generation engine and API
  - Input validation (via Back Components / json-validator)
  - Rendering, layout, pagination, assets, caching, error model
- **Frontend (web)**
  - Template creation/editing (JSON definitions)
  - Validation feedback and preview flows
  - Integration with the service API

**Owns**  
- PDF definition model (as the product contract)
- Rendering engine behavior and API boundaries
- Product-level UX and workflow
