# Exercise 38: Advanced Todo List

## 🎯 Objectives

Create a feature-rich todo list application:

- Task struct with title, description, priority, status
- Sort by priority, due date, creation date
- Filter tasks by various criteria
- File persistence (JSON or custom format)
- Complete task lifecycle management

## 📚 Concepts

- Complex struct design with enums
- Sorting and filtering collections
- Date/time handling
- State management (task status)
- Priority systems
- Data persistence

## 📖 Background

**Task management systems** track work items through their lifecycle. A task typically has:

**Multiple states:**

```
Todo → In Progress → Done → Archived
```

**Priority levels** help with organization:

```
Low:     Can wait
Medium:  Normal importance
High:    Important, do soon
Urgent:  Drop everything, do now
```

**Attributes matter:**

- Title: What needs to be done
- Description: Details and context
- Due date: When it's needed
- Created date: When it was added
- Completed date: When it was finished
- Tags: Organization and grouping

**Real-world examples:**

```
Task: "Fix login bug"
Priority: Urgent
Status: In Progress
Due: 2024-01-20
Tags: ["bug", "security"]

Task: "Write documentation"
Priority: Medium
Status: Todo
Due: 2024-02-01
Tags: ["docs"]
```

## ⚙️ Requirements

**First Pass:**

- ✅ Task struct with title, description, priority, status
- ✅ Add, list, complete, delete tasks
- ✅ Sort by priority
- ✅ Save/load from file
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments on public items
- ✅ **Rich Task model**:
  - Unique ID
  - Title (required)
  - Description (optional)
  - Priority (Low, Medium, High, Urgent)
  - Status (Todo, InProgress, Done, Archived)
  - Created timestamp
  - Due date (optional)
  - Completion timestamp (when done)
  - Tags/categories
- ✅ **Sorting options**:
  - By priority
  - By due date
  - By creation date
  - By status
  - Custom ordering
- ✅ **Filtering**:
  - By status
  - By priority
  - By due date range
  - By tags
  - Show overdue tasks
  - Show completed tasks
  - Combine multiple filters
- ✅ **Task operations**:
  - Create new task
  - Update existing task
  - Mark as in progress
  - Mark as complete
  - Archive old tasks
  - Delete permanently
  - Reopen completed task
- ✅ **Display features**:
  - List view
  - Detailed view
  - Statistics summary
  - Progress indicators
- ✅ **Persistence**:
  - Save to file
  - Load from file
  - Handle corrupted data
  - Human-readable format

## 🚫 Constraints

- Use `serde` for JSON serialization (allowed)
- Use `chrono` for dates/times (allowed)
- Standard library for core logic
- Proper error handling

## 💡 Approaches

**Data modeling:**

- Enums for priority and status
- Struct for task with all attributes
- Separate struct for managing collection
- ID generation strategy

**Sorting strategies:**

- Sort by key (priority, date)
- Custom comparators
- Multi-field sorting
- Stable vs unstable sort

**Filtering approaches:**

- Iterator chains with filter
- Predicate functions
- Multiple filter combinations
- Building filter expressions

**Persistence options:**

- JSON for human-readable storage
- Binary format for efficiency
- Database (SQLite)
- Custom text format

**Date handling:**

- Store as timestamps
- Parse user input
- Calculate due/overdue
- Time zones consideration

## ✅ Validation

Expected outputs for various operations:

```
# Adding a task
$ todo add "Fix critical bug" --priority high --due "2024-01-20"
Task added: #1

# Listing tasks
$ todo list
Active Tasks (3):
[URGENT] Fix critical bug - Todo (Due: 2024-01-20)
[HIGH]   Write tests - In Progress
[LOW]    Update README - Todo

# Filtering by status
$ todo list --status todo
Tasks (2):
[URGENT] Fix critical bug
[LOW]    Update README

# Filtering overdue
$ todo list --overdue
Overdue Tasks (1):
[URGENT] Fix critical bug (Due: 2024-01-20) ⚠️

# Sorting by due date
$ todo list --sort due
[URGENT] Fix critical bug (Due: 2024-01-20)
[HIGH]   Submit report (Due: 2024-01-25)
[LOW]    Update README (No due date)

# Statistics
$ todo stats
Statistics:
  Total: 10 tasks
  Todo: 3
  In Progress: 2
  Done: 4
  Archived: 1
  Overdue: 1 ⚠️

# Completing a task
$ todo done 1
Task #1 marked as complete!
```

JSON file format example:

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "Fix critical bug",
      "description": "Memory leak in parser",
      "priority": "High",
      "status": "InProgress",
      "created_at": "2024-01-15T10:00:00Z",
      "due_date": "2024-01-20T17:00:00Z",
      "completed_at": null,
      "tags": ["bug", "urgent"]
    }
  ],
  "next_id": 2
}
```

## 🔍 Challenge

Add recurring tasks that automatically create new tasks on schedule (daily, weekly, monthly), implement task dependencies (task B can't start until task A is done), or add time tracking to measure how long you actually spend on each task.

---

**Previous:** [37_contacts](../37_contacts/README.md) | **Next:** [39_calculator_history](../39_calculator_history/README.md)
