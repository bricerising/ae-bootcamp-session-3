# Product Requirements Document (PRD) - TODO App Enhancement

## 1. Overview

We are upgrading the basic TODO app to support due dates, priorities, and filters so users can better organize tasks. The current app only supports a title and completed status. These enhancements will make it more practical without overcomplicating the user experience.

---

## 2. MVP Scope

- Add `dueDate` field (ISO `YYYY-MM-DD`, optional) to tasks
- Add `priority` enum field: `P1 | P2 | P3` (default `P3`)
- Priority displayed as color-coded badges: Red for P1, Orange for P2, Gray for P3
- Add filter tabs: **All**, **Today**, **Overdue**
- In "Today" and "Overdue" views, only show incomplete tasks
- In "All" view, show all tasks including completed ones
- Keep storage **local** (in-memory, no external/backend storage changes beyond what exists)
- Data model validation:
  - `title`: required
  - `priority`: `"P1" | "P2" | "P3"`, default `"P3"`
  - `dueDate`: optional ISO `YYYY-MM-DD`; invalid values should be ignored (treated as absent)

---

## 3. Post-MVP Scope

- Overdue tasks visually highlighted (e.g., red background or border)
- Sorting logic: overdue first, then by priority (P1 → P3), then by due date ascending, then undated tasks last

---

## 4. Out of Scope

- Notifications
- Recurring tasks
- Multi-user support
- Keyboard navigation / special accessibility features
- External storage (staying local/in-memory only)
