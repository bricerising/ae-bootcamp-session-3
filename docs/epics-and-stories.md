# Epics and Stories

## MVP

### Epic: Due Date Support

#### Story: Add due date field to task creation form

**Acceptance Criteria**
- Users can optionally select a due date when creating a task
- Due date is stored in ISO `YYYY-MM-DD` format
- Tasks without a due date are valid and stored normally
- Invalid date values are ignored (treated as absent)

**Technical Requirements**
- Add `due_date` column to the SQLite `tasks` table (already present)
- Update `POST /api/tasks` to accept `due_date` in the request body (already present)
- Update `PUT /api/tasks/:id` to accept `due_date` in the request body (already present)
- Add date input field to `TaskForm.js` component (already present)

#### Story: Display due date on task items

**Acceptance Criteria**
- Tasks with a due date display the date in a readable format
- Tasks without a due date show no date indicator

**Technical Requirements**
- Format date string for display in `TaskList.js` using locale date formatting (already present)
- Render due date chip/badge next to task title (already present)

---

### Epic: Priority Field

#### Story: Add priority field with default P3

**Acceptance Criteria**
- New tasks created without an explicit priority are stored with priority value "P3"
- Priority field supports only values "P1", "P2", "P3"
- Users can select priority via radio-style buttons (P1, P2, P3) in the task list
- Selected priority button is displayed in blue (#07F2E6)
- Unselected priority buttons are displayed in gray (#7A7A7A)

**Technical Requirements**
- Add `priority` column to the SQLite `tasks` table with default value `'P3'`
- Update `POST /api/tasks` to accept `priority` in the request body
- Add `PUT /api/tasks/:id` endpoint to update priority for existing tasks
- Add priority radio buttons to each task item in `TaskList.js`
- Add CSS classes for priority button colors (selected: #07F2E6, unselected: #7A7A7A)

---

### Epic: Task Filtering

#### Story: Add filter tabs for All, Today, and Overdue

**Acceptance Criteria**
- Users can switch between "All", "Today", and "Overdue" views using tabs
- "All" view shows all tasks including completed ones
- "Today" view shows only incomplete tasks with today's due date
- "Overdue" view shows only incomplete tasks with a past due date

**Technical Requirements**
- Add tab/button group to `TaskList.js` for filter selection
- Implement client-side filtering logic comparing `due_date` against current date
- Filter out completed tasks in "Today" and "Overdue" views

---

## Post-MVP

### Epic: Visual Overdue Highlighting

#### Story: Highlight overdue tasks with visual indicator

**Acceptance Criteria**
- Tasks past their due date are visually distinct (e.g., red border or background)
- Highlighting only applies to incomplete tasks

**Technical Requirements**
- Add conditional CSS class to task items in `TaskList.js` when `due_date < today` and `completed === false`
- Define overdue styling in `App.css`

---

### Epic: Advanced Sorting

#### Story: Sort tasks by overdue status, priority, and due date

**Acceptance Criteria**
- Overdue incomplete tasks appear first
- Within each group, tasks are sorted by priority (P1 first, then P2, then P3)
- Within the same priority, tasks are sorted by due date ascending
- Tasks without a due date appear last

**Technical Requirements**
- Implement multi-level sort comparator in the frontend or backend query
- Sort order: overdue → priority (P1→P3) → due date ASC → undated last
