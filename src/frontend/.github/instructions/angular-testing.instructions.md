---
description: "Use when creating or updating Angular unit tests, component tests, service tests, or Vitest specs for the Todo app frontend. Covers Vitest, Angular TestBed, signals, reactive forms, router state, and task UI behavior."
name: "Todo Angular Testing Guidelines"
applyTo: "src/**/*.spec.ts, src/**/*.test.ts"
---

# Angular Testing Guidelines

Use these instructions when generating or modifying frontend tests for the Todo app.

## Required Testing Stack

- Use `Vitest` as the test runner.
- Use Angular `TestBed` for component and service tests.
- Use the Angular workspace test command already defined in the project.
- Keep tests compatible with the current Angular build-based test setup rather than introducing a separate custom runner configuration without need.

## General Testing Approach

- Prefer focused unit and component tests close to the feature being exercised.
- Import standalone components directly in tests.
- Keep tests aligned with Angular 21 patterns and the project rules around signals, standalone components, OnPush change detection, and reactive forms.
- Structure tests with Arrange-Act-Assert and use descriptive behavior-oriented names.
- Test observable behavior in the DOM, emitted outputs, router state, and service calls rather than private implementation details.

## What to Cover

At a minimum, cover the Todo app behavior that matters to users and to the frontend-backend contract:

- task list rendering with default state
- loading, empty, and error UI states
- overdue visual differentiation for incomplete overdue tasks
- create and edit drawer behavior
- reactive form validation for title, description, and tag limits
- completion toggle behavior
- delete flows and list refresh behavior
- search, priority filtering, and multi-tag OR filtering
- pagination interactions with fixed page size expectations
- URL query parameter synchronization and restore behavior
- service request construction for backend query params and payloads

## Component Testing Guidance

- Import the standalone component under test directly into `TestBed`.
- Stub child components only when they are not part of the behavior being verified.
- Call `fixture.detectChanges()` after state changes that affect the template.
- Use `await fixture.whenStable()` when the template depends on async work.
- For OnPush components, make assertions after the state update and change detection cycle.
- Prefer semantic DOM assertions that reflect the visible UX.

## Service and HTTP Testing Guidance

- Test API services separately from components.
- Verify query parameter construction for `q`, `priority`, repeated `tag`, sort fields, page, and page size.
- Verify that frontend defaults stay aligned with backend limits and contracts.
- Mock HTTP interactions with Angular testing utilities rather than making real network calls.
- If the test uses `HttpClient`, prefer Angular's testing providers for HTTP rather than ad hoc spies.

## Signals, Forms, and Router State

- Test signal-driven state transitions through public behavior.
- Prefer `set()` and `update()`-driven flows; keep assertions aligned with computed state and rendered output.
- For reactive forms, cover both valid and invalid states.
- Assert validation messages or invalid control states for title required, title max length, description max length, and tag count limits.
- When URL state matters, test router query param reads and writes explicitly.

## Quality Rules

- Keep tests deterministic.
- Use fixed input dates when testing overdue behavior.
- Avoid brittle selectors tied to incidental markup when a stable semantic query is available.
- Keep one behavior per test unless a single user flow is clearer as one spec.
- Reuse small setup helpers when they reduce duplication without hiding intent.

## What to Avoid

- Do not test private methods directly.
- Do not couple tests to internal signal implementation details when DOM or public state is sufficient.
- Do not introduce template-driven form test patterns in this codebase.
- Do not add a second frontend testing framework when Vitest and TestBed already cover the need.
- Do not write non-descriptive test names such as `should work`.
