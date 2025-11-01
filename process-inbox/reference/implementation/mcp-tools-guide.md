# MCP Tools Guide

This document lists all available MCP tools from the `gtd-mcp` server and when to use them during inbox processing.

## Tool Categories

### Action Management (00k)

#### `add_action`
**Purpose:** Add a next action to a context list

**Parameters:**
- `text` (required) - Action description
- `context` (required) - Context: @macbook, @phone, @errands, @home, etc.
- `project` (optional) - Project name in kebab-case
- `due` (optional) - Due date (YYYY-MM-DD)
- `defer` (optional) - Defer until date (YYYY-MM-DD)
- `action_date` (optional) - Date action was created (defaults to today)

**Example:**
```
add_action(
  text="Complete DBT homework worksheet 8",
  context="@macbook",
  project="dbt-skills-group",
  due="2025-11-07"
)
```

**When to use:** When inbox item is a single, concrete action that takes >2 minutes

---

#### `add_to_waiting`
**Purpose:** Add item to @waiting list (delegated or waiting for others)

**Parameters:**
- `text` (required) - What you're waiting for
- `project` (optional) - Related project
- `due` (optional) - Expected completion date
- `defer` (optional) - When to check back
- `action_date` (optional) - Date added

**Example:**
```
add_to_waiting(
  text="Response from Eric at Millennium about HRT update",
  project="update-eric-on-hrt-outcome"
)
```

**When to use:** After delegating or when waiting for someone's response/action

---

#### `add_to_deferred`
**Purpose:** Add action to @deferred list (scheduled for specific future date)

**Parameters:**
- `text` (required) - Action description
- `project` (optional) - Related project
- `defer` (optional) - Date to activate this action
- `action_date` (optional) - Date added

**Example:**
```
add_to_deferred(
  text="Review Q4 financial statements",
  defer="2025-12-20"
)
```

**When to use:** When action can't/shouldn't be done until specific future date

---

#### `add_to_incubating`
**Purpose:** Add action to @incubating list (not ready to act yet, but might be)

**Parameters:**
- `text` (required) - Action description
- `project` (optional) - Related project
- `action_date` (optional) - Date added

**Example:**
```
add_to_incubating(
  text="Research ML frameworks for agent architecture"
)
```

**When to use:** When you might want to do this, but not committed yet

---

#### `complete_action`
**Purpose:** Mark an action as complete and archive it

**Parameters:**
- `file_path` (required) - Path to action file
- `line_number` (required) - Line number of the action
- `completion_date` (optional) - Date completed (defaults to today)

**Example:**
```
complete_action(
  file_path="docs/execution_system/00k-next-actions/contexts/@macbook.md",
  line_number=15
)
```

**When to use:** Only when completing existing actions (not typically used during inbox processing)

---

#### `list_actions`
**Purpose:** List existing actions with filtering

**Parameters:**
- `group_by` (optional) - How to group: "project", "context", "flat" (default: "project")
- `include_states` (optional) - Which states: ["next", "waiting", "deferred", "incubating"]
- `filter_project` (optional) - Filter to specific project
- `filter_context` (optional) - Filter to specific context

**Example:**
```
list_actions(
  group_by="context",
  filter_context="@macbook"
)
```

**When to use:** To check if similar action exists, or to show user their current actions

---

### 📂 Project Management (10k)

#### `create_project`
**Purpose:** Create a new GTD project with proper structure

**Parameters:**
- `title` (required) - Project title
- `area` (required) - Area of focus (must match configured areas)
- `type` (required) - "standard", "habit", or "coordination"
- `folder` (required) - "active" or "incubator"
- `due` (optional) - Due date (YYYY-MM-DD)

**Example:**
```
create_project(
  title="Automate GTD System with LLM Agent",
  area="Mission",
  type="standard",
  folder="active"
)
```

