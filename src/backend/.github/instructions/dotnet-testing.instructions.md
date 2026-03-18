---
description: "Use when creating or updating .NET backend unit tests, endpoint tests, integration tests, validators, or service tests for the Todo app. Covers xUnit, FluentAssertions, Moq, WebApplicationFactory, and required coverage for API, application, and infrastructure behavior."
name: "Todo Backend Testing Guidelines"
---

# Backend Testing Guidelines

Use these instructions when generating or modifying backend tests for the Todo app.

## Test Project Structure

- Create tests in a separate backend test project or module rather than inside `Todo.API`.
- Prefer a clear name such as `Todo.API.Tests` or `Todo.Tests`.
- Mirror the production structure in test folders when it helps navigation, for example `Endpoints/`, `Services/`, `Validators/`, and `Infrastructure/`.
- Keep test setup reusable, but do not hide the behavior under overly clever abstractions.

## Required Testing Stack

- Use `xUnit` as the default test framework.
- Use `FluentAssertions` for readable assertions.
- Use `Moq` only when mocking a collaborator adds clarity and keeps the test unit-scoped.
- Use `Microsoft.AspNetCore.Mvc.Testing` for endpoint coverage against the minimal API surface.
- Prefer realistic EF Core testing for data access behavior. If query translation or persistence behavior matters, use SQLite-based tests instead of mocking EF Core.

## Coverage Expectations

Before writing tests, analyze the backend codebase and identify the business logic, services, validators, endpoint behavior, and infrastructure code that materially affect application behavior.

At a minimum, cover:

- all task endpoints
- service-layer business rules
- request validators and query validators
- success paths
- validation failures
- not-found paths
- concurrency or conflict behavior when implemented
- pagination boundaries and invalid page size handling
- default sorting behavior
- title-only search behavior
- OR-based tag filtering behavior
- soft-delete behavior and exclusion from active lists
- completion toggle behavior in both directions
- ProblemDetails error responses for expected failures

## Unit vs Integration Guidance

- Use unit tests for validators, pure business logic, mapping helpers, and small service methods with isolated collaborators.
- Use integration-style tests for minimal API endpoints, request/response contracts, middleware behavior, and EF-backed query behavior.
- If an endpoint test needs routing, JSON serialization, filters, middleware, and ProblemDetails behavior, use `WebApplicationFactory` instead of piecing together mocks.
- If a service is mostly LINQ and EF query composition, prefer a database-backed test over a heavily mocked query provider.

## Test Design Rules

- Follow the Arrange-Act-Assert pattern.
- Use descriptive test names that explain behavior, for example `ListTasks_returns_default_sorted_first_page_when_no_filters_are_provided`.
- Keep each test focused on one behavior.
- Make tests deterministic. Control time explicitly if overdue, retention, or TTL logic depends on the current clock.
- Do not share mutable state across tests.
- Keep fixtures and builders simple and explicit.
- Prefer data builders or helper methods for valid default requests, then override only the field under test.

## Endpoint Test Expectations

- Assert both HTTP status codes and response payloads.
- Verify ProblemDetails shape for `400`, `404`, and `409` responses when applicable.
- Cover the full endpoint surface for:
  - `GET /api/tasks`
  - `GET /api/tasks/{id}`
  - `POST /api/tasks`
  - `PUT /api/tasks/{id}`
  - `PATCH /api/tasks/{id}/completed`
  - `DELETE /api/tasks/{id}`
- Include tests for default query behavior and combined filters where the API contract requires it.

## Validator and Service Test Expectations

- Validators should assert each documented rule and at least one valid request.
- Service tests should cover happy paths, edge cases, and failure behavior rather than only object construction.
- Where services orchestrate persistence, assert observable outcomes, not private implementation details.
- If service behavior is defined by requirements documents, align assertions to those requirements rather than ad hoc assumptions.

## What to Avoid

- Do not put backend tests inside the production project.
- Do not mock every dependency by default.
- Do not rely on fragile assertions against internal implementation details.
- Do not write vague test names such as `ShouldWork` or `Test1`.
- Do not skip negative-path testing for validation, paging limits, or missing entities.