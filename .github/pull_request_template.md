## Summary

<!-- What changed and why? Keep this concise and user-impact focused. -->

## Related Context

<!-- Link related issue(s), requirement docs, or design task(s). -->
- Requirement(s): 
- Design/Task doc(s):
- Issue(s):

## Scope of Change

- [ ] Frontend (`src/frontend/**`)
- [ ] Backend (`src/backend/**`)
- [ ] API/contract
- [ ] Documentation
- [ ] Tests only
- [ ] Refactor (no behavior change)

## Requirements & Design Alignment

<!-- Confirm alignment with requirements/design, or explicitly describe intended deltas. -->
- Requirements source checked: `docs/requirements/001- final_requirements.md`
- Design source checked: `tasks/002- tech_design.md`
- Contract changes introduced?  
  - [ ] No  
  - [ ] Yes (describe and list all synchronized updates below)

## Contract/Schema Changes (if applicable)

<!-- Required when API payloads, DTOs, validation rules, or response behavior changed. -->
- [ ] Frontend updated
- [ ] Backend updated
- [ ] Tests updated
- [ ] Docs updated
- Notes:

## Testing

### What I ran

- [ ] Frontend tests (`npm test` in `src/frontend` or workspace test task)
- [ ] Backend tests (`dotnet test` in `src/backend`)
- [ ] Both suites (for cross-stack changes)
- [ ] Lint/format checks (if applicable)

### Results

<!-- Paste concise results or summary. -->
- Outcome:
- If tests were not run, explain why and risk impact:

## Documentation Checklist

- [ ] No documentation impact
- [ ] Updated `docs/frontend/*` (for UI/UX/component/state/routing changes)
- [ ] Updated `docs/backend/*` (for API/domain/persistence/ops changes)
- [ ] Updated `docs/requirements/*` (only if requirement/contract changed)
- [ ] Updated `tasks/*` (design/implementation artifacts as needed)

## Risk & Rollback

- Risk level: [ ] Low [ ] Medium [ ] High
- Main risks:
- Rollback plan:

## Reviewer Guidance (Copilot + Humans)

Please review using:

1. `.github/instructions/code-review.instructions.md` (global review baseline)
2. Scoped instructions based on changed files:
   - Frontend:
     - `src/frontend/.github/instructions/angular.instructions.md`
     - `src/frontend/.github/instructions/angular-testing.instructions.md` (if tests affected)
     - `src/frontend/AGENTS.md`
   - Backend:
     - `src/backend/.github/instructions/dotnet.instructions.md`
     - `src/backend/.github/instructions/dotnet-testing.instructions.md` (if tests affected)
   - Documentation:
     - `.github/instructions/documentation.instructions.md`

### Review focus requested by author

<!-- Optional: ask reviewers to focus on specific risk areas, tradeoffs, or uncertain decisions. -->
