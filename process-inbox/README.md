# Process Inbox Skill

Guides users through the GTD inbox processing workflow - clarifying and organizing captured items one at a time until inbox is empty.

## Purpose

Traditional inbox processing is overwhelming. You stare at a list of random items and don't know where to start. The GTD Processing Guide tells you to "start at the top and process one at a time," but that's easier said than done when items are vague, complex, or touch multiple areas of your life.

This skill embeds GTD coaching expertise into Claude Code. It guides you through a structured conversation for each inbox item:

- **Clarifying**: What is this? Is it actionable? What's the next physical action?
- **Routing**: Which horizon does it belong to? (00k actions → 50k purpose)
- **Organizing**: Using MCP tools to put it in the right place in your system
- **Removing**: Deleting it from inbox (never going back)

No more decision paralysis. No more items sitting in inbox for weeks. Just clear, decisive processing with an AI partner who knows GTD.

## How It Works

**You:** "Process inbox"

**Claude:**
1. Reads your inbox file
2. Presents first item from the top
3. Asks clarifying questions naturally
4. Helps you decide: action? project? higher horizon?
5. Uses MCP tools to organize it properly
6. Deletes it from inbox
7. Repeats for next item

**Result:** Inbox at zero, everything in the right place, habits reinforced.

## Key Features

### Follows GTD Rules Strictly

- **Top item first** - No cherry-picking
- **One at a time** - Full focus on current item
- **Never back to inbox** - One-way path out
- **Every project gets action** - No orphaned projects
- **Two-minute rule** - Do quick things now

### Multi-Horizon Intelligence

Routes items across all 6 horizons:
- **00k** - Next actions (@macbook, @phone, @waiting, etc.)
- **10k** - Projects (creates new, appends to existing)
- **20k** - Areas of focus
- **30k** - Goals (1-2 years)
- **40k** - Vision (3-5 years)
- **50k** - Purpose & principles

### Adaptive Coaching

Matches your processing style:
- **Fast processors**: Moves quickly, minimal questions
- **Thinkers**: Asks probing questions, helps clarify
- **Dumpers**: Extracts structure from brain dumps

### Context-Aware

- Searches for existing projects before creating duplicates
- Validates areas against your configuration
- Suggests related items ("This might also need a goal...")
- Uses proper formatting (todo.txt, kebab-case, etc.)

## Usage

### Basic

```
You: Process inbox
Claude: [guides you through each item]
```

### Resume Session

```
You: Process inbox
Claude: Welcome back. You have 5 items remaining. Let's continue...
```

### Get Help

```
You: I'm stuck on this inbox item
Claude: [helps clarify what it is and where it should go]
```

## Requirements

**MCP Server:**
- `gtd-mcp` server must be running and configured
- Requires tools: `add_action`, `create_project`, `list_areas`, `search_projects`, etc.

**File Structure:**
- Inbox at: `docs/execution_system/00-inbox.md`
- Follows standard GTD horizons structure (see `reference/implementation/file-structure.md`)

**Configuration:**
- Areas of focus defined in `~/.config/gtd-mcp/config.json`
- Must match areas in `docs/execution_system/20k-areas/active/areas-of-focus.md`

## Reference Materials

The skill includes comprehensive documentation:

**GTD Principles** (`reference/gtd-principles/`):
- Original GTD concepts
- Processing guidelines, two-minute rule, etc.
- 17 files covering clarify and organize phases

**Implementation Guide** (`reference/implementation/`):
- `horizons-of-focus.md` - The 6-level model explained
- `file-structure.md` - Where everything lives
- `mcp-tools-guide.md` - All available tools
- `action-format.md` - Todo.txt formatting

**Workflows** (`workflows/`):
- `multi-horizon-routing.md` - Decision tree for routing items

## Example Session

```
User: Process inbox

Claude: You have 8 items in your inbox. Let's process them one by one, from top to bottom.

Let's look at the first item: "Call chiropractor"

User: Yeah, need to schedule an appointment

Claude: Got it. Is this a single action or part of a bigger project?

User: Just a single action

Claude: Great. Where would you do this - phone or computer?

User: Phone

Claude: Does it relate to any existing project?

User: Not really

Claude: Perfect. I'll add this to your @phone list.
[adds action]
Item processed. 7 items remaining.

Let's look at the next item: "Create skill to help process inbox"
...
```

## Best Practices

1. **Schedule inbox processing** - Daily or every 2-3 days
2. **Block time** - 15-30 minutes for small batches
3. **Trust the process** - Don't skip items, follow GTD rules
4. **Start with small batches** - Process 5-10 items at a time
5. **Use capture freely** - Get stuff into inbox quickly, process later

## Common Scenarios

### Vague Item
**Inbox:** "Health stuff"
**Skill:** Asks clarifying questions until concrete action emerges

### Complex Item
**Inbox:** [paragraph about product vision]
**Skill:** Identifies it touches multiple horizons, processes each level

### Duplicate
**Inbox:** "Research ML frameworks"
**Skill:** Searches, finds existing project, appends instead of duplicating

### Multi-Step Item
**Inbox:** "Plan anniversary trip"
**Skill:** Recognizes as project, creates it, ensures at least one action added

## Troubleshooting

**Skill not activating?**
- Ensure SKILL.md is in Claude Code's skills path
- Reference skill explicitly: "Use process-inbox skill"

**MCP tools failing?**
- Check gtd-mcp server is running
- Verify config at `~/.config/gtd-mcp/config.json`

**Items going to wrong place?**
- Review `workflows/multi-horizon-routing.md`
- Skill can make mistakes - you can always move items later

## Philosophy

This skill embodies a key GTD insight:

> "When I coach people through this process, it invariably becomes a dance back and forth between the simple decision-making stage of processing the open loops and the trickier task of figuring out the best way to enter these decisions in their particular organization systems."

The skill IS that coach. It dances between clarifying (What is it?) and organizing (Where does it go?) naturally, making inbox processing feel less like a chore and more like a productive conversation with a knowledgeable partner.

## Related Skills

- **natural-planning-project** - For creating well-formed projects during inbox processing
- **weekly-review** (future) - For reviewing system health

## Contributing

This skill is part of the gtd-skills repository. Issues and improvements welcome.
