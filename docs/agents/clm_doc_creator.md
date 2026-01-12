# CLM Doc Creator Agent [Confluence Link](https://nubank.atlassian.net/wiki/spaces/FCB/pages/264529543175/CLM+Doc+Creator+Agent)

## Table of Contents
- [Overview](#overview)
- [Agent Availability](#agent-availability)
- [Requirements](#requirements)
- [Installation](#installation)
- [How to Use](#how-to-use)
- [What It Does](#what-it-does)
- [Important Information](#important-information)
- [Troubleshooting](#troubleshooting)

---

## Overview

The **CLM Doc Creator Agent** is an intelligent Cursor AI agent designed to automatically generate and maintain technical documentation for Customer Lifecycle Management (CLM) business rules in Confluence. It analyzes Scala code files for product eligibility, activity, and conversion logic, then creates human-readable documentation that non-technical stakeholders (PMs, business analysts) can understand.

### Key Capabilities
- 🔍 **Analyzes Scala code** to extract business rules from activity, eligibility, and conversion datasets
- 📊 **Queries metadata** from Data Discovery to enrich documentation
- 📝 **Generates structured documentation** in clear, accessible language
- 📤 **Publishes to Confluence** automatically with proper hierarchy and navigation
- 🔄 **Detects changes** and provides intelligent diff comparisons before updating
- 📈 **Maintains version history** with semantic versioning

### Context
- **Project**: Itaipu (Spark Runtime Project)
- **Target Codebase**: `subprojects/data-domains/core-brazil-cross-segment/src/main/scala/nu/data_domain/core_brazil_cross_segment/br/customer_product_profile/datasets`
- **Confluence Space**: FCB (Foundational Core Brazil)
- **Parent Page**: [CLM Data Products Rules](https://nubank.atlassian.net/wiki/spaces/FCB/pages/264501298309/CLM+Data+Products+Rules) (Page ID: `264501298309`)

---

## Agent Availability

The **CLM Doc Creator Agent** is part of the **Cross-Segment AI Tools** repository, which provides AI-powered coding assistants for Nu's cross-segment development workflows. This repository contains Cursor rules and agents that automate repetitive tasks, enforce best practices, and accelerate development across Core, PJ, and other data domains.

### Repository Location

The agent is stored in the Cross-Segment AI Tools repository structure:

```
.cursor/
└── rules/
    └── core/
        └── agents/
            └── clm_doc_creator_agent.mdc
```

### Domains Supported
- **Core** (PF segment) - Primary domain
- **PJ** (PJ segment)
- **High-Income**
- Other cross-segment domains

---

## Requirements

### 1. Cursor IDE
- Latest version of [Cursor](https://cursor.sh/)
- Cursor must be configured with MCP (Model Context Protocol) support
- Access to Nu's internal repositories

### 2. Nu CLI
The `nu` CLI tool is required to install and manage Cross-Segment AI Tools.

- Ensure `nu` CLI is installed and configured
- Verify installation:
  ```bash
  nu --version
  ```

### 3. Git Repository Access
- Clone the **Itaipu** repository:
  ```bash
  git clone <itaipu-repo-url>
  cd itaipu
  ```
- Ensure you're in the correct project directory when using the agent

### 4. Atlassian MCP Server
The Atlassian MCP server enables interaction with Confluence and Jira.

- **Documentation**: [Setting Up Cursor for Confluence Integration](https://nubank.atlassian.net/wiki/spaces/DOC/pages/264239124130/Setting+Up+Cursor+for+Confluence+Integration)
- **Capabilities**:
  - Create/update Confluence pages
  - Search Confluence content
  - Manage page hierarchy
  - Lookup user account IDs

### 5. Data Discovery MCP Server
The Data Discovery MCP server provides access to dataset metadata.

- **Documentation**: [How to Use Cursor Data Discovery MCP](https://nubank.atlassian.net/wiki/spaces/Playbooks/pages/264342546910/How+to+Use+Cursor+Data+Discovery+MCP)
- **Capabilities**:
  - Search dataset metadata
  - Query table information
  - Get owner and steward details
  - Validate dataset existence

---

## Installation

### Quick Start

The CLM Doc Creator Agent can be installed to your Itaipu project using the `nu` CLI tool:

```bash
# Install rules (includes the CLM Doc Creator Agent) to Itaipu
nu cross-segment-ai-tools rules install itaipu

# Or install to a specific project path
nu cross-segment-ai-tools rules install ~/dev/nu/itaipu
```

### What Gets Installed

When you run the installation command:
- The agent (`clm_doc_creator_agent.mdc`) is added to your project's `.cursor/rules/` directory
- The agent becomes automatically available in Cursor when you open the Itaipu project
- No manual configuration is needed - the agent is ready to use

### Updating the Agent

Keep the agent up to date with the latest improvements:

```bash
# Update all projects that have rules installed
nu cross-segment-ai-tools rules update

# Update a specific project
nu cross-segment-ai-tools rules update ~/dev/nu/itaipu
```

### Removing the Agent

If you need to remove the agent from your project:

```bash
# Remove rules from Itaipu
nu cross-segment-ai-tools rules remove itaipu

# Or remove from a specific project path
nu cross-segment-ai-tools rules remove ~/dev/nu/itaipu
```

### Getting Help

For more information about the installation commands:

```bash
nu cross-segment-ai-tools rules --help
```

---

## MCP Server Setup

After installing the agent, you need to configure the required MCP servers.

### Step 1: Install MCP Servers

Follow the installation instructions from the documentation links above for:
1. **Atlassian MCP** - Confluence/Jira integration
2. **Data Discovery MCP** - Dataset metadata queries

### Step 2: Configure Cursor

Add the MCP servers to your Cursor configuration (typically in `~/.cursor/config.json` or through Cursor settings):

```json
{
  "mcpServers": {
    "atlassian": {
      "command": "<path-to-atlassian-mcp>",
      "args": [],
      "env": {
        "ATLASSIAN_CLOUD_ID": "c43390d3-e5f8-43ca-9eec-c382a5220bd9"
      }
    },
    "data-discovery-mcp": {
      "command": "<path-to-data-discovery-mcp>",
      "args": []
    }
  }
}
```

### Step 3: Verify Installation and Connection

After installing the agent and configuring MCP servers:

1. Open the Itaipu project in Cursor
2. Test that the agent is available and MCP servers are connected:

```
@clm-doc-creator test connection
```

The agent should confirm it can access:
- ✅ Agent loaded successfully
- ✅ Confluence (via Atlassian MCP)
- ✅ Data Discovery (via Data Discovery MCP)
- ✅ Itaipu repository

---

## How to Use

### Invocation Methods

#### 1. Direct Invocation
Simply mention the agent:
```
clm-doc-creator
@clm-doc-creator
```

#### 2. Document a Specific Product
```
clm-doc-creator, create documentation for collateral-lines
Document product nucel
clm-doc-creator, update roxinho documentation
```

#### 3. Document Specific Files
```
clm-doc-creator, document:
- ProductActivityNucelFact.scala
- ProductEligibilityNucelFact.scala
```

#### 4. Automatic Detection
The agent activates automatically when you mention keywords like:
- `documentation` + (`rules`, `business`, `activity`, `eligibility`, `conversion`)
- `doc` + (`clm`, `product`)
- `document` + (`product`, `rules`)

### Basic Workflow

1. **Invoke the agent** using any method above
2. **Agent confirms activation** and identifies files
3. **Agent analyzes code** and extracts business rules
4. **Agent queries metadata** (you'll see searches happening)
5. **For updates**: Agent compares with existing documentation and shows diff
6. **Confirm changes** (if updating existing documentation)
7. **Agent generates** structured documentation
8. **Agent publishes** to Confluence
9. **Review the result** using the provided Confluence link

### Example Session

```
You: clm-doc-creator, create documentation for nucel

Agent: 🔍 Searching for nucel files...
       ✓ ProductEligibilityNucelFact.scala
       ✓ ProductActivityNucelFact.scala
       ✓ ProductConversionNucel.scala
       
       📖 Analyzing Scala code...
       ✓ Eligibility rules extracted
       ✓ Activity rules extracted
       ✓ Conversion rules extracted
       
       🗄️ Querying metadata...
       ✓ Dataset metadata retrieved
       
       ✅ Validating output datasets...
       ✓ All datasets validated
       
       📝 Generating documentation...
       ✓ Documentation complete
       
       📤 Publishing to Confluence...
       ✓ Product Group updated
       ✓ Product page created
       
       ✅ Documentation created successfully!
       📄 Page: NuCel - CLM Rules
       🔗 Link: https://nubank.atlassian.net/wiki/spaces/FCB/pages/...
```

---

## What It Does

### Agent Process Flow

The agent follows a **7-phase process**:

#### Phase 1: File Identification
- Searches for activity, eligibility, and conversion files
- Identifies the product and product group
- Supports search by product name, file list, or git diff

#### Phase 2: Scala Code Analysis
- Extracts input datasets (AutoInput, InternalInput)
- Identifies filters and business conditions
- Detects Product Interaction usage (for conversions)
- Extracts output column definitions

#### Phase 3: Metadata Extraction
- Queries Data Discovery for each dataset
- Retrieves owner squad, data accountable, and data stewards
- Looks up Confluence user information
- Formats contact information

#### Phase 4: Output Validation
- Infers output dataset paths from traits
- Validates datasets exist via Data Discovery
- Generates FreeWilly links
- Identifies SCD (Slowly Changing Dimension) tables

#### Phase 5: Rule Translation
- Converts Scala code to natural language
- Creates clear, non-technical descriptions
- Filters out implementation details
- Provides practical examples

#### Phase 6: Documentation Generation
- Assembles structured Markdown
- Includes all sections: eligibility, activity, conversion
- Adds data sources with FreeWilly links
- Creates SQL query examples
- Initializes version history

#### Phase 7: Confluence Publishing
- Ensures product group page exists
- Updates product group with new documentation
- Creates or updates product page
- **For updates**: Detects changes, shows diff, asks confirmation
- Maintains proper page hierarchy and navigation

### Documentation Structure

The agent creates a **3-level hierarchy** in Confluence:

```
Level 0: CLM Data Products Rules (parent page - already exists)
├── Level 1: {ProductGroup} - Product Group (created/updated by agent)
│   ├── Level 2: {Product1} - CLM Rules (created/updated by agent)
│   └── Level 2: {Product2} - CLM Rules (created/updated by agent)
```

Each product page includes:
- 📋 **Product Information** (name, group, owner, data accountable, stewards)
- 🎯 **Overview** (product description)
- 📊 **Data Sources** (input datasets with FreeWilly links)
- ✅ **Eligibility Rules** (who is eligible for the product)
- 🔄 **Activity Rules** (who is actively using the product)
- 🚀 **Conversion Rules** (when customers convert to the product)
- 🚀 **Product Journey Moment** (if applicable)
- 💡 **SQL Query Examples** (how to query the data)
- 📚 **Version History** (all changes tracked)

---

## Important Information

### Change Detection (for Updates)

When updating existing documentation, the agent:

1. **Downloads current documentation** from Confluence
2. **Parses existing rules** into structured format
3. **Analyzes current code** to extract new rules
4. **Compares old vs. new** using similarity matching
5. **Classifies changes**:
   - 🟢 **Low Impact**: Typo fixes, description updates
   - 🟡 **Medium Impact**: Time window changes, new conditions
   - 🔴 **High Impact**: Rule removal, logic changes
6. **Shows diff** with impact analysis
7. **Asks for confirmation** before updating
8. **Skips update** if no changes detected

### Version Management

The agent uses **semantic versioning**:
- **Patch** (1.0.0 → 1.0.1): Minor changes
- **Minor** (1.0.0 → 1.1.0): Moderate changes
- **Major** (1.0.0 → 2.0.0): Critical changes

Version history is automatically maintained in a table at the end of each product page.

### Special Cases

#### 1. Standard Eligibility Dataset
If a product doesn't have a specific eligibility file, the agent documents that it uses the **standard eligibility dataset** (`dataset/nu-core-br-canonical-fact-segment-customer-start-date`) where all customers are eligible by default.

#### 2. Product Interaction in Conversion
When conversion uses a Product Interaction:
- Agent reads the Product Interaction file
- Lists Product Interaction's input datasets as conversion data sources
- Explains the relationship clearly
- Documents how Product Interaction feeds into conversion

#### 3. Temporal Windows
- Agent **ignores** technical data-loading windows (typically 4-5 days)
- Only documents **business rule time windows** (e.g., "active in last 30 days")

#### 4. SCD Tables
- Agent only creates SCD sections if the SCD dataset **exists**
- Validates via Data Discovery before including

### Output Links

The agent generates **FreeWilly links** for all datasets:
- Format: `` `{dataset_name}` | [FreeWilly]({link})``
- Example: `` `nu-br/dataset/table-name` | [FreeWilly](https://backoffice.nubank.com.br/free-willy/summary/?datasetName=nu-br/dataset/table-name)``
- Dataset names are displayed as inline code (not hyperlinked)
- Only "FreeWilly" text is hyperlinked

---

## Troubleshooting

### Agent Not Responding

**Issue**: Agent doesn't activate when invoked

**Solutions**:
1. Verify the agent is installed:
   ```bash
   # Check if commands are installed in your project
   ls .cursor/commands/core/
   ```
2. Ensure you're in the Itaipu project directory where the agent is installed
3. Try explicit invocation: `@clm-doc-creator`
4. Restart Cursor to reload the agent
5. Verify MCP servers are connected (see Step 3 in MCP Server Setup)

### MCP Connection Errors

**Issue**: "Cannot connect to MCP server" or similar errors

**Solutions**:
1. Verify MCP servers are installed correctly
2. Check Cursor MCP configuration (`~/.cursor/config.json`)
3. Restart Cursor after configuration changes
4. Test MCP servers independently (refer to MCP documentation)

### Dataset Not Found

**Issue**: Agent reports "⚠️ Output table path not found"

**Solutions**:
1. The agent will **ask you** for the correct dataset path
2. Provide the full dataset path (e.g., `nu-br/dataset/table-name`)
3. Verify the dataset exists in Data Discovery
4. Check if the dataset name has changed recently

### Confluence Page Creation Fails

**Issue**: Agent cannot create or update Confluence pages

**Solutions**:
1. Verify you have **write permissions** in the FCB space
2. Check if the parent page (264501298309) still exists
3. Ensure Atlassian MCP is authenticated correctly
4. Try refreshing Confluence authentication

### Scala Code Analysis Issues

**Issue**: Agent misunderstands business rules or extracts incorrect information

**Solutions**:
1. Ensure Scala files follow standard patterns (see project rules)
2. Check for unusual code structures that might confuse parsing
3. Manually review the generated documentation and provide corrections
4. Report specific patterns that cause issues to improve the agent

### Performance

**Issue**: Agent takes a long time to complete

**Expected behavior**:
- Simple products: 2-5 minutes
- Complex products with Product Interaction: 5-10 minutes
- Updates with no changes: 1-2 minutes

The agent will display the total time taken upon completion.

---

## Additional Resources

### Additional Resources

### Cross-Segment AI Tools
- [Cross-Segment AI Tools Repository](https://github.com/nubank/cross-segment-ai-tools) - Repository containing this and other AI agents
- Available agents in the ecosystem:
  - **Rapidash** - Audience Manager Attribute Generator
  - **Pé de Pano** - Purple Loop Campaign Automation
  - **CLM Doc Creator** - This agent

### Documentation Links
- [Confluence Space (FCB)](https://nubank.atlassian.net/wiki/spaces/FCB/)
- [CLM Data Products Rules (Parent Page)](https://nubank.atlassian.net/wiki/spaces/FCB/pages/264501298309/CLM+Data+Products+Rules)
- [Setting Up Cursor for Confluence Integration](https://nubank.atlassian.net/wiki/spaces/DOC/pages/264239124130/Setting+Up+Cursor+for+Confluence+Integration)
- [How to Use Cursor Data Discovery MCP](https://nubank.atlassian.net/wiki/spaces/Playbooks/pages/264342546910/How+to+Use+Cursor+Data+Discovery+MCP)

### FreeWilly
- [FreeWilly](https://backoffice.nubank.com.br/free-willy/) - Dataset discovery and metadata tool

### Support
For questions or issues with the agent:
1. Check this documentation first
2. Review the `.mdc` file for detailed implementation notes
3. Consult the [Cross-Segment AI Tools documentation](https://github.com/nubank/cross-segment-ai-tools)
4. Contact the Data Infrastructure team
5. Report issues to improve the agent Purple Loop campaign updates and template management

---

## Version History

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.1.0 | 2026-01-12 | Added Cross-Segment AI Tools installation instructions and agent availability information | Samuel Chaves |
| 1.0.0 | 2026-01-12 | Initial documentation | Samuel Chaves |

---

**Last Updated**: January 12, 2026  
**Agent Version**: 1.0.0  
**Status**: Experimental
