# Code Review Instructions (Repository-Wide)

Use this file as the default reference for pull request reviews in this repository.  
Keep feedback actionable, evidence-based, and aligned with the repository’s existing instruction files and architecture constraints.

## Review Objectives

Prioritize findings that impact:

1. Correctness and functional behavior
2. Contract and requirement stability
3. Security and data safety
4. Maintainability and readability
5. Test coverage and reliability
6. Documentation completeness

Focus on high-signal findings, not stylistic noise.

## Source Of Truth And Conflict Resolution

When reviewing, validate changes against:

- `docs/requirements/001- final_requirements.md` (stable product/API behavior)
- `tasks/002- tech_design.md` (current architecture/layering/API/documentation style)

If implementation, docs, and requirements conflict, call it out explicitly and request resolution.  
Do not assume intent when sources disagree.

## Scope Routing (Must Apply)

For changed files, apply the relevant scoped instructions instead of reinterpreting rules:

- Frontend (`src/frontend/**`):
  - `src/frontend/.github/instructions/angular.instructions.md`
  - `src/frontend/.github/instructions/angular-testing.instructions.md` (when tests are affected)
  - `src/frontend/AGENTS.md`
- Backend (`src/backend/**`):
  - `src/backend/.github/instructions/dotnet.instructions.md`
  - `src/backend/.github/instructions/dotnet-testing.instructions.md` (when tests are affected)
- Documentation (`docs/**`, `tasks/**`):
  - `.github/instructions/documentation.instructions.md`

Do not duplicate detailed Angular/.NET/testing guidance in review comments; enforce and reference the scoped files.

## Review Checklist

### 1) Requirements And Contract Safety
- Verify behavior remains consistent with requirements unless PR explicitly changes requirements.
- Confirm frontend-backend contract compatibility is preserved.
- If contract changes are intentional, ensure frontend, backend, tests, and docs are updated together.

### 2) Architecture And Layering
- Check alignment with `tasks/002- tech_design.md` layering and API shape.
- Flag cross-layer leakage, hidden coupling, or bypassed boundaries.
- Prefer focused, incremental changes; flag unnecessary broad refactors.

### 3) Code Quality
- Validate clarity, cohesion, and naming.
- Look for duplicated logic, dead code, and avoidable complexity.
- Ensure error handling is explicit and meaningful.
- Ensure changes follow existing project patterns rather than introducing ad hoc patterns.

### 4) Security And Reliability
- Flag unsafe input handling, missing validation, auth/authz gaps, secret exposure, and risky defaults.
- Check null/undefined handling, edge-case behavior, and failure-path correctness.
- Ensure user-facing failures are handled predictably.

### 5) Testing Expectations
- Confirm tests were added/updated for changed behavior.
- Confirm relevant test suites were run:
  - Frontend changes: workspace test task or `npm test` in `src/frontend`
  - Backend changes: `dotnet test` in `src/backend`
  - Cross-stack changes: both suites
- If tests could not run, require explicit reason and impact statement.
- If backend behavior changed without existing coverage, require minimal appropriate backend tests.

### 6) Documentation Expectations
- Confirm docs are updated in the same PR when behavior/architecture changes.
- Validate docs are placed in correct locations:
  - `docs/backend/` for backend behavior/architecture/API/persistence/ops
  - `docs/frontend/` for UI behavior/components/routing/state/interactions
  - `docs/requirements/` only for product requirement/contract changes
  - `tasks/` for design/implementation planning artifacts
- Ensure documentation matches code and does not conflict with requirements/design docs.

## Feedback Style

- Be specific: reference file, function/class, and behavior.
- Explain impact and why it matters.
- Provide concrete fix guidance (or acceptable alternatives).
- Prioritize findings by severity:
  - **Blocking**: correctness, security, contract, missing required tests/docs
  - **Non-blocking**: maintainability improvements, minor simplifications
- Avoid requesting preference-only changes unless a repository rule supports them.

## PR Completion Gate (Review Verdict)

Do not approve if any of the following are unresolved for affected scope:

1. Implementation changes incomplete or inconsistent
2. Required tests missing/insufficient or not run
3. Required documentation updates missing
4. Conflicts with requirements or tech design not explicitly resolved

If all checks pass, summarize residual risks (if any) and approve.
