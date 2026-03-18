# Repository Instructions

This file defines the always-on rules for work in this repository. Keep it thin. Do not duplicate the detailed Angular, .NET, or testing guidance that already exists in scoped instruction files.

## Source Of Truth

- Use `docs/requirements/001- final_requirements.md` for product and API behavior that must remain stable.
- Use `tasks/002- tech_design.md` for the current architecture, layering, API shape, and documentation style.
- When requirements, implementation, and documentation conflict, resolve the conflict explicitly instead of guessing.

## Scope Routing

- For frontend work in `src/frontend`, follow:
  - `src/frontend/.github/instructions/angular.instructions.md`
  - `src/frontend/.github/instructions/angular-testing.instructions.md` when tests are involved
  - `src/frontend/AGENTS.md`
- For backend work in `src/backend`, follow:
  - `src/backend/.github/instructions/dotnet.instructions.md`
  - `src/backend/.github/instructions/dotnet-testing.instructions.md` when tests are involved
- For documentation work in `docs/` and `tasks/`, follow:
  - `.github/instructions/documentation.instructions.md`

Do not restate those files inside new instructions. Reference them and apply the right one for the task.

## Working Rules

- Keep changes aligned with the existing split between Angular frontend, .NET backend, requirements, and design artifacts.
- Preserve the frontend-backend contract unless the task explicitly changes it, then update code, tests, and documentation together.
- Prefer focused, incremental changes over broad refactors.
- Treat requirements and tech design as implementation constraints, not optional background reading.

## Definition Of Done

A task is not complete until all of the following are handled for the affected area:

1. Implementation is updated.
2. Relevant unit or integration tests are added or updated.
3. Relevant tests are run.
4. Relevant documentation is updated.

## Test Execution Expectations

- Frontend: run the workspace test task or `npm test` from `src/frontend` after frontend changes.
- Backend: run `dotnet test` from `src/backend` after backend changes.
- If a backend change introduces behavior that is not yet covered because no backend test project exists, create the smallest appropriate test coverage that follows the backend testing instructions, then run `dotnet test`.
- If a task affects both frontend and backend behavior, run both relevant test suites.
- If tests cannot run, state why clearly and do not present the task as complete.

## Documentation Expectations

- Update the relevant documentation in the same task.
- Use `docs/backend/` for backend architecture, API, persistence, and operational behavior.
- Use `docs/frontend/` for UI behavior, component structure, routing, state, and interaction flows.
- Use `docs/requirements/` only when product requirements or contractual behavior change.
- Use `tasks/` for working design artifacts, implementation plans, and technical design updates.
- Keep documentation consistent with `.github/instructions/documentation.instructions.md`.

## Practical Reminders

- Prefer existing workspace tasks when available.
- Do not introduce new frameworks or architecture layers unless the task requires them.
- Do not mark work finished while tests or docs are still pending.