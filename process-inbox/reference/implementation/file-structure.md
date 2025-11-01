# File Structure

This document maps the conceptual horizons of focus to the actual file system structure.

## Root Directory

```
$EXECUTION_SYSTEM_REPO/docs/execution_system/
```

All files live under this root. The `$EXECUTION_SYSTEM_REPO` variable should point to your personal execution system repository (e.g., `/Users/you/Dropbox/repos/brian/`).

## Full Structure

```
docs/execution_system/
├── 00-inbox.md                              # Capture inbox (process this!)
├── 00k-next-actions/
│   ├── contexts/
│   │   ├── @macbook.md                      # Computer actions
│   │   ├── @phone.md                        # Phone calls
│   │   ├── @errands.md                      # Out and about
│   │   ├── @home.md                         # Home-only actions
│   │   ├── @anywhere.md                     # Can do anywhere
│   │   ├── @grocery.md                      # Grocery shopping
│   │   ├── @articles.md                     # Articles to read
│   │   └── @books.md                        # Books to read
│   ├── agendas/
│   │   ├── @agenda-PersonName.md            # One per person
│   │   └── @agenda-MeetingName.md           # One per recurring meeting
│   ├── @waiting.md                          # Waiting for others
│   ├── @deferred.md                         # Scheduled for future
│   ├── @incubating.md                       # Not ready yet
│   ├── someday/
│   │   ├── someday-general.md              # General someday/maybe
│   │   ├── books-to-read.md                # Books
│   │   ├── movies-to-watch.md              # Movies
│   │   ├── tv-shows-to-watch.md            # TV shows
│   │   ├── restaurants-to-try.md           # Restaurants
│   │   └── reading-list.md                 # Articles/papers
│   └── completed.md                         # Completed actions archive
│
├── 10k-projects/
│   ├── active/                              # Projects being worked on
│   │   ├── {area}/                          # One folder per area
│   │   │   └── project-name.md             # Project files
│   ├── incubator/                           # Maybe someday projects
│   │   └── {area}/
│   │       └── project-name.md
│   └── completed/                           # Completed projects archive
│       └── {area}/
│           └── project-name.md
│
├── 20k-areas/
│   ├── active/
│   │   ├── areas-of-focus.md               # Master list
│   │   └── [other area-specific files]     # Notes on maintaining areas
│   └── incubator/
│       └── [area notes being developed]
│
├── 30k-goals/
│   ├── active/
│   │   └── goal-name.md                    # Active goals
│   └── incubator/
│       └── goal-name.md                    # Goals being considered
│
├── 40k-vision/
│   ├── active/
│   │   ├── health.md                       # Vision by area
│   │   ├── learning.md
│   │   ├── career.md
│   │   ├── mission.md
│   │   ├── personal-growth-systems.md
│   │   ├── character.md
│   │   ├── emotional-health.md
│   │   ├── finance.md
│   │   └── hobbies-and-recreation.md
│   └── incubator/
│       └── [vision notes being developed]
│
└── 50k-purpose-and-principles/
    ├── active/
    │   ├── purpose.md                      # Life purpose
    │   └── principles.md                   # Core principles
    └── incubator/
        └── [purpose/principles explorations]
```

## File Naming Conventions

### Projects (10k)
- Lowercase, kebab-case: `project-name.md`
- Example: `complete-cs-61c-course.md`, `automate-gtd-system-with-llm-agent.md`

### Context Files (00k)
- Prefix with `@`: `@context.md`
- Lowercase: `@macbook.md`, `@phone.md`

### Agenda Files (00k)
- Prefix with `@agenda-`: `@agenda-PersonName.md`
- CamelCase for person names: `@agenda-TinaSmith.md`

### Someday Lists (00k)
- Descriptive kebab-case: `books-to-read.md`, `restaurants-to-try.md`

### Higher Horizon Files (20k-50k)
- Kebab-case, descriptive: `areas-of-focus.md`, `purpose-v2.md`

## YAML Frontmatter

Most files include YAML frontmatter for metadata.

### Project Files
```yaml
---
area: Career
title: Complete CS 61C Course
type: standard
last_reviewed: 2025-11-01
started: 2025-10-15
due: 2025-12-31
---
```

### Action List Files
```yaml
---
title: Macbook
last_reviewed: 2025-11-01
---
```

### Goal Files
```yaml
---
area: Health
title: Bulk to 187lbs
type: goal
last_reviewed: 2025-11-01
---
```

## Where to Put New Items During Inbox Processing

| Item Type | Location | Method |
|-----------|----------|--------|
| Next action | `00k-next-actions/contexts/@{context}.md` | MCP: `add_action` |
| Waiting for | `00k-next-actions/@waiting.md` | MCP: `add_to_waiting` |
| Deferred action | `00k-next-actions/@deferred.md` | MCP: `add_to_deferred` |
| Incubating action | `00k-next-actions/@incubating.md` | MCP: `add_to_incubating` |
| Someday/Maybe | `00k-next-actions/someday/{list}.md` | Edit tool |
| New project | `10k-projects/active/{area}/` or `incubator/{area}/` | MCP: `create_project` |
| Project note | Append to existing project file | Read + Edit tools |
| Area note | `20k-areas/active/{area-file}.md` | Edit tool |
| Goal idea | `30k-goals/incubator/{goal-name}.md` | Write tool (new) or Edit (existing) |
| Vision idea | `40k-vision/active/{area}.md` | Edit tool |
| Purpose/Principle | `50k-purpose-and-principles/active/purpose.md` or `principles.md` | Edit tool |
| Reference | File system or notes app (outside execution system structure) | Manual filing |
| Trash | Delete from inbox | Delete line |

## Key Relationships

**Projects → Actions:**
- Every project in `10k-projects/active/` should have at least one next action in `00k-next-actions/`
- Actions reference projects with `+project-name` tag

**Areas → Projects:**
- Projects are organized by area
- Areas are listed in `20k-areas/active/areas-of-focus.md`

**Goals → Projects:**
- Goals often spawn multiple projects
- Projects can reference parent goal in frontmatter or body

## Special Files

**Inbox:** `00-inbox.md`
- Unprocessed capture items
- Line-by-line format
- Process top-to-bottom
- Delete lines as you process them

**Completed:** `00k-next-actions/completed.md`
- Archive of completed actions
- Automatically populated by `complete_action` MCP tool
- Good for weekly review

## Configuration

The MCP server requires a config file at:
```
~/.config/execution-system-mcp/config.json
```

This defines:
- `gtd_repo_path` - Absolute path to your execution system repo
- `areas` - List of valid area names (must match `20k-areas/active/areas-of-focus.md`)
