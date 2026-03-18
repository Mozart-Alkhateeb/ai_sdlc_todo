# Todo App MVP Delivery Artifacts

## 1. Stories and Gherkin Acceptance Criteria

- **US-01 (List Default View)**  
	**Story (INVEST):** As an end user, I want to see a task list on first load with sensible defaults, so that I can immediately understand my current work.

	```gherkin
	Scenario: Load default task list view
		Given I open the Todo app for the first time
		When the task list finishes loading
		Then I should see tasks sorted by priority descending and then due date descending
		And I should see at most 10 tasks on the page
		And each task row should display title, priority, due date (if present), tags, and completion status
	```

- **US-02 (Create Task in Drawer)**  
	**Story (INVEST):** As an end user, I want to create a new task from a right-side drawer, so that I can add work without leaving the main list context.

	```gherkin
	Scenario: Create a new task from the right-side drawer
		Given I am on the task list page
		When I click the Create Task action
		Then a right-side drawer should open with a task form
		When I enter a valid title and submit
		Then the drawer should close
		And the new task should appear in the list using the default sort behavior
		And the new task priority should default to medium if I did not set one
	```

- **US-03 (Edit Task in Same Drawer)**  
	**Story (INVEST):** As an end user, I want to edit an existing task in the same right-side drawer used for creation, so that the experience stays consistent and quick.

	```gherkin
	Scenario: Edit a task using the shared create/edit drawer
		Given I can see an existing task in the list
		When I click Edit on that task
		Then the right-side drawer should open with the task's current values prefilled
		When I update one or more fields and save
		Then the drawer should close
		And the task row should show the updated values in the list
	```

- **US-04 (Toggle Complete and Reopen)**  
	**Story (INVEST):** As an end user, I want to mark a task as completed and later reopen it, so that I can correct status changes when plans evolve.

	```gherkin
	Scenario: Toggle task completion state both directions
		Given I can see a task that is not completed
		When I mark the task as completed
		Then the task should show a completed visual state
		When I toggle the same task back to not completed
		Then the completed visual state should be removed
		And the task should remain visible in the list
	```

- **US-05 (Soft Delete Task)**  
	**Story (INVEST):** As an end user, I want to delete a task from my active view, so that my list stays focused on current items.

	```gherkin
	Scenario: Soft delete removes task from active list
		Given I can see a task in the active task list
		When I choose Delete for that task and confirm
		Then the task should no longer appear in the active list
		And refreshing the page should keep the task hidden from the active list
		And no restore-from-delete action should be shown in the MVP UI
	```

- **US-06 (Search by Title)**  
	**Story (INVEST):** As an end user, I want to search tasks by title keywords, so that I can quickly find the task I care about.

	```gherkin
	Scenario: Search only within task titles
		Given I have tasks with different titles and descriptions
		When I enter a keyword into the search field
		Then only tasks with matching titles should be shown
		And tasks that match only in description should not be shown
		And clearing the search should restore the previous unsearched list state
	```

- **US-07 (Filter by Priority)**  
	**Story (INVEST):** As an end user, I want to filter tasks by priority, so that I can focus on urgent or low-priority work as needed.

	```gherkin
	Scenario: Filter list by selected priority
		Given I am viewing the task list
		When I apply a High priority filter
		Then only tasks with High priority should be displayed
		And removing the filter should show tasks from all priorities again
	```

- **US-08 (Filter by Tags with OR Logic)**  
	**Story (INVEST):** As an end user, I want to filter by multiple tags using OR behavior, so that I can see tasks related to any selected context.

	```gherkin
	Scenario: Multi-tag filter uses OR semantics
		Given tasks exist with tags Home, Work, and Errand
		When I select tag filters Home and Work
		Then I should see tasks tagged Home or Work
		And tasks with neither Home nor Work tags should be hidden
	```

- **US-09 (Persist List State in URL)**  
	**Story (INVEST):** As an end user, I want my list state saved in the URL, so that I can refresh or share the page without losing search, filters, sorting, or page selection.

	```gherkin
	Scenario: Restore list state from URL query parameters
		Given I applied search, priority filter, tag filter, sort, and pagination
		And the URL contains matching query parameters
		When I refresh the browser
		Then the list should reload with the same search, filters, sort, and page
		When I share the URL and another user opens it
		Then they should see the same list state
	```

- **US-10 (Pagination Controls)**  
	**Story (INVEST):** As an end user, I want to navigate through paginated tasks, so that I can browse larger task collections without overload.

	```gherkin
	Scenario: Move between pages with fixed page size
		Given there are more than 10 tasks matching the current list criteria
		When I click Next page
		Then I should see the next set of tasks
		And each page should contain up to 10 tasks
		And page size controls should not allow custom page size changes in MVP
	```

- **US-11 (Loading, Empty, Error States)**  
	**Story (INVEST):** As an end user, I want clear loading, empty, and error feedback, so that I always understand what the app is doing and what to do next.

	```gherkin
	Scenario: Show loading and empty states
		Given I open the task list page
		When data is being requested
		Then I should see a loading indicator in the list area
		When the request returns no tasks
		Then I should see an empty state message with guidance to create a task

	Scenario: Show actionable error state
		Given I open the task list page
		When the request fails
		Then I should see an error state message
		And I should see a retry action
	```

