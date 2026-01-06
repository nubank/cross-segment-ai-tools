# Cross Segment AI Tools

This repository contains **AI Agents** - specialized assistants that help developers with cross-segment development tasks (PJ, Core, High Income, and other segments). The CLI features have been moved to the nucli project.

## 📁 Structure

```
.cursor/
└── rules/                       # AI agent definitions
    ├── agents/                  # General-purpose AI agents
    ├── pj/                      # PJ-specific AI agents
    │   └── agents/              # PJ domain agents
    ├── core/                    # Core-specific AI agents
    │   └── agents/              # Core domain agents
    └── high-income/             # High Income-specific AI agents
        └── agents/              # High Income domain agents
```

## 🤖 Available AI Agents

This repository currently focuses on **AI Agents** - specialized assistants that help developers with cross-segment development tasks (PJ, Core, High Income, and other segments). These agents are defined as `.mdc` files and can be installed via the `cross-segment-ai-tools` CLI.

### Quick Install

> **Note**: The CLI is currently under development and will be integrated into **nucli**. Once available, you'll be able to use the `cross-segment-ai-tools` command to install agents to your projects.

```bash
# Future CLI usage (coming soon):
# cross-segment-ai-tools rules install ~/dev/my-project
# cross-segment-ai-tools rules update ~/dev/my-project
# cross-segment-ai-tools rules remove ~/dev/my-project
```

### 🐦 PJ Agents

PJ-specific AI agents are available in `.cursor/rules/pj/agents/`

### 💎 High Income Agents

High Income-specific AI agents are available in `.cursor/rules/high-income/agents/`

### 🏦 Core Agents

Core-specific AI agents are available in `.cursor/rules/core/agents/`

## 📖 Adding New AI Agents

AI agents are defined as individual `.mdc` files in the `.cursor/rules/agents/` or domain-specific agent directories. Each agent file should:

1. **Follow the `.mdc` format** with frontmatter metadata
2. **Include clear description** of the agent's purpose
3. **Define scope** using `globs` patterns
4. **Specify if always applied** using `alwaysApply: true/false`

### Example Agent Structure

```markdown
---
description: "Agent description and purpose"
globs: ["**/*.clj", "**/pj/**"]
alwaysApply: false
---

# Agent Name

Agent-specific rules and guidelines...
```

### Recommended Location for New Agents

Place new AI agent files in:
- `.cursor/rules/agents/` - For general-purpose agents
- `.cursor/rules/pj/agents/` - For PJ-specific agents
- `.cursor/rules/core/agents/` - For Core-specific agents
- `.cursor/rules/high-income/agents/` - For High Income-specific agents

## 🔧 Development

### Adding New Agents

1. Create new `.mdc` files in the appropriate agent directory:
   - `.cursor/rules/agents/` - For general-purpose agents
   - `.cursor/rules/pj/agents/` - For PJ-specific agents
   - `.cursor/rules/core/agents/` - For Core-specific agents
   - `.cursor/rules/high-income/agents/` - For High Income-specific agents
2. Follow the existing naming conventions and structure
3. Include comprehensive documentation and examples
4. Test with the cross-segment-ai-tools CLI (from nucli)

### Agent Format

Agents use `.mdc` (Markdown with Cursor extensions) format optimized for AI coding assistants:

- Clear, actionable instructions
- Comprehensive examples and templates
- Business context and reasoning
- Step-by-step workflows
- User interaction patterns

## 🤝 Contributing

1. Agents should be **specific and actionable**
2. Include **business context** and reasoning
3. Provide **clear examples** and use cases
4. Follow **existing naming conventions**
5. Test agents with real projects before submitting

## 📜 License

This project is part of the Nu cross-segment development ecosystem. See repository license for details.

---

**Note**: The CLI features for managing these agents have been moved to the nucli project for centralized tooling management. This repository focuses exclusively on AI agents for cross-segment development workflows.

