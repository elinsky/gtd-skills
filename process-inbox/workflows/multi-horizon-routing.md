# Multi-Horizon Routing

A decision workflow for determining which horizon an inbox item belongs to.

## Quick Reference

| If the item is... | It belongs at... | Action to take |
|-------------------|------------------|----------------|
| A single concrete task | 00k (Next Action) | `add_action()` or other 00k tools |
| Multiple steps to outcome | 10k (Project) | `create_project()` + `add_action()` |
| Ongoing responsibility | 20k (Area) | Edit area file |
| 1-2 year objective | 30k (Goal) | Edit/create goal file |
| 3-5 year aspiration | 40k (Vision) | Edit vision file |
| Core value/principle | 50k (Purpose) | Edit purpose/principles file |

## Detailed Decision Tree

### Start: What is this inbox item?

```
Is it actionable?
├─ YES → Continue to "Actionable Items"
└─ NO → Continue to "Non-Actionable Items"
```

## Actionable Items

### Step 1: Single action or multiple actions?

**Question:** Can this be completed in one action, or does it require multiple steps?

**Test:** If you do the obvious next action, is the commitment fully satisfied?

#### If SINGLE ACTION (00k level):

**Question:** How long will it take?

- **Less than 2 minutes?** → Do it now (no tools needed, then delete from inbox)
- **More than 2 minutes?** → Continue below

**Question:** Who should do it?

- **Someone else?** → Delegate it
  - Use `add_to_waiting()` to track
  - Delete from inbox

- **You, but not now?** → When can you do it?
  - **Not until specific date?** → `add_to_deferred(defer="YYYY-MM-DD")`
  - **Maybe someday?** → `add_to_incubating()` or someday list (Edit tool)
  - **As soon as possible?** → Continue below

**Question:** What context do you need?

- Determine context: @macbook, @phone, @errands, @home, etc.
- Use `add_action(text="...", context="@...")`
- **Optional:** Add project tag if it relates to existing project
- Delete from inbox

#### If MULTIPLE ACTIONS (10k level):

This is a PROJECT.

**Question:** Does a project already exist for this?

- **YES** → Add note to existing project
  - Use `search_projects(query="...")` to find it
  - Read project file
  - Edit project file to append idea/note
  - If there's a new action: `add_action()`
  - Delete from inbox

- **NO** → Create new project
  - Determine area (use `list_areas()` if needed)
  - Determine type: standard, habit, or coordination
  - Determine folder: active or incubator
  - Use `create_project(title="...", area="...", type="...", folder="...")`
  - Optionally edit to add purpose/vision
  - **Critical:** Create at least one next action with `add_action()`
  - Delete from inbox

## Non-Actionable Items

### Step 2: What kind of thing is it?

#### Trash
**Recognition:** No value, outdated, irrelevant

**Action:** Delete line from inbox

---

#### Reference
**Recognition:** Information you might need later, but no action required

**Action:** File it in your reference system (outside GTD structure), then delete from inbox

---

#### Someday/Maybe
**Recognition:** Might want to do this eventually, but not committed

**Types:**
- Book to read → `someday/books-to-read.md`
- Movie to watch → `someday/movies-to-watch.md`
- Restaurant to try → `someday/restaurants-to-try.md`
- General idea → `someday/someday-general.md` or `add_to_incubating()`

**Action:** Edit appropriate someday file, delete from inbox

---

#### Higher Horizon Capture

**Question:** What level of thinking is this?

##### 20k - Area of Focus
**Recognition:**
- Thoughts about ongoing responsibilities
- Notes about maintaining areas of life
- Observations about roles

**Examples:**
- "Need to stay more in touch with Chicago friends"
- "Health area needs more attention"
- "Career development feeling stagnant"

**Action:**
- Read `20k-areas/active/areas-of-focus.md` to see areas
- Edit relevant area file or create new one
- Delete from inbox

---

##### 30k - Goals
**Recognition:**
- Specific outcome you want in 1-2 years
- Time-bound objective
- Measurable achievement

**Examples:**
- "Lose 20 lbs by June"
- "Get promoted to Director by Q3"
- "Complete CS degree by December"

