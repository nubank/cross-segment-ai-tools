# Cross-Segment AI Tools

AI-powered coding assistants for Nu's cross-segment development workflows. This repository contains Cursor rules and commands that automate repetitive tasks, enforce best practices, and accelerate development across Core, PJ, and other data domains.

## 🚀 Quick Start

### Installation

Install commands or rules to your project using the `nu` CLI:

```bash
# Install commands to a project
nu cross-segment-ai-tools commands install <repo>
nu cross-segment-ai-tools commands install itaipu
nu cross-segment-ai-tools commands install ~/dev/nu/my-project

# Install rules to a project
nu cross-segment-ai-tools rules install <repo>
nu cross-segment-ai-tools rules install itaipu
nu cross-segment-ai-tools rules install ~/dev/nu/my-project
```

### Update

Keep your tools up to date:

```bash
# Update all projects that have commands installed
nu cross-segment-ai-tools commands update

# Update a specific project
nu cross-segment-ai-tools commands update ~/dev/nu/itaipu

# Update all projects that have rules installed
nu cross-segment-ai-tools rules update

# Update a specific project
nu cross-segment-ai-tools rules update ~/dev/nu/itaipu
```

### Remove

Remove tools from a project:

```bash
# Remove commands from a project
nu cross-segment-ai-tools commands remove <repo>
nu cross-segment-ai-tools commands remove itaipu

# Remove rules from a project
nu cross-segment-ai-tools rules remove <repo>
nu cross-segment-ai-tools rules remove itaipu
```

### Help

```bash
nu cross-segment-ai-tools commands --help
nu cross-segment-ai-tools rules --help
```

---

## 📁 Repository Structure

```
.cursor/
└── commands/                    # AI commands (executable prompts & agents)
    ├── core/                    # Core-specific commands
    │   ├── pe-de-pano-v2.md    # Purple Loop campaign automation
    │   └── clm_doc_creator.md   # CLM business rules documentation automation
    ├── pj/                      # PJ-specific commands
    └── cross-segments/          # Cross-segment commands
        └── rapidash.md          # Audience Manager attribute generator

docs/
└── agents/
    └── clm_doc_creator.md       # CLM Doc Creator Agent documentation
```

---

## 🤖 Available AI Assistants

### 🔥 Rapidash — Audience Manager Attribute Generator

**Domain:** Cross-segment (Core, PJ, High-Income)

Rapidash automates the entire process of creating audience manager attributes—from requirements gathering to production-ready code. In ~10 minutes, it can:

- ✅ Generate complete Scala attribute code
- ✅ Detect duplicates with comprehensive validation
- ✅ Suggest attribute generators for parameter variations
- ✅ Handle git workflows automatically
- ✅ Deliver a ready-to-review pull request

**How to use:**
1. Open your Itaipu project in Cursor
2. Use the command: `/rapidash`
3. Follow the conversational prompts

**Supported domains:** `core-brazil`, `high-income`, `pj-brazil`, and more

**Documentation:** Included in agent file

---

### 🦶 Pé de Pano — Purple Loop Campaign Automation

**Domain:** Core (PF segment)

Pé de Pano automates three Purple Loop-related tasks:

1. **Campaign Updater** — Add campaign vals to product config files
2. **Templates Updater** — Insert templates into product template lists
3. **Ranking Strategy Updater** — Include campaigns in ranking strategy lists

**How to use:**
1. Open your Itaipu project in Cursor
2. Use the command: `/pe-de-pano-v2`
3. Provide campaign/template data as tables
4. Review dry-run plan before applying changes

**Supported products:** Money Boxes, Caixinha Turbo, Insurance, Lending, and 30+ more

**Documentation:** Included in command file

---

### 📝 CLM Doc Creator Agent — Business Rules Documentation Automation

**Domain:** Core (PF segment)

CLM Doc Creator Agent automates the creation and maintenance of technical documentation for Customer Lifecycle Management (CLM) business rules in Confluence. It analyzes Scala code files for product eligibility, activity, and conversion logic, then creates human-readable documentation that non-technical stakeholders (PMs, business analysts) can understand.

**Key Features:**
- 🔍 **Analyzes Scala code** to extract business rules from activity, eligibility, and conversion datasets
- 📊 **Queries metadata** from Data Discovery to enrich documentation
- 📝 **Generates structured documentation** in clear, accessible language
- 📤 **Publishes to Confluence** automatically with proper hierarchy and navigation
- 🔄 **Detects changes** and provides intelligent diff comparisons before updating
- 📈 **Maintains version history** with semantic versioning

**How to use:**
1. Open your Itaipu project in Cursor
2. Use the command: `/clm-doc-creator`
3. Specify a product (e.g., "document nucel") or let it detect from context
4. Review the generated documentation before publishing

**Requirements:**
- Atlassian MCP Server (for Confluence integration)
- Data Discovery MCP Server (for dataset metadata)

**Documentation:** [docs/agents/clm_doc_creator_agent.md](docs/agents/clm_doc_creator_agent.md)

---

## 🎯 Commands vs Rules

| Feature | Commands | Rules |
|---------|----------|-------|
| **Purpose** | Executable prompts for specific tasks | Context & guidelines for AI behavior |
| **Usage** | Invoke with `/command-name` | Applied automatically or by glob pattern |
| **Scope** | Task-specific (e.g., create attribute) | Domain-wide (e.g., Scala best practices) |
| **Output** | Code, PRs, changes | AI behavior modification |

---

## 📖 Adding New Agents or Commands

### Adding a New Command

1. Create a new `.md` file in the appropriate folder:
   - `.cursor/commands/core/` — Core-specific
   - `.cursor/commands/pj/` — PJ-specific
   - `.cursor/commands/cross-segments/` — Cross-segment

2. Include clear step-by-step instructions for the AI

3. Test with a real project before committing

### Adding a New Rule/Agent

1. Create a new `.md` or `.mdc` file in the appropriate folder:
   - `.cursor/commands/core/` — Core-specific agents
   - `.cursor/commands/pj/` — PJ-specific agents
   - `.cursor/commands/cross-segments/` — Cross-segment agents

2. For `.mdc` files, use frontmatter:

```markdown
---
description: "Brief description of the agent"
globs: ["**/*.scala", "**/pj/**"]
alwaysApply: false
---

# Agent Name

Your agent rules and guidelines...
```

3. Test the rule with real projects

---

## 🛠️ Development

### Prerequisites

- [Cursor IDE](https://cursor.sh/) with AI features enabled
- Access to Nu's internal repositories
- `nu` CLI installed

### Testing Changes

1. Make your changes to commands/rules
2. Install to a test project:
   ```bash
   nu cross-segment-ai-tools commands install ~/dev/nu/test-project
   ```
3. Test the AI assistant behavior
4. Update if needed

---

## 🤝 Contributing

1. **Keep it focused** — Each command/rule should have a clear, single purpose
2. **Document thoroughly** — Include examples and expected behavior
3. **Test before submitting** — Verify with real projects
4. **Follow conventions** — Match existing naming and structure

---

## 📚 Related Resources

- [Itaipu Repository](https://github.com/nubank/itaipu) — Main data domains repository
- [Nu CLI Documentation](https://github.com/nubank/nucli) — CLI tooling

---

## 📜 License

This project is part of Nu's internal development ecosystem.