- **US-12 (Overdue Visual Differentiation)**  
	**Story (INVEST):** As an end user, I want overdue tasks visually differentiated, so that I can identify and prioritize late work at a glance.

	```gherkin
	Scenario: Apply overdue styling to late, incomplete tasks
		Given a task has a due date-time earlier than now
		And the task is not completed
		When the task list is displayed
		Then that task should use the overdue visual style
		And non-overdue tasks should not use overdue styling
	```

- **US-13 (Form Validation and Limits)**  
	**Story (INVEST):** As an end user, I want clear validation in the task form, so that I can submit correct data without confusion.

	```gherkin
	Scenario: Enforce title, description, and tag limits
		Given the create/edit drawer is open
		When I leave title empty and attempt to save
		Then I should see a required validation message for title
		When I enter more than 100 characters for title
		Then I should see a max-length validation message
		When I enter more than 1000 characters for description
		Then I should see a max-length validation message
		When I add a 6th tag
		Then I should see a validation message that limits tags to 5
	```

## 2. Backlog Table

| ID | Story | Epic | Priority | Estimate | Dependencies |
|---|---|---|---|---|---|
| US-01 | Default task list view with sorting and 10-item page | Task List Foundation | High | 5 SP (No AI) / 3 SP (With AI) | None |
| US-02 | Create task in right-side drawer | CRUD Drawer Flows | High | 8 SP (No AI) / 5 SP (With AI) | US-01 |
| US-03 | Edit task in shared create/edit drawer | CRUD Drawer Flows | High | 5 SP (No AI) / 3 SP (With AI) | US-02 |
| US-04 | Toggle complete and reopen task | CRUD Drawer Flows | High | 3 SP (No AI) / 2 SP (With AI) | US-01 |
| US-05 | Soft delete task from active list | CRUD Drawer Flows | High | 5 SP (No AI) / 3 SP (With AI) | US-01 |
| US-06 | Search tasks by title only | Filtering and Discovery | High | 5 SP (No AI) / 3 SP (With AI) | US-01 |
| US-07 | Filter tasks by priority | Filtering and Discovery | Medium | 3 SP (No AI) / 2 SP (With AI) | US-01 |
| US-08 | Filter tasks by multiple tags using OR logic | Filtering and Discovery | Medium | 5 SP (No AI) / 3 SP (With AI) | US-01 |
| US-09 | Persist list state in URL query parameters | URL State and Navigation | High | 8 SP (No AI) / 5 SP (With AI) | US-06, US-07, US-08, US-10 |
| US-10 | Paginate task list with fixed size of 10 | URL State and Navigation | High | 5 SP (No AI) / 3 SP (With AI) | US-01 |
| US-11 | Loading, empty, and error states in list UX | Usability and Feedback | High | 5 SP (No AI) / 3 SP (With AI) | US-01 |
| US-12 | Overdue task visual differentiation | Usability and Feedback | Medium | 3 SP (No AI) / 2 SP (With AI) | US-01 |
| US-13 | Form validation for field and tag limits | Validation and Guardrails | High | 5 SP (No AI) / 3 SP (With AI) | US-02 |

## 3. Sprint Plan (2 Weeks Each)

### Sprint 1 (Weeks 1-2)
- Backend enablers for List/Create/Update/Delete/Toggle APIs and query support are implemented first in the sprint to unblock UI stories.
- US-01: Default task list foundation.
- US-02: Create task drawer flow.
- US-03: Edit task in shared drawer.
- US-04: Toggle completed and reopen.
- US-05: Soft delete behavior in active list.
- US-13: Form validation and limits.
- US-11: Loading, empty, and error states (baseline implementation for list and drawer submit feedback).

### Sprint 2 (Weeks 3-4)
- Backend enablers for advanced query composition and URL-compatible parameters are finalized early in sprint.
- US-06: Search by title.
- US-07: Priority filter.
- US-08: Tag filter with OR semantics.
- US-10: Pagination controls with fixed page size 10.
- US-09: URL state persistence and shareable list state.
- US-12: Overdue visual styling and polish.
- Hardening pass: regression checks across drawer, filters, URL state, and list states.

## 4. Risks and Assumptions

### Assumptions
- Backend endpoints will support all required query parameters for search, filters, sorting, and pagination in time for Sprint 2 UI work.
- Due date values are consistently stored and returned with timezone offset so overdue detection is deterministic.
- Tag filtering OR semantics are supported by backend query behavior and parameter contract.
- Soft-delete retention (24h TTL) is enforced outside core UX flow and does not require additional MVP screens.
- Tailwind default theme remains acceptable for MVP visual delivery without custom design system scope expansion.

### Risks and Unknowns
- URL state complexity may introduce edge cases when combining search, multi-tag filters, sorting, and pagination at once.
- Timezone handling could produce incorrect overdue styling near date boundaries if client/server normalization differs.
- If backend pagination constraints are not enforced consistently, UI may surface unexpected 400 errors for malformed URLs.
- Shared create/edit drawer can accumulate form-state bugs (stale values, validation carryover) without strong test coverage.
- Soft-delete TTL cleanup process is deferred; if not implemented soon after MVP, data retention behavior may drift from requirement intent.
