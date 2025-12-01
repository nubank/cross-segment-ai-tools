# PJ Core Dev Tools - AI Coding Rules

This repository contains AI coding rules and patterns for PJ and Core development workflows. The CLI features have been moved to the nucli project.

## 📁 Structure

```
.cursor/
└── rules/                       # AI coding rules and patterns
    ├── clojure/                 # Clojure language rules
    │   ├── datomic/            # Datomic database rules
    │   ├── diplomat_architecture/  # Diplomat Architecture patterns
    │   └── testing/            # Testing guidelines
    ├── scala/                   # Scala language rules
    ├── pj/                      # PJ-specific rules and patterns
    ├── core/                    # Core-specific rules and patterns
    └── agents/                  # AI agent definitions (MD files)
```

## 🚀 Using the Rules

The rules in this repository are managed by the `pj-core-dev-tools` CLI, which is now part of the **nucli** project.

### Quick Install

```bash
# The CLI is now in nucli - install from there
cd ~/dev/nu/nucli/nucli.d/pj-core-dev-tools.d
./scripts/install

# Then use it to install rules to your projects
pj-core-dev-tools rules install ~/dev/my-project
```

### Available Rules

#### 🔧 Clojure Rules

- **Core Language**: Idiomatic Clojure development patterns, data structures, and functional programming
- **Diplomat Architecture**: Complete architectural patterns for layered service design
- **Datomic**: Database interaction patterns and best practices
- **Error Handling**: Robust error handling and validation patterns
- **Testing**: Comprehensive testing strategies and patterns
- **State Management**: Concurrent state management patterns
- **Performance**: Java interop and performance optimization

#### 📊 Scala Rules

- **Dataset Patterns**: Function-oriented dataset generation following data engineering best practices
- **Unit Testing**: Comprehensive unit testing patterns

#### 🏢 PJ & Core Specific Rules

- **PJ Rules**: Business logic patterns specific to PJ (Pessoa Jurídica) domain
- **Core Rules**: Core banking patterns and best practices
- **AI Agents**: Individual AI agent definitions for specific use cases

### 🎯 Rule Categories

All rules are organized by:
- **Language** (clojure, scala)
- **Domain** (PJ, Core, architect patterns, testing)
- **Specificity** (core language features vs specialized frameworks)

## 📖 Adding AI Agents

AI agents are defined as individual `.mdc` files in the `.cursor/rules/agents/` directory. Each agent file should:

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

## 🔧 Development

### Adding New Rules

1. Create new `.mdc` files in the appropriate category folder
2. Follow the existing naming conventions and structure
3. Include comprehensive documentation and examples
4. Test with the pj-core-dev-tools CLI (from nucli)

### Rule Format

Rules use `.mdc` (Markdown with Cursor extensions) format optimized for AI coding assistants:

- Clear, actionable patterns
- Comprehensive examples
- Business context and reasoning
- Anti-patterns to avoid
- Testing strategies

## 🤝 Contributing

1. Rules should be **specific and actionable**
2. Include **business context** and reasoning
3. Provide **positive and negative examples**
4. Follow **existing naming conventions**
5. Test rules with real projects before submitting

## 📜 License

This project is part of the Nu PJ and Core development ecosystem. See repository license for details.

---

**Note**: The CLI features for managing these rules have been moved to the nucli project for centralized tooling management. This repository now focuses exclusively on the AI coding rules and patterns.

