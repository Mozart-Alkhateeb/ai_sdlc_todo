# Todo App — Final Requirements (MVP)

## Stakeholder Clarifications (Questions and Answers)

1. **Q:** Is this multi-user? Is there authentication/authorization in scope?
   **A:** No user concept in MVP. App is open.

2. **Q:** If multi-user, are tasks private/shared/assignable?
   **A:** Not applicable in MVP (no user concept).

3. **Q:** Is assignment to others required?
   **A:** Not applicable in MVP (no user concept).

4. **Q:** What does soft delete mean in UX and data behavior?
   **A:** No restore/trash UX for deleted tasks. Set `isDeleted=true` and apply TTL of 24 hours. Cleanup mechanism can be handled later.

5. **Q:** Can completed tasks be restored (re-opened)?
   **A:** Yes, completion can be toggled back.

6. **Q:** How should overdue tasks be handled?
   **A:** Overdue tasks should have different styling in the UI.

7. **Q:** Is manual ordering/reordering in scope?
   **A:** Not in MVP v1.

8. **Q:** Field limits?
   **A:** `title` max 100 chars, `description` max 1000 chars.

9. **Q:** Is priority required/default?
   **A:** Default priority is `medium`.

10. **Q:** Are tags free text or predefined?
    **A:** Free-text tags.

11. **Q:** Max tags per task?
    **A:** 5 tags.

12. **Q:** Due date format/timezone handling?
    **A:** Date-time with offset.

13. **Q:** Search scope for `q`?
    **A:** Title only.

14. **Q:** Multi-tag filter logic?
    **A:** OR logic, represented with its own query parameter.

15. **Q:** Default sorting?
    **A:** Priority descending, then due date descending.

16. **Q:** Pagination defaults/configurability?
    **A:** 10 items per page, not user-configurable.

17. **Q:** Should filters/sort persist?
    **A:** Yes, store list state in URL query parameters.

18. **Q:** Create interaction pattern?
    **A:** Right-side drawer.

19. **Q:** Edit interaction pattern?
    **A:** Use the same create drawer.

20. **Q:** Required UI states?
    **A:** Include loading, empty, and error states.

21. **Q:** Target devices?
    **A:** Desktop and tablet.

22. **Q:** Performance/scale constraints?
    **A:** No user concept. Pagination is sufficient. Backend maximum page size is 100; requests above this return HTTP 400.

23. **Q:** Offline/PWA required?
    **A:** No.

24. **Q:** Accessibility requirements?
    **A:** No explicit requirement for MVP.

25. **Q:** Retention for soft-deleted tasks?
    **A:** 24 hours.

26. **Q:** Design system/component library?
    **A:** Tailwind CSS, default theme.

27. **Q:** Third-party integrations?
    **A:** None.

28. **Q:** Audit log required?
    **A:** No.

29. **Q:** Environment and CI/CD requirements?
    **A:** Not needed right now.

30. **Q:** Technical architecture constraints?
    **A:** Frontend: Angular standalone components with signals. Backend: vertical-slice architecture in a single C# project, split by responsibility using folders.

---

## 1. Product Summary
Build a simple Todo app for individuals/small teams as an open MVP (no user accounts), focused on task CRUD and list management from a single page.

## 2. MVP Scope

### 2.1 Task Operations
- Create task
- Read/list tasks
- Update task
- Soft delete task
- Toggle completed status (including restoring completed -> not completed)

### 2.2 Task Fields
- `title` (required, max 100 chars)
- `description` (optional, max 1000 chars)
- `dueDate` (optional, date-time with offset)
- `priority` (`low` | `med` | `high`, default `medium`)
- `tags` (0..5, free-text)
- `isDeleted` (internal soft-delete flag)

### 2.3 List Features
- Search by `q` (title only)
- Filter by priority
- Filter by tags (OR semantics, via dedicated query param)
- Default sort: priority DESC, then due date DESC
- Pagination: default page size 10, not user-configurable

### 2.4 UI Scope
- Single page including: list, filters, and task create/edit entry points
- Create/Edit in a right-side drawer (same drawer for both flows)
- Required UI states: loading, empty, error
- Overdue task visual differentiation via styling
- Target devices: desktop and tablet

## 3. Data Lifecycle and Deletion Rules
- Deletion is soft delete (`isDeleted=true`)
- Deleted items are retained for 24 hours (TTL)
- No restore-from-delete UX in MVP
- Deferred concern: implementation details for cleanup job/process can be handled after MVP

## 4. URL State and Query Behavior
- List state must be represented in URL query params for persistence/sharing:
  - `q`
  - priority filter
  - tag filter query param(s)
  - sort
  - pagination values

## 5. Constraints and Validation
- Backend enforces max page size of 100; requests above 100 return HTTP 400
- Frontend should constrain defaults to page size 10 and avoid exceeding backend limits
- No drag-and-drop/manual ordering in MVP v1

## 6. Non-Functional and Platform Requirements
- Offline/PWA support: out of scope
- Third-party integrations: out of scope
- Audit logging: out of scope
- Environment/CI-CD requirements: not defined for MVP
- Accessibility: no explicit requirement captured for MVP

## 7. Technology and Architecture
- Frontend:
  - Angular with standalone components
  - Signals-based state handling
  - Tailwind CSS (default theme)
- Backend:
  - Single C# project
  - Vertical-slice architecture by responsibility folders

## 8. Explicitly Out of Scope (MVP)
- Authentication and user management
- Multi-user ownership/assignment semantics
- Restore flow for deleted tasks
- Reordering tasks via drag-and-drop/manual position
- External integrations (calendar, notifications, etc.)