**When to use:** When inbox item requires multiple actions to complete (it's a project!)

---

#### `list_projects`
**Purpose:** List projects with flexible filtering

**Parameters:**
- `folder` (optional) - "active", "incubator", "completed", "all" (default: "active")
- `group_by` (optional) - "area", "due_date", "flat" (default: "area")
- `filter_area` (optional) - Filter to specific area
- `filter_has_due` (optional) - true (has due date) or false (no due date)

**Example:**
```
list_projects(
  folder="active",
  filter_area="Career"
)
```

**When to use:** To check if similar project exists, or to show user context

---

#### `list_active_projects`
**Purpose:** Quick list of all active projects grouped by area

**Parameters:** None

**Example:**
```
list_active_projects()
```

**When to use:** To show user overview of current commitments, useful when deciding if inbox item fits existing project

---

#### `search_projects`
**Purpose:** Search project titles and content

**Parameters:**
- `query` (required) - Search text
- `folder` (optional) - Which folders to search (default: "all")
- `filter_area` (optional) - Limit to specific area

**Example:**
```
search_projects(
  query="DBT",
  folder="active"
)
```

**When to use:** To find existing project that inbox item might relate to

---

#### `complete_project`
**Purpose:** Move project to completed folder

**When to use:** Not typically used during inbox processing

---

#### `activate_project`
**Purpose:** Move project from incubator to active

**When to use:** When inbox item triggers decision to activate incubating project

---

### Information Tools

#### `list_areas`
**Purpose:** List all configured areas of focus

**Parameters:** None

**Example:**
```
list_areas()
```

**Returns JSON:**
```json
{
  "areas": [
    {"name": "Health", "kebab": "health"},
    {"name": "Learning", "kebab": "learning"},
    {"name": "Career", "kebab": "career"},
    ...
  ]
}
```

**When to use:** When user needs to pick an area for project or to understand available areas

---

#### `list_goals`
**Purpose:** List all goals (projects with type="goal")

**Parameters:** None

**Example:**
```
list_goals()
```

**When to use:** To check if inbox item relates to existing goal

---

#### `search_actions`
**Purpose:** Search action content across all action files

**Parameters:**
- `query` (required) - Search text
- `include_states` (optional) - Which states to search
- `filter_project` (optional) - Limit to specific project
- `filter_context` (optional) - Limit to specific context

**Example:**
```
search_actions(
  query="DBT"
)
```

**When to use:** To find similar/duplicate actions before creating new one

---

### Audit Tools

These are primarily for system maintenance, not inbox processing:
- `audit_projects` - Find data quality issues
- `audit_orphan_projects` - Find projects without actions
- `audit_orphan_actions` - Find actions with invalid projects/contexts
- `update_review_dates` - Bulk update review dates

## Decision Tree: Which Tool to Use?

```
Inbox item clarified
    |
    ├─ Is it actionable?
    │   ├─ YES: Is it a single action or multiple actions?
    │   │   ├─ Single action (00k)
    │   │   │   ├─ Takes <2 min? → Do it now (no tool)
    │   │   │   ├─ I'm not the right person? → add_to_waiting()
    │   │   │   ├─ Can't do until later? → add_to_deferred()
    │   │   │   ├─ Maybe someday? → add_to_incubating()
    │   │   │   └─ Next action? → add_action()
    │   │   │
    │   │   └─ Multiple actions (10k)
    │   │       ├─ Does project exist?
    │   │       │   ├─ YES → Use Edit tool to append note
    │   │       │   └─ NO → create_project()
    │   │       └─ Then add at least one action with add_action()
    │   │
    │   └─ NO: What is it?
    │       ├─ Trash → Delete line from inbox
    │       ├─ Reference → File it (outside GTD)
    │       ├─ Someday/Maybe → Use Edit tool on someday lists
    │       ├─ Higher horizon (20k-50k) → Use Edit/Read tools on appropriate files
    │       └─ Incubate → add_to_incubating() or someday list
```

## Tool Usage Patterns

### Pattern 1: Simple Action
```
1. Clarify inbox item
2. add_action(text="...", context="@macbook", project="...")
3. Delete line from inbox
```

### Pattern 2: New Project with Action
```
1. Clarify inbox item (it's a project!)
2. create_project(title="...", area="...", type="standard", folder="active")
3. Use Edit tool to add purpose/vision if needed
4. add_action(text="...", context="@macbook", project="...")
5. Delete line from inbox
```

### Pattern 3: Add to Existing Project
```
1. Clarify inbox item
2. search_projects(query="...") to find related project
3. Read project file
4. Edit project file to append note/idea
5. If action needed: add_action(...)
6. Delete line from inbox
```

### Pattern 4: Higher Horizon Capture
```
1. Clarify inbox item (it's a vision/goal/principle)
2. Read appropriate file (e.g., 40k-vision/active/mission.md)
3. Edit file to append idea
4. Delete line from inbox
```

## Common Mistakes

**Don't:**
- Use `add_action` for items that take <2 minutes (do them immediately instead)
- Create a project without also creating at least one next action
- Forget to delete processed items from inbox
- Use tools for file operations when Read/Edit/Write tools are simpler

**Do:**
- Check for existing projects/actions before creating new ones
- Use proper kebab-case for project names in tags
- Validate areas against `list_areas()` before creating projects
- Ask user for clarification if item could be either action or project
