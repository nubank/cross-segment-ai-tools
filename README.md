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

The CLI is integrated into **nucli**. Once you have nucli set up, you can use the `cross-segment-ai-tools` command directly:

```bash
# Install agents to your project
cross-segment-ai-tools rules install ~/dev/my-project

# Update agents in a project
cross-segment-ai-tools rules update ~/dev/my-project

# Remove agents from a project
cross-segment-ai-tools rules remove ~/dev/my-project
```

**Note**: The command will automatically clone the `cross-segment-ai-tools` repository if it doesn't exist locally.

### 🐦 PJ Agents

#### Cockpidgey AI Agent
- **Location**: `.cursor/rules/pj/agents/cockpidgey-ai-agent.mdc`
- **Purpose**: Helps developers create simple metrics in Cockpit in a guided and interactive way
- **Features**:
  - Guides developers in creating simple metrics (User-level Base Metrics)
  - Collects information iteratively and in a friendly manner
  - Creates one metric at a time: `-users`, `-volume`, or `-value`
  - Ensures Event Logs and necessary records are created
  - Follows established patterns in the Experimentation domain
- **Invocation**: Use `@cockpidgey-ai-agent` to start the guided workflow

### 💎 High Income Agents

High Income-specific AI agents will be available here.

**Location**: `.cursor/rules/high-income/agents/`

### 🎯 Agent Categories

Agents are organized by:
- **Domain** (PJ, Core, High Income)
- **Purpose** (metrics creation, code generation, etc.)
- **Scope** (general-purpose vs domain-specific)

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

