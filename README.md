# GTD Skills

Reusable AI agent skills for Getting Things Done (GTD) workflows. These skills guide Claude Code and AI agents through GTD best practices, particularly the Natural Planning Model.

## Why This Exists

Traditional project planning tools present you with empty form fields: "Project Name", "Description", "Due Date". But effective planning requires thinking through *why* you're doing something before deciding *what* to do. This backwards approach leads to shallow projects that lack clarity.

David Allen's Natural Planning Model solves this - it's how your brain naturally plans when it works well. You think through purpose first, then envision success, then brainstorm, then organize, then identify next actions. In that order.

These skills embed that expertise into Claude Code, so you get guided through high-quality planning as a conversation:

- **Creating a project?** Claude asks about purpose and vision before letting you add tasks
- **Stuck on a project?** Claude helps you reconnect with why it matters
- **Moving too fast?** Claude ensures you've thought it through

No more blank forms. No more shallow projects. Just natural planning with an AI partner who knows GTD.

## Overview

Skills are conversational prompts that instruct AI assistants on how to guide users through complex workflows. They can be used standalone in Claude Code or orchestrated by autonomous agents.

## Available Skills

### Natural Planning Project Creation
**Location:** `skills/natural-planning-project/`

Guides users through David Allen's Natural Planning Model when creating new GTD projects. Ensures projects are well-formed with clear purpose, vision, and next actions.

**Key Features:**

- Adaptive depth control (Quick/Standard/Deep planning)
- Integrates with gtd-mcp tools for project creation
- Ensures every project has at least one next action
- Follows GTD best practices from "Getting Things Done"

See [skills/natural-planning-project/README.md](skills/natural-planning-project/README.md) for details.

## Usage

These skills are designed to work with:

- **Claude Code** - Interactive CLI coding assistant
- **gtd-mcp** - MCP server providing GTD project management tools
- **Future GTD Agent** - Autonomous agent for execution system management

### Integration with Claude Code

Reference the skill in your project's `CLAUDE.md` or Claude Code settings. When you ask Claude to create a project, it will automatically use the Natural Planning Model.

## Architecture Vision

This repository is part of a larger GTD automation system:

```
gtd-mcp/           # Low-level MCP tools (create projects, list actions, etc.)
gtd-skills/        # Reusable conversational workflows (this repo)
gtd-agent/         # Future: Autonomous agent orchestrating skills + tools
```

Skills are the middle layer - they encode GTD expertise as reusable prompts that can be invoked by humans or agents.

## Contributing

This is currently a personal project being developed in public. As it matures, contribution guidelines will be added.
