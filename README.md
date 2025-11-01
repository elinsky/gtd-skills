# Execution System Skills

Reusable AI agent skills for execution system workflows. These skills guide Claude Code and AI agents through workflow best practices.

## Why This Exists

Getting Things Done works, but it's hard to implement consistently. You know you should process your inbox regularly, create well-formed projects, and maintain your system - but actually doing it requires discipline and expertise.

These skills embed productivity coaching expertise into Claude Code, so you get guided through best practices as a natural conversation:

- **Processing inbox?** Claude coaches you through clarify and organize for each item
- **Creating a project?** Claude asks about purpose and vision before letting you add tasks
- **Stuck on something?** Claude helps you apply workflow principles to get unstuck

No more decision paralysis. No more shallow projects. No more items sitting in inbox for weeks. Just effective execution with an AI partner who knows the methodology.

## Overview

Skills are conversational prompts that instruct AI assistants on how to guide users through complex workflows. They can be used standalone in Claude Code or orchestrated by autonomous agents.

## Available Skills

### Natural Planning Project Creation
**Location:** `skills/natural-planning-project/`

Guides users through the Natural Planning Model when creating new projects. Ensures projects are well-formed with clear purpose, vision, and next actions.

**Key Features:**

- Adaptive depth control (Quick/Standard/Deep planning)
- Integrates with execution-system-mcp tools for project creation
- Ensures every project has at least one next action
- Follows workflow best practices

See [skills/natural-planning-project/README.md](skills/natural-planning-project/README.md) for details.

### Process Inbox
**Location:** `skills/process-inbox/`

Guides users through inbox processing - clarifying and organizing captured items one at a time until inbox is empty. Acts as your productivity coach, helping you route items across all horizons of focus (00k actions through 50k purpose).

**Key Features:**

- Enforces processing rules (top first, one at a time, never back to inbox)
- Multi-horizon routing (00k-50k)
- Adaptive questioning based on item complexity
- Integrates with execution-system-mcp tools for organizing
- Comprehensive reference materials included

See [skills/process-inbox/README.md](skills/process-inbox/README.md) for details.

## Usage

These skills are designed to work with:

- **Claude Code** - Interactive CLI coding assistant
- **execution-system-mcp** - MCP server providing project management tools
- **Future Execution Agent** - Autonomous agent for execution system management

### Integration with Claude Code

Reference the skill in your project's `CLAUDE.md` or Claude Code settings. When you ask Claude to create a project, it will automatically use the Natural Planning Model.

## Architecture Vision

This repository is part of a larger execution system automation:

```
execution-system-mcp/      # Low-level MCP tools (create projects, list actions, etc.)
execution-system-skills/   # Reusable conversational workflows (this repo)
execution-system-agent/    # Future: Autonomous agent orchestrating skills + tools
```

Skills are the middle layer - they encode productivity expertise as reusable prompts that can be invoked by humans or agents.

## Contributing

This is currently a personal project being developed in public. As it matures, contribution guidelines will be added.
