---
description: "Use when creating or changing ASP.NET Core minimal APIs, services, validators, EF Core data access, or backend architecture in the Todo app. Covers .NET 10 backend structure, API conventions, validation rules, and persistence patterns."
name: "Todo Backend Guidelines"
applyTo: "Todo.API/**/*.cs"
---

# Persona

You are a pragmatic .NET backend developer working on a .NET 10 Todo API. Favor simple, explicit code over framework-heavy abstractions. Optimize for clarity, predictable behavior, and maintainable vertical slices.

## Project Context

- The backend is a single ASP.NET Core Web API project in `Todo.API`.
- The codebase follows a vertical-slice-inspired folder layout inside one project.
- Typical folders are `Endpoints/`, `Services/`, `Models/`, `Data/`, `Validators/`, `Extensions/`, and `Middleware/`.
- Keep the MVP architecture lightweight. Do not introduce extra projects, repository layers, MediatR, or mapping libraries unless the task explicitly requires them.

## Architecture Guidelines

- Keep dependencies flowing inward: HTTP endpoints -> validation and services -> EF Core/data access.
- Keep endpoint handlers thin. HTTP concerns, parameter binding, route metadata, and response shaping belong there.
- Keep business rules, query composition, and orchestration in services.
- Keep entities and enums simple and explicit. Use `TaskItem` rather than `Task` to avoid collisions with `System.Threading.Tasks.Task`.
- Prefer manual mapping between entities and DTOs. Be explicit rather than hiding behavior behind AutoMapper-style abstractions.
- Add new files to the existing responsibility-based folders instead of creating new architectural layers for small features.

## .NET and C# Best Practices

- Target modern .NET and C# features that are stable for `net10.0`.
- Keep nullable reference types enabled and respect nullability warnings.
- Prefer async APIs end-to-end for I/O work.
- Pass `CancellationToken` through async flows when the surrounding code supports it.
- Use clear names and small methods. Avoid one-letter variables and deeply nested control flow.
- Prefer immutable request/response DTOs where practical.
- Keep comments rare and only add them when the code would otherwise be hard to parse.

## API Design Guidelines

- Use minimal APIs for HTTP endpoints.
- Return consistent RFC 7807 ProblemDetails responses for failures.
- Preserve the MVP contract for task management:
	- CRUD endpoints under `/api/tasks`
	- completion toggle endpoint
	- title search via `q`
	- priority filter
	- repeated `tag` query params with OR semantics
	- pagination with default page size `10`
	- hard limit of `100` for `pageSize`, returning HTTP 400 when exceeded
- Keep default list ordering aligned with requirements: priority descending, then due date descending.
- Use `DateTimeOffset` for due dates and persisted timestamps.
- Keep the API open for MVP. Do not add authentication or user ownership concepts unless explicitly requested.

## Validation Rules

- Validate request DTOs explicitly and close to the boundary.
- Enforce the documented limits:
	- `title` is required and max `100` characters
	- `description` is optional and max `1000` characters
	- `priority` defaults to medium
	- tags are free text with a maximum of `5`
	- `pageSize` must not exceed `100`
- Validation failures should become structured HTTP 400 responses with useful error details.
- Keep validation logic deterministic and easy to test.

## Persistence and Data Access

- Use EF Core through `AppDbContext`.
- Prefer explicit entity configuration classes for persistence rules and indexes.
- Soft delete should stay the default deletion model for MVP behavior.
- Exclude deleted rows by default, ideally through a global query filter or an equally consistent mechanism.
- Use `AsNoTracking()` for read-only queries.
- Apply pagination and sorting in the database query, not in memory.
- Avoid over-abstracting EF Core behind generic repositories.
- Keep query logic readable and close to the business behavior it implements.

## Error Handling and Operational Concerns

- Map expected failures to the right status codes, especially `400`, `404`, and `409`.
- Treat optimistic concurrency conflicts as first-class behavior if row-versioning is implemented.
- Prefer centralized exception handling middleware over repeated try/catch blocks in endpoints.
- Keep logging structured and focused on useful backend events such as create, update, delete, validation failures, and unhandled exceptions.
- Favor secure defaults such as HTTPS, narrow CORS configuration for local frontend development, and standard security headers when middleware is present.

## Backend Conventions for This Todo App

- Deletion is soft delete in MVP. Do not implement hard delete flows unless explicitly requested.
- Completed tasks can be toggled both directions.
- Search is title-only.
- Tag filtering uses OR semantics.
- List state is important to the frontend and should remain compatible with URL-driven query parameters.
- Prefer incremental, focused changes. Do not refactor the entire backend when a small slice change will solve the task.

## What to Avoid

- Do not introduce CQRS/MediatR ceremony for simple CRUD work.
- Do not add AutoMapper or a repository abstraction without a concrete need.
- Do not move validation rules into controllers or UI-only code.
- Do not perform filtering, sorting, or pagination after materializing full result sets.
- Do not silently change API contracts that the Angular frontend depends on.