# AI Agents

This directory contains individual AI agent definitions for PJ and Core development workflows.

## 📁 Directory Structure

- `.cursor/rules/agents/` - General-purpose AI agents
- `.cursor/rules/pj/agents/` - PJ-specific AI agents
- `.cursor/rules/core/agents/` - Core-specific AI agents

## 📝 Adding a New Agent

1. **Choose the appropriate directory** based on the agent's scope:
   - Use `agents/` for general-purpose agents
   - Use `pj/agents/` for PJ-specific agents
   - Use `core/agents/` for Core-specific agents

2. **Create a new `.mdc` file** with a descriptive name (e.g., `payment_processing_agent.mdc`)

3. **Follow the standard format**:

```markdown
---
description: "Brief description of what this agent does"
globs: ["**/*.clj", "**/payment/**"]  # File patterns this agent applies to
alwaysApply: false  # Set to true if agent should always be active
---

# Agent Name

## Purpose
Describe the agent's purpose and use cases.

## Guidelines
- Rule 1
- Rule 2
- Rule 3

## Examples
Provide examples of how the agent should behave.
```

## 🎯 Best Practices

- **Be specific**: Each agent should have a clear, focused purpose
- **Use descriptive names**: File names should clearly indicate the agent's function
- **Document thoroughly**: Include examples and use cases
- **Test before committing**: Verify the agent works as expected in real projects

## 📚 Example Agents

See the finance-dev-tools repository for examples of well-structured agent files.

