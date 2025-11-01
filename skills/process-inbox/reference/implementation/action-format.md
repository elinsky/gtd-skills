# Action Format

Actions in this system use a todo.txt-inspired format with specific conventions.

## Basic Format

```
- [ ] YYYY-MM-DD Action description @context +project-name due:YYYY-MM-DD defer:YYYY-MM-DD
```

## Components

### Checkbox
- `- [ ]` - Incomplete action
- `- [x]` - Completed action (with completion date)

### Date
- Format: `YYYY-MM-DD`
- Position: Immediately after checkbox
- Represents: Date action was created
- Example: `2025-11-01`

### Action Description
- Clear, concrete, physical activity
- Starts with verb when possible
- Specific enough to know exactly what to do
- Good: "Call Dr. Smith to schedule annual checkup"
- Bad: "Health stuff", "Think about doctor"

### Context Tag
- Format: `@context`
- Indicates where/how action can be done
- Common contexts:
  - `@macbook` - Computer work
  - `@phone` - Phone calls
  - `@errands` - Out and about
  - `@home` - Home-only actions
  - `@anywhere` - Can do anywhere
- Must match existing context file names

### Project Tag
- Format: `+project-name`
- Links action to parent project
- Must be in kebab-case
- Should match project filename (without .md extension)
- Example: `+dbt-skills-group` links to `dbt-skills-group.md`
- Optional: Actions don't have to belong to a project

### Due Date (Optional)
- Format: `due:YYYY-MM-DD`
- Hard deadline for action
- Use sparingly - most actions don't have true due dates
- Example: `due:2025-12-15`

### Defer Date (Optional)
- Format: `defer:YYYY-MM-DD`
- Date when action becomes relevant
- "Don't show me this until..."
- Example: `defer:2025-11-20`

## Complete Examples

### Simple action with context
```
- [ ] 2025-11-01 Buy milk @errands
```

### Action with project
```
- [ ] 2025-11-01 Complete DBT homework worksheet 8 @macbook +dbt-skills-group
```

### Action with due date
```
- [ ] 2025-11-01 File quarterly taxes @macbook +tax-preparation due:2025-12-31
```

### Action with project and due date
```
- [ ] 2025-11-01 Send proposal to client @macbook +acme-consulting due:2025-11-15
```

### Action with defer date
```
- [ ] 2025-11-01 Review Q4 budget @macbook +financial-planning defer:2025-12-20
```

### Completed action
```
- [x] 2025-11-01 Set up Lumi on iPad and iPhone @macbook +digital-setup completed:2025-10-31
```

## Sorting and Organization

Actions within a file are typically sorted by creation date (newest first), but this is not strictly enforced. The MCP `add_action` tool will add new actions at an appropriate location.

## Special Files

### Context Files
Location: `00k-next-actions/contexts/@{context}.md`

Contains actions for a specific context. Each file has YAML frontmatter:

```yaml
---
title: Macbook
last_reviewed: 2025-11-01
---

- [ ] 2025-11-01 Action one @macbook +project-a
- [ ] 2025-10-30 Action two @macbook +project-b due:2025-12-01
```

### Waiting For (@waiting.md)
Location: `00k-next-actions/@waiting.md`

Actions waiting for others. No `@waiting` context tag needed (it's implied by the file).

```
- [ ] 2025-11-01 Response from Eric about proposal +client-project
- [ ] 2025-10-28 Feedback from Sarah on draft +marketing-plan
```

### Deferred (@deferred.md)
Location: `00k-next-actions/@deferred.md`

Actions scheduled for future dates. Use `defer:` tag.

```
- [ ] 2025-11-01 Review annual performance @macbook defer:2025-12-15
- [ ] 2025-10-25 Plan Q1 goals @macbook defer:2026-01-01
```

### Incubating (@incubating.md)
Location: `00k-next-actions/@incubating.md`

Actions you might do, but not committed yet.

```
- [ ] 2025-11-01 Research ML frameworks for project
- [ ] 2025-10-20 Explore meditation apps
```

## Action States

Based on which file an action lives in:

- **Next** - In a context file (e.g., `@macbook.md`) - ready to do now
- **Waiting** - In `@waiting.md` - waiting for someone else
- **Deferred** - In `@deferred.md` - scheduled for future
- **Incubating** - In `@incubating.md` - maybe someday

## Best Practices

### Be Specific
- Bad: "Plan trip"
- Good: "Search Google Flights for Chicago to NYC flights Dec 15-20 @macbook +holiday-trip"

### Start with Verbs
- Call, Email, Draft, Research, Buy, Schedule, Review, Update, etc.
- Makes actions feel concrete and doable

### Include Context Info
If you'll need to remember specifics, include them:
- "Call Dr. Smith (555-1234) to schedule checkup @phone"
- "Buy 2% milk and eggs @grocery"

### One Action Per Line
Don't combine multiple actions:
- Bad: "Call Sarah and email report"
- Good: Two separate lines

### Keep Context Pure
An action should only have ONE context tag. If it could be done in multiple contexts, pick the most specific or most likely:
- Can do on phone or computer? Pick one based on which you'd prefer

### Projects Are Required
Every action needs a project tag. Quick one-off tasks are not fine without the project tag:
- `- [ ] 2025-11-01 Buy birthday card @errands +send-birthday-card`

### Use Due Dates Sparingly
True deadlines are rare. Most "due dates" are really preferences. Reserve `due:` for real consequences:
- Has due date: "File taxes", "Submit proposal before deadline"
- No due date: "Call dentist", "Read article", "Research options"
