# Horizons of Focus

GTD uses a six-level model for organizing commitments, from ground-level actions up to life purpose. This implementation uses these horizons to organize all captured items.

## The Six Levels

### 00k - Ground: Next Actions (Runway)

**What it is:** The immediate, concrete, physical actions you can take right now.

**File location:** `docs/execution_system/00k-next-actions/`

**Categories:**
- **Context lists** - Actions grouped by where/how you can do them
  - `contexts/@macbook.md` - Computer work
  - `contexts/@phone.md` - Phone calls
  - `contexts/@errands.md` - Things to do out and about
  - `contexts/@home.md` - Home-only actions
  - Other contexts as needed

- **State lists** - Actions in special states
  - `@waiting.md` - Waiting for others
  - `@deferred.md` - Scheduled for future date
  - `@incubating.md` - Not ready to act yet

- **Someday/Maybe** - Ideas for possible future actions
  - `someday/books-to-read.md`
  - `someday/movies-to-watch.md`
  - `someday/restaurants-to-try.md`
  - `someday/someday-general.md`

**Action format:** todo.txt style with tags
```
- [ ] 2025-11-01 Action description @context +project-name due:2025-12-01 defer:2025-11-15
```

### 10k - Projects (Current Outcomes)

**What it is:** Any outcome requiring more than one action to complete. "Finish quarterly taxes", "Plan anniversary trip", "Launch product feature".

**File location:** `docs/execution_system/10k-projects/`

**Folders:**
- `active/{area}/` - Projects you're actively working on
- `incubator/{area}/` - Projects you might do someday
- `completed/{area}/` - Completed projects (archive)

**Project types:**
- `standard` - Regular project with outcome and actions
- `habit` - Recurring practice or routine
- `coordination` - Multi-stakeholder project

**Key principle:** Every project needs at least one next action at 00k level.

### 20k - Areas of Focus (Responsibilities)

**What it is:** Ongoing roles and areas you're responsible for maintaining. Not outcomes, but ongoing standards. "Health", "Career", "Relationships", "Learning".

**File location:** `docs/execution_system/20k-areas/active/`

**Examples:**
- `areas-of-focus.md` - Master list of all areas
- `dunbar-chicago.md` - Tracking close relationships (Dunbar number)
- `mentees.md` - People you mentor
- `mentors.md` - People mentoring you

**Key principle:** Areas generate projects. If an area needs attention, create a 10k project.

### 30k - Goals (1-2 Year Objectives)

**What it is:** Medium-term objectives you want to accomplish. Specific, time-bound outcomes. "Get promoted to Director", "Run a half-marathon", "Build product MVP".

**File location:** `docs/execution_system/30k-goals/`

**Folders:**
- `active/` - Goals you're committed to
- `incubator/` - Goals you're considering
- `planning/` - Goals being defined

**Key principle:** Goals generate projects. Break goals down into 10k projects with concrete actions.

### 40k - Vision (3-5 Year Picture)

**What it is:** Your desired future state across key life domains. What do you want your life to look like in 3-5 years?

**File location:** `docs/execution_system/40k-vision/`

**Organized by area:**
- `active/health.md` - Health vision
- `active/career.md` - Career vision
- `active/mission.md` - Mission/purpose vision
- `active/learning.md` - Learning vision
- etc.

**Key principle:** Vision generates goals. Connect 30k goals to 40k vision for motivation and direction.

### 50k - Purpose & Principles (Life Direction)

**What it is:** Why you exist, your core values, your guiding principles. The "North Star" for all decisions.

**File location:** `docs/execution_system/50k-purpose-and-principles/active/`

**Files:**
- `purpose.md` or `purpose-v1.md`, `purpose-v2.md` - Your life purpose
- `principles.md` - Core principles you live by
- `role-models.md` - People who embody your values

**Key principle:** Purpose and principles guide vision. Everything else cascades from here.

## How to Use During Inbox Processing

When clarifying an inbox item, ask: "What level does this belong at?"

**Signs it's 00k (Action):**
- Single, concrete task
- No outcome beyond the action itself
- Examples: "Call dentist", "Buy milk", "Email Sarah"

**Signs it's 10k (Project):**
- Requires multiple steps
- Has a specific outcome/completion criteria
- Examples: "Plan team offsite", "Fix broken sink", "Research ML frameworks"

**Signs it's 20k (Area):**
- Ongoing responsibility, no end date
- Maintenance or stewardship
- Examples: Notes about maintaining relationships, health observations, role responsibilities

**Signs it's 30k (Goal):**
- Medium-term objective (1-2 years)
- Time-bound outcome
- Examples: "Lose 20 lbs by June", "Ship V1 by Q2", "Read 24 books this year"

**Signs it's 40k (Vision):**
- Long-term aspiration
- Paints a picture of desired future
- Examples: "Living in house with garden", "Leading a team of 10", "Fluent in Spanish"

**Signs it's 50k (Purpose/Principles):**
- Core values, life direction
- Timeless, foundational
- Examples: "Help others grow", "Create beauty", "Live with integrity"

## The Cascade

Higher horizons inform lower ones:

```
50k (Purpose) → Clarifies what matters
40k (Vision) → Envisions the future
30k (Goals) → Sets specific targets
20k (Areas) → Defines responsibilities
10k (Projects) → Creates concrete outcomes
00k (Actions) → Takes next steps
```

When processing inbox, most items will be 00k or 10k. Occasionally you'll capture ideas for higher levels. That's good! It means you're thinking holistically about your life.
