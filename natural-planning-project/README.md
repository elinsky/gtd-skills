# Natural Planning Project Creation Skill

A conversational AI skill that guides users through the Natural Planning Model when creating GTD projects.

## What It Does

This skill ensures every project you create is well-formed with:

- Clear purpose and vision
- Appropriate planning depth (quick/standard/deep)
- At least one concrete next action
- Proper GTD structure and metadata

## How It Works

The skill guides you through a structured conversation:

1. **Assess Complexity** - Choose how much planning this project needs
2. **Gather Metadata** - Title, area, type, folder, due date
3. **Create Project File** - Uses MCP to generate the file with template
4. **Natural Planning** - Walks through NPM phases based on chosen depth
5. **Next Actions** - Ensures at least one action is created
6. **Summary** - Confirms what was created

## Planning Depths

### Quick Mode

**Use for:** Simple, straightforward projects
**Captures:** Outcome + 1 action
**Time:** ~30 seconds
**Example:** "Drop off dry cleaning"

### Standard Mode

**Use for:** Most projects needing some thought
**Captures:** Purpose + Vision + Actions
**Time:** ~2 minutes
**Example:** "Set up home office workspace"

### Deep Mode

**Use for:** Complex, important, or multi-faceted projects
**Captures:** Full 5-phase NPM (Purpose, Principles, Vision, Brainstorm, Organize, Actions)
**Time:** 5-10 minutes
**Example:** "Build a GTD agent product"

## Prerequisites

**Required:**

- [gtd-mcp](https://github.com/elinsky/gtd-mcp) server running
- GTD project structure in your brian/ repo:
  - `docs/execution_system/10k-projects/[area]/[folder]/`
  - `docs/execution_system/00k-next-actions/[context].md`

**Configuration:**

- Areas of focus configured in gtd-mcp config
- Context files created (@macbook.md, @waiting.md, etc.)

## Usage

### With Claude Code

Add to your `brian/CLAUDE.md`:

```markdown
# Project Creation
When I ask you to create a project, use the Natural Planning skill at:
/path/to/gtd-skills/skills/natural-planning-project/skill.md
```

Then simply say: "Create a project for me"

### Standalone

You can also invoke the skill by directly referencing it in your prompt:

```
Follow the Natural Planning Project Creation Skill at [path/to/skill.md].
I want to create a project about [your project idea].
```

## Example Conversation

**Quick Mode:**
```
User: Create a project for me
Claude: I'll help you create a GTD project. What's it about?
User: I need to renew my driver's license
Claude: How much planning does this need? Quick/Standard/Deep?
User: Quick
Claude: What area does this belong to? [shows areas]
User: Personal Growth Systems
Claude: Is this a standard project? And should it be active or incubator?
User: Standard, active
[Claude creates project file]
Claude: What does success look like?
User: I have a valid driver's license for 5 more years
[Claude fills in outcome]
Claude: What's your first next action?
User: Look up DMV appointment times online
Claude: Which context?
User: @macbook
[Claude creates action]
Claude: Any more actions?
User: No
[Claude shows summary]
```

**Deep Mode:**
```
User: Create a project - I want to build a GTD agent
Claude: That sounds complex. How much planning? Quick/Standard/Deep?
User: Deep - this is important
[Claude gathers metadata]
[Claude creates project file]
Claude: Why are you doing this project? What larger goal does it serve?
User: I want to help other people implement GTD effectively...
[Continues through all 5 NPM phases]
[Creates multiple next actions]
[Shows summary]
```

## Benefits

**Reduces Cognitive Load**
You don't have to remember NPM phases - the skill guides you through them.

**Ensures Completeness**
Every project gets at least one next action. No orphan projects.

**Adapts to Complexity**
Simple projects stay simple. Complex projects get the planning they deserve.

**Teaches GTD**
By using the skill, you internalize the Natural Planning Model over time.

**Consistent Structure**
All projects follow the same template and metadata standards.

## Customization

You can modify [skill.md](skill.md) to:

- Change the conversation style
- Add/remove NPM phases
- Adjust context list
- Modify project types or areas
- Change file paths for different repo structures

## Future Enhancements

- [ ] Support for project templates within NPM (e.g., "software project" template)
- [ ] Integration with weekly review skill
- [ ] Automatic project activation from incubator when first action is taken
- [ ] Multi-project planning for related initiatives
- [ ] Voice mode support for hands-free planning

## Related Skills

- (Future) Weekly Review Skill
- (Future) Project Completion Skill
- (Future) Someday/Maybe Review Skill

## License

MIT
