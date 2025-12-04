# Feature Specification: Task Manager CLI

**Feature Branch**: `1-task-manager`
**Created**: 2025-12-03
**Status**: Draft
**Input**: User description: "1. Core Features (MVP)..."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Manage Basic Tasks (Priority: P1)

As a user, I want to be able to add, list, update, delete, and mark tasks as complete so I can keep track of my essential to-dos.

**Why this priority**: These are the fundamental operations for any task management application and provide immediate value to the user.

**Independent Test**: Can be fully tested by creating a task, listing it, updating it, completing it, and then deleting it, ensuring all states are correctly reflected.

**Acceptance Scenarios**:

1.  **Given** no tasks exist, **When** I add a task with a title and description, **Then** a new task with a unique ID is created and can be listed.
2.  **Given** an existing task, **When** I update its title or description, **Then** the task's details are modified.
3.  **Given** an existing task, **When** I mark it as complete, **Then** its status changes to complete.
4.  **Given** an existing task, **When** I delete it, **Then** the task is removed from the list.
5.  **Given** multiple tasks, **When** I list them, **Then** all active tasks are displayed.

---

### User Story 2 - Organize Tasks (Priority: P2)

As a user, I want to be able to assign priorities and tags to tasks, and then search, filter, and sort my tasks so I can better organize and find specific items.

**Why this priority**: These features enhance usability and allow users to manage a larger, more complex set of tasks efficiently.

**Independent Test**: Can be fully tested by creating tasks with different priorities and tags, then verifying that search, filter, and sort commands produce the expected subsets and orderings.

**Acceptance Scenarios**:

1.  **Given** an existing task, **When** I assign a priority (e.g., high) and tags (e.g., work, urgent), **Then** the task reflects these attributes, and tags are stored lowercase and deduplicated.
2.  **Given** multiple tasks with various priorities and tags, **When** I search for a keyword, **Then** tasks containing the keyword are returned.
3.  **Given** multiple tasks with various statuses, priorities, and tags, **When** I filter by status (incomplete), priority (high), or tag (work), **Then** only matching tasks are displayed.
4.  **Given** multiple tasks with due dates, priorities, and titles, **When** I sort by due date, priority, or alphabetical order, **Then** tasks are displayed in the correct order.

---

### User Story 3 - Handle Advanced Task Scheduling (Priority: P3)

As a user, I want to set tasks as recurring and assign due dates so I can manage routine activities and be aware of deadlines.

**Why this priority**: These features provide advanced scheduling capabilities, improving long-term task management and accountability.

**Independent Test**: Can be fully tested by creating a recurring task, marking it complete and observing the next occurrence, and by setting a due date and verifying overdue detection.

**Acceptance Scenarios**:

1.  **Given** a new task, **When** I set it to repeat weekly, **Then** the task is marked as recurring, and upon completion, the next occurrence is automatically generated.
2.  **Given** a new task, **When** I assign a specific due date and time, **Then** the task displays its due date.
3.  **Given** a task with a past due date, **When** I list tasks, **Then** the task is clearly marked as overdue.

---

### Edge Cases

- What happens when a user attempts to update, delete, or complete a task with an ID that does not exist? The system should provide a clear error message.
- How does the system handle an attempt to add a task without a title? The system should reject the request and prompt for a title.
- What if an invalid date format is provided for a due date? The system should reject the input and provide an error message.
- What happens if a search query yields no results? The system should indicate no matches were found.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow creation of tasks with a title and optional description.
- **FR-002**: System MUST generate a unique ID for each task.
- **FR-003**: System MUST allow listing all tasks.
- **FR-004**: System MUST allow updating a task by its ID (title, description).
- **FR-005**: System MUST allow deleting a task by its ID.
- **FR-006**: System MUST allow toggling the completion status of a task by its ID.
- **FR-007**: System MUST allow assigning priority (e.g., high, medium, low) to a task.
- **FR-008**: System MUST allow assigning multiple tags to a task.
- **FR-009**: Tags MUST be stored in lowercase and deduplicated.
- **FR-010**: System MUST allow searching tasks by keyword.
- **FR-011**: System MUST allow filtering tasks by status (e.g., incomplete, complete), priority, and tag.
- **FR-012**: System MUST allow sorting tasks by due date, priority, and alphabetical order of title.
- **FR-013**: System MUST support recurring tasks (e.g., weekly, daily, monthly).
- **FR-014**: When a recurring task is marked complete, the system MUST automatically generate its next occurrence.
- **FR-015**: System MUST allow setting a due date and time for a task.
- **FR-016**: System MUST detect and mark tasks as overdue.
- **FR-017**: (Optional) System MAY provide local reminders via system notifications or console alerts.
- **FR-018**: System MUST store tasks in a persistent manner.
- **FR-019**: System MUST store tasks in a JSON file.

### Key Entities

-   **Task**: Represents a single to-do item.
    -   Attributes: `id` (unique identifier), `title` (string, mandatory), `description` (string, optional), `completed` (boolean), `priority` (a defined set of levels, e.g., high, medium, low), `tags` (a collection of labels), `recurrence` (string, e.g., weekly, monthly), `dueDate` (an optional date and time).

## Success Criteria *(mandatory)*

### Measurable Outcomes

-   **SC-001**: Users can successfully perform all core CRUD operations (add, list, update, delete, complete) for tasks via CLI commands with 100% data integrity.
-   **SC-002**: Task filtering, searching, and sorting operations return accurate and relevant results in under 500ms for up to 1000 tasks.
-   **SC-003**: Recurring tasks, when marked complete, correctly generate their next occurrence according to their defined schedule.
-   **SC-004**: Overdue tasks are identified and visually indicated as such within task listings.