**Action:**
- Use `list_goals()` to check existing goals
- Either:
  - Edit existing goal file to add idea
  - Create new goal file in `30k-goals/incubator/`
- Delete from inbox

**Note:** Goals often spawn projects. Consider if this should be BOTH a goal AND a project.

---

##### 40k - Vision
**Recognition:**
- Long-term aspiration (3-5 years)
- Paints picture of desired future
- What you want life to look like

**Examples:**
- "Want to be leading a team of 10 people"
- "Living in house with garden and workshop"
- "Fluent in Spanish, traveling regularly"
- "Financially independent with passive income"

**Action:**
- Determine which area this vision relates to (Health, Career, Mission, etc.)
- Read `40k-vision/active/{area}.md`
- Edit to add vision idea
- Delete from inbox

---

##### 50k - Purpose & Principles
**Recognition:**
- Core values
- Life direction
- Guiding principles
- Why you exist

**Examples:**
- "Help others grow and develop"
- "Create beauty in the world"
- "Live with integrity and honesty"
- "Principle: Always choose learning over comfort"

**Action:**
- If it's about purpose: Edit `50k-purpose-and-principles/active/purpose.md`
- If it's a principle: Edit `50k-purpose-and-principles/active/principles.md`
- Delete from inbox

## Complex Cases

### Case 1: Item touches multiple horizons

**Example:** "I want to get healthier - lose weight, exercise more, feel better"

**Analysis:**
- 40k vision component: "Feel healthy and energetic"
- 30k goal component: "Lose 15 lbs by March"
- 10k project component: "Establish exercise routine"
- 00k action component: "Research gym memberships"

**Resolution:**
1. Start with HIGHEST horizon first (vision)
2. Work down to action level
3. May result in updates at multiple levels

**Process:**
1. Edit `40k-vision/active/health.md` with vision
2. Create goal file in `30k-goals/incubator/` or `active/`
3. `create_project(title="Establish exercise routine", area="Health", ...)`
4. `add_action(text="Research gym memberships", context="@macbook", ...)`
5. Delete from inbox

### Case 2: Unclear if action or project

**Example:** "Plan trip to Chicago"

**Question to ask:** What does "done" look like?

- If done = flights booked → Single action
- If done = full itinerary, hotel, activities planned → Project

**When in doubt:**
- Ask user: "Does this require multiple steps?"
- Err toward creating a project (can always simplify later)

### Case 3: Already have similar project/action

**Prevention:** Always search first
- `search_projects(query="...")`
- `search_actions(query="...")`

**If found:**
- Don't duplicate
- Add to existing project/action as note
- Or realize it's already captured and just delete

## Routing Summary

```
Inbox Item
    │
    ├─ Actionable?
    │   ├─ YES → Single or Multiple?
    │   │   ├─ Single → 00k (Action)
    │   │   │   ├─ <2min? → Do now
    │   │   │   ├─ Delegate? → add_to_waiting()
    │   │   │   ├─ Later? → add_to_deferred() or add_to_incubating()
    │   │   │   └─ ASAP → add_action()
    │   │   │
    │   │   └─ Multiple → 10k (Project)
    │   │       ├─ Exists? → Edit existing
    │   │       └─ New? → create_project() + add_action()
    │   │
    │   └─ NO → What is it?
    │       ├─ Trash → Delete
    │       ├─ Reference → File it
    │       ├─ Someday → Edit someday list
    │       └─ Higher horizon:
    │           ├─ Ongoing responsibility → 20k (Area)
    │           ├─ 1-2 year objective → 30k (Goal)
    │           ├─ 3-5 year aspiration → 40k (Vision)
    │           └─ Core value → 50k (Purpose/Principle)
    │
    └─ Delete from inbox when done
```

## Key Principles

1. **Process top to bottom** - No cherry-picking
2. **One item at a time** - Stay focused
3. **Never back to inbox** - One-way path out
4. **Decide quickly** - Trust your gut, can always refine later
5. **Always search first** - Avoid duplicates
6. **Projects need actions** - Never orphan a project
7. **Delete when done** - Inbox should go to zero
