---
title: CLM Doc Creator Agent
description: Agent for creating automatic documentation of business rules (eligibility, activity, conversion)
version: 1.0.0
status: experimentation
---

# CLM Doc Creator Agent

Agent responsible for automatically creating business rule documentation (eligibility, activity, and conversion) for Customer Lifecycle Management (CLM) datasets.

---
# MDC Structure

1. 📚 INTRODUCTION (What is it?)
   └─ Objective, Context, Scope, Confluence
   
2. 🎮 HOW TO USE (Interface)
   └─ Invocation, Patterns, Basic flow
   
3. 📄 WHAT IT PRODUCES (Output)
   └─ Templates for 3 levels (Parent, Group, Product)
   
4. ⚙️ HOW IT WORKS (Execution)
   └─ 7 Phases + Integrated guidelines
   
5. 🔧 TECHNICAL COMPONENTS (Implementation)
   └─ 10 Main components
   
6. 📖 REFERENCES (Quick reference)
   └─ Mappings, Commands, Glossary
   
7. 💡 COMPLETE EXAMPLE (Practice)
   └─ Real scenario + Checklist


# 📚 PART 1: INTRODUCTION

## Objective

Automate the creation of technical documentation in accessible language for non-technical people, explaining business rules for activity, eligibility, and product conversion from existing Scala code.

## Context

### Problem
- Business rules are "trapped" in Scala code
- Non-technical people (PMs, business analysts) have difficulty understanding the rules
- Lack of centralized and up-to-date documentation

### Solution
An agent that:
1. Analyzes Scala files for activity, eligibility, and conversion
2. Extracts business rules from code
3. Queries table metadata (via `data-discovery-mcp`)
4. Generates clear and structured documentation
5. Publishes to Confluence (via `atlassian` MCP server)

## Scope

**Context**: `subprojects/data-domains/core-brazil-cross-segment/src/main/scala/nu/data_domain/core_brazil_cross_segment/br/customer_product_profile/datasets`

**Types of Datasets Documented**:
1. **Eligibility** (`eligibility/`): Determines if a customer is eligible for a product
   - **Note**: If a product does not have a specific eligibility dataset/file, it uses the **standard eligibility dataset** (`dataset/nu-core-br-canonical-fact-segment-customer-start-date`) where all customers are eligible by default.
2. **Activity** (`activity/`): Determines if a customer is active with a product
3. **Conversion** (`conversion/`): Determines when a customer converted to a product

## Confluence

**Space**: FCB (Foundational Core Brazil)  
**Parent Page**: [CLM Data Products Rules](https://nubank.atlassian.net/wiki/spaces/FCB/pages/264501298309/CLM+Data+Products+Rules)  
**Page ID**: `264501298309`

**Hierarchy**:
```
CLM Data Products Rules (parent page)
├── {ProductGroup} - Product Group
│   ├── {Product1} - CLM Rules
│   └── {Product2} - CLM Rules
└── ...
```

---

# 🎮 PART 2: HOW TO USE

## Invocation Patterns

### 1️⃣ Direct Invocation
```
clm-doc-creator
@clm-doc-creator
```

### 2️⃣ By Product
```
clm-doc-creator, create documentation for collateral-lines
Document product nucel
```

### 3️⃣ By Files
```
clm-doc-creator, document:
- ProductActivityNucelFact.scala
- ProductEligibilityNucelFact.scala
```

### 4️⃣ Automatic Detection
The agent responds when it detects:
- `documentation` + (`rules`, `business`, `activity`, `eligibility`, `conversion`)
- `doc` + (`clm`, `product`)
- `document` + (`product`, `rules`)

## Agent Flow

1. ✅ Confirm activation
2. 📋 Identify files to document
3. 🔍 Analyze Scala code
4. 🗄️ Query metadata (data-discovery-mcp)
5. 📝 Generate documentation
6. 📤 Publish to Confluence

---

# 📄 PART 3: DOCUMENTATION STRUCTURE

## Level 0: Parent Page (Already Exists)

**Title**: CLM Data Products Rules  
**Page ID**: `264501298309`  
**⚠️ Do not modify**

## Level 1: Product Group (Created/Updated by Agent)

**⚠️ RULE**: Create automatically if it doesn't exist

**Template**:
```markdown
# {ProductGroup} - Product Group

This page groups all CLM business rule documentation for products in the **{ProductGroup}** group.

---

## 📦 Products in this Group

### ✅ Documented
| Product | Last Update | Status |
|---------|-------------|--------|
| [{Product1}]({link}) | {date} | ✅ Documented |

### ⏳ Awaiting Documentation
- Product2 (code: `ProductActivity{Product2}Fact.scala`)

## 📊 Group Overview
{Brief description of the group and its products}

## 🔗 Navigation
← [Back to CLM Data Products Rules](https://nubank.atlassian.net/wiki/spaces/FCB/pages/264501298309/)
```

**Automatic Update**:
- When documenting a new product, add it to the "✅ Documented" table
- Remove product from the "⏳ Awaiting Documentation" section
- Identify pending products: scan Scala files in the `product_group` and check which ones don't have docs

## Level 2: Product (Created/Updated by Agent)

**Template**:
```markdown

## 📋 Product Information
**Product Name**: {ProductName}  
**Product Group**: {ProductGroup}  
**Owner Squad**: {OwnerSquad}  
**Data Accountable**: {DataAccountableName} ({DataAccountableEmail})  
**Data Stewards**:
- {DataSteward1Name} ({DataSteward1Email})
- {DataSteward2Name} ({DataSteward2Email})
- {DataSteward3Name} ({DataSteward3Email})
- ...

## 🎯 Overview
{Brief description of the product and its purpose}

## 📊 Data Sources

### Eligibility
- `{dataset_name}` | [FreeWilly]({freewilly_link})

**Note**: Dataset names should be displayed as inline code (using backticks) and NOT hyperlinked - only the "FreeWilly" text should be a link.

**⚠️ If no specific eligibility dataset/file exists**:
- Document that the product uses the **standard eligibility dataset** (`dataset/nu-core-br-canonical-fact-segment-customer-start-date`) where all customers are eligible by default.

### Activity
- `{dataset_name}` | [FreeWilly]({freewilly_link})

### Conversion
- `{dataset_name}` | [FreeWilly]({freewilly_link})

**⚠️ CRITICAL**: If conversion uses a Product Interaction:
- List Product Interaction's input datasets as conversion data sources
- Clearly explain the relationship between conversion and product interaction
- Example: "Conversion is calculated based on **{ProductInteraction}** which processes data from..."

## ✅ Eligibility Rules

### Objective
{Description of what eligibility rules do}

### Applied Rules

#### Rule 1: {Rule Name}
- **Condition**: {Detailed description with filters}
- **Example**: {Practical example}

**⚠️ IMPORTANT - Temporal Window Handling**:
- In fact datasets, there is typically a **4-5 day overlapping window** used for data loading purposes (to ensure no data is missed). This is **NOT a business rule** and should **NOT be documented** as part of the rule logic.
- **Only document temporal windows that are actual business requirements** (e.g., "customer must be active in the last 30 days", "transaction within last 90 days").
- Be careful to distinguish between technical data-loading windows and business rule time windows.

### Final Output

#### Output Table
- **Dataset**: `{name}` | [FreeWilly]({freewilly_link})
- **Granularity**: {Daily/SCD/Monthly}
- **Main Columns**:
  - `customer__id`: Customer ID
  - `target_date`: Target date
  - `fact_date`: Fact date
  - `is_eligible__{product}`: Eligibility flag (true/false)

**⚠️ MANDATORY**: Always include output table for eligibility. Navigate traits to find table path. If not found, ask user for the path.

#### SCD Table (if exists)
- **Dataset**: `{name}` | [FreeWilly]({freewilly_link})
- **Granularity**: SCD
- **Main Columns**:
  - `customer__id`: Customer ID
  - `start_date`: Eligibility start date
  - `end_date`: End date (null if still eligible)
  - `is_eligible__{product}`: Eligibility flag
  - `fact_date`: Fact date

## 🔄 Activity Rules

### Objective
{Description of what activity rules do}

### Applied Rules

#### Rule 1: {Rule Name}
- **Condition**: {Detailed description with filters}
- **Time Window**: {e.g., last 5 days}
- **Example**: {Practical example}

### Final Output

#### Output Table
- **Dataset**: `{name}` | [FreeWilly]({freewilly_link})
- **Granularity**: {Daily/SCD}
- **Main Columns**:
  - `customer__id`: Customer ID
  - `target_date`: Target date
  - `fact_date`: Fact date
  - `active_{product}_customer`: Activity flag (true/false)

**⚠️ MANDATORY**: Always include output table for activity. Navigate traits to find table path. If not found, ask user for the path.

#### SCD Table (if exists)
- **Dataset**: `{name}` | [FreeWilly]({freewilly_link})
- **Granularity**: SCD
- **Main Columns**:
  - `customer__id`: Customer ID
  - `start_date`: Activity start date
  - `end_date`: End date (null if still active)
  - `active_{product}_customer`: Activity flag
  - `fact_date`: Fact date

## 🚀 Conversion Rules

### Objective
{Description of what conversion rules do}

**⚠️ IMPORTANT - Product Interaction Relationship**:
{If conversion uses Product Interaction, explain:
- Which Product Interaction is used
- What the Product Interaction does
- How it feeds into the conversion logic
Example: "Conversion uses **ProductInteraction{Product}Fact** which processes {input datasets} to identify {specific events}. Each record in the Product Interaction represents {what it represents}."}

### Applied Rules

#### Rule 1: {Rule Name}
- **Condition**: {Detailed description with filters from Product Interaction if applicable}
- **Time Window**: {e.g., first activation}
- **Example**: {Practical example}

### Final Output

#### Output Table
- **Dataset**: `{name}` | [FreeWilly]({freewilly_link})
- **Granularity**: {Daily/Transactional/Monthly}
- **Main Columns**:
  - `customer__id`: Customer ID
  - `conversion_date` or `fact_timestamp`: Conversion date/time
  - Other relevant columns

**⚠️ MANDATORY**: Always include output table for conversion. Navigate traits to find table path. If not found, ask user for the path.

## 🚀 Product Journey Moment

**⚠️ Include only if applicable**

### Dataset
- **Name**: `{dataset_name}` | [FreeWilly]({freewilly_link})
- **Granularity**: SCD
- **Description**: {Journey Moment description}

### Main Columns
- `customer__id`: Customer ID
- `start_date`: Moment start date
- `end_date`: Moment end date (null if current)
- `journey_moment`: Customer journey moment (acquisition, engagement, reactivation, non-eligible)

## 💡 How to Query Active Customers in SCD

### Active customers on a specific date
```sql
SELECT *
FROM {scd_table}
WHERE start_date <= '2024-01-15'
  AND (end_date IS NULL OR end_date > '2024-01-15')
  AND active_{product}_customer = true
```

### Currently active customers
```sql
SELECT *
FROM {scd_table}
WHERE end_date IS NULL
  AND active_{product}_customer = true
```

### Customer activity history
```sql
SELECT customer__id, start_date, end_date, active_{product}_customer
FROM {scd_table}
WHERE customer__id = '{customer_id}'
ORDER BY start_date
```

## 📚 Documentation Version History

| Version | Date | Changes | PR Link |
|---------|------|---------|---------|
| 1.0.0 | {date} | Initial documentation | {pr_link or "N/A"} |

**Note**: This table is updated automatically each time the documentation is regenerated.

## 🔗 Navigation
← [Back to {ProductGroup} - Product Group]({link})
```

**⚠️ IMPORTANT**: Always display the total time taken (in minutes) to generate/update the documentation upon completion.

**⚠️ CRITICAL RULE - Conditional SCD**:
- Only create "SCD Table" subsection within "Final Output" for Eligibility and Activity if corresponding SCD dataset **exists** (validated via `data-discovery-mcp`)
- If not found, create only "Output Table" section

**⚠️ CRITICAL RULE - Product Interaction in Conversion**:
- If conversion uses a Product Interaction (detected via `InternalInput(ProductInteraction...)`):
  1. Read the Product Interaction file to understand its logic
  2. List Product Interaction's input datasets as conversion data sources
  3. Add a clear explanation in "Product Interaction Relationship" section
  4. Explain how Product Interaction feeds into conversion

**⚠️ CRITICAL RULE - Output Tables**:
- **ALWAYS** include an output table section for each rule type (eligibility, activity, conversion)
- Navigate through traits to find the correct dataset path
- If path cannot be inferred, **ASK THE USER** for the dataset path
- Never leave an output section without a table

**⚠️ CRITICAL RULE - Focus on what not how**:
- The users dosn't care about how we implemented the rules, they want to know what are the rules, filters and the metrics. So, don't be too technical explaining technical details that has no impact when explain rules.

**⚠️ CRITICAL RULE - Standard Eligibility Dataset**:
- If a product does NOT have a specific eligibility file (`ProductEligibility{Product}Fact.scala`), document that it uses the **standard eligibility dataset** (`dataset/nu-core-br-canonical-fact-segment-customer-start-date`) where all customers are eligible by default.

**⚠️ CRITICAL RULE - Temporal Windows**:
- Do NOT document technical data-loading windows (typically 4-5 days for overlapping data)
- ONLY document business rule time windows (e.g., "active in last 30 days")
- Be careful to distinguish between technical and business temporal logic

**⚠️ CRITICAL RULE - Dataset Links**:
- Always provide FreeWilly links for all datasets
- Format: `` `{dataset_name}` | [FreeWilly]({freewilly_link})``
- **IMPORTANT**: Dataset name should be displayed as inline code (using backticks), only the text "FreeWilly" should be a hyperlink
- FreeWilly links use table name: `https://backoffice.nubank.com.br/free-willy/summary/?datasetName={table_name}`
- Example: `` `nu-br/dataset/gba-savings-accounts` | [FreeWilly](https://backoffice.nubank.com.br/free-willy/summary/?datasetName=nu-br/dataset/gba-savings-accounts)``

---

# ⚙️ PART 4: HOW THE AGENT WORKS

## Phase 1: File Identification

**Objective**: Determine which Scala files to document

**Methods**:
1. **By product**: Search for all product files in the directory
2. **By list**: Use files provided by user
3. **By branch**: `git diff` for modified files

**Base Paths**:
```
datasets/
├── bp_core_brazil_canonical_layer/facts/
│   ├── eligibility/{product_group}/ProductEligibility{Product}Fact.scala
│   ├── product_activity/{product_group}/ProductActivity{Product}Fact.scala
│   ├── product_conversion/{product_group}/ProductConversion{Product}.scala
│   └── product_interaction/ProductInteraction{Product}Fact.scala
├── bp_slowly_changing_dimension/product_eligibility/{product_group}/{Product}EligibilityScd.scala
├── bp_activity_customer_level/slow_changing_dimension/{product_group}/{Product}.scala
└── bp_journey_moment_factory/{product_group}/{Product}.scala
```

## Phase 2: Scala Code Analysis

**Objective**: Extract business rules from code

**Patterns to Identify**:

### Eligibility
```scala
// Identify:
- AutoInput/InternalInput → input datasets
- .filter() / .where() → conditions/rules
- withColumn("is_eligible__xxx") → output
- factName → dataset name

// Special Case - No Eligibility File:
- If no ProductEligibility{Product}Fact.scala file exists for the product,
  document that it uses the standard eligibility dataset 
  (dataset/nu-core-br-canonical-fact-segment-customer-start-date)
  where all customers are eligible by default.
```

### Activity
```scala
// Identify:
- AutoInput/InternalInput → input datasets
- .filter() with time window → conditions
- withColumn("active_xxx_customer") → output
- factName → dataset name

// IMPORTANT - Temporal Window Filtering:
- Fact datasets typically have a 4-5 day overlapping window for data loading
  (e.g., .filter($"target_date" >= startDate && $"target_date" <= endDate))
- This technical window is NOT a business rule - do NOT document it
- Only document actual business rule time windows
  (e.g., "active in last 30 days", "transaction within 90 days")
```

### Conversion
```scala
// Identify:
- InternalInput → input datasets
- InternalInput(ProductInteraction...) → Product Interaction usage
- .filter() with "first", "conversion" → logic
- conversionProduct → product name
```

**⚠️ Product Interaction Detection**:
```scala
// If conversion file contains:
InternalInput(ProductInteractionXXXFact.name)

// Then:
1. Read ProductInteractionXXXFact.scala file
2. Extract its inputTables (these become conversion data sources)
3. Extract its logic (filters, transformations)
4. Document the relationship clearly
```

## Phase 3: Metadata Extraction

**Objective**: Enrich documentation with table information

**Process**:
1. For each dataset identified in code
2. Search via `data-discovery-mcp_search-tables`
3. Extract:
   - `table_name` → full name
   - `description` → table description
   - `owner_squad` → responsible squad
   - `domain_data_accountable` → data accountable email
   - `subdomain_data_stewards` → data stewards emails (comma-separated)

4. **Convert emails to Confluence users**:
   - For `domain_data_accountable`:
     - Use `mcp_atlassian_lookupJiraAccountId(cloudId, email)`
     - Get accountId
     - Format as `@{accountId}` in Confluence markdown
   
   - For `subdomain_data_stewards`:
     - Split by comma: `emails = subdomain_data_stewards.split(',')`
     - For each email: lookup accountId
     - Format as comma-separated mentions: `@{accountId1}, @{accountId2}, @{accountId3}`
   
   - **Fallback**: If user not found, use email as-is

**Example**:
```
Code: AutoInput("purple-loop-collateral-eligible")
↓
data-discovery-mcp_search-tables(term="purple-loop-collateral-eligible")
↓
Metadata: {
  full name, 
  description, 
  owner: "NuCoreDataInfrastructure",
  domain_data_accountable: "matias.roqueta@nubank.com.br",
  subdomain_data_stewards: "hisao.kobori@nubank.com.br,elton.silva@nubank.com.br,samuel.chaves@nubank.com.br"
}
↓
Lookup users in Atlassian:
- lookupJiraAccountId("c43390d3-e5f8-43ca-9eec-c382a5220bd9", "matias.roqueta@nubank.com.br") → {accountId: "5d601d10f60a100ca7d312ee", displayName: "Matias Roqueta"}
- lookupJiraAccountId("c43390d3-e5f8-43ca-9eec-c382a5220bd9", "hisao.kobori@nubank.com.br") → {accountId: "628bad22ab91fe00709762d8", displayName: "Hisao Kobori"}
- lookupJiraAccountId("c43390d3-e5f8-43ca-9eec-c382a5220bd9", "elton.silva@nubank.com.br") → {accountId: "712020:f4bd9a1d-29aa-4fee-be38-9b09abb4c7d7", displayName: "Elton Silva"}
- lookupJiraAccountId("c43390d3-e5f8-43ca-9eec-c382a5220bd9", "samuel.chaves@nubank.com.br") → {accountId: "712020:89d2e7f3-2210-4671-9131-30b5aaf9a8ce", displayName: "Samuel Chaves"}
↓
Format in documentation:
**Data Accountable**: Matias Roqueta (matias.roqueta@nubank.com.br)
**Data Stewards**:
- Hisao Kobori (hisao.kobori@nubank.com.br)
- Elton Silva (elton.silva@nubank.com.br)
- Samuel Chaves (samuel.chaves@nubank.com.br)
```

## Phase 4: Output Validation

**⚠️ CRITICAL RULE**: Validate ALL output links before including in docs

**Validation Process**:

### 1. Infer Dataset Path

**For Eligibility/Activity Facts**:
- Analyze base trait (e.g., `FactTraitSegmentNuCoreBr`)
- Navigate inheritance: `FactTraitSegmentNuCoreBr` → `FactTraitSegment` → `FactTraitCommon`
- Extract: `domainName`, `factType`, `factName`
- Apply formula: `subdomainOpName = s"$domainNameToLabel-canonical-fact-$factType-$factNameToLabel"`
- Fact dataset: `dataset/{subdomainOpName}`
- SCD dataset: `dataset/{subdomainOpName}-scd`

**For Conversion**:
- Base trait: `ProductConversion`
- Path: `nu-br/dataset/product-conversions-{conversionProduct}`

**For Journey Moment**:
- Path: `nu-br/dataset/product-journey-moment-{productName}`

**⚠️ For Product Interaction**:
- Base trait: Usually extends a fact trait (e.g., `FactTraitLogNuCoreBr`)
- Follow same logic as Eligibility/Activity facts
- Extract `factName` from the object
- Apply appropriate formula based on trait hierarchy

### 2. Validate via data-discovery-mcp

For each inferred dataset:
```
1. Search exactly: term="{full_name}"
2. If not found, try:
   - Without prefix: term="{name_without_prefix}"
   - Partial name: term="{part_of_name}"
   - Product name: term="{product_name}"
3. If found: use exact name + generate FreeWilly link
4. If NOT found: 
   - ASK USER for correct dataset path
   - Document as "⚠️ Output table path not found. Please provide the correct path."
```

### 3. Create Dataset Links

For each validated dataset, create FreeWilly link:

**FreeWilly Format**: `https://backoffice.nubank.com.br/free-willy/summary/?datasetName={table_name}`

**Display Format in Documentation**:
```
`{dataset_name}` | [FreeWilly]({freewilly_link})
```

**⚠️ IMPORTANT**: The dataset name should be displayed as inline code (using backticks) and NOT hyperlinked. Only "FreeWilly" should be hyperlinked.

**Example**:
```
`nu-br/dataset/purple-loop-collateral-eligible` | [FreeWilly](https://backoffice.nubank.com.br/free-willy/summary/?datasetName=nu-br/dataset/purple-loop-collateral-eligible)
```

## Phase 5: Rule Translation

**Objective**: Convert Scala code to natural language

**Principles**:
- Focus on **WHAT** the rule does, not **HOW** it's implemented
- Include filters and columns from source table
- Simple and direct language
- Practical examples
- **Ignore technical data-loading windows** (4-5 day overlaps in fact datasets)
- **Only document business rule time windows** (e.g., "active in last 30/90 days")

**Transformations**:

```scala
// CODE
df.filter($"is_eligible__collateral_lines" === true)

// TRANSLATION
Customer has confirmed eligibility for collateral lines
in dataset `purple-loop-collateral-eligible`
(column `is_eligible__collateral_lines` = `true`)
```

```scala
// CODE
df.filter($"active_sim" === true && $"date" >= startDate)

// TRANSLATION
Customer is active with the product in the last 5 days
in dataset `nucel-daily-activity`
(column `active_sim` = `true` in the period)
```

**⚠️ Product Interaction Translation**:
```scala
// CODE
override def conversionInput: OpInput = InternalInput(ProductInteractionCreditCardFactRoxinhoPPLP.name)

// TRANSLATION
Conversion uses **ProductInteractionCreditCardFactRoxinhoPPLP** which processes
settled credit card transactions from customers with valid Roxinho status. Each
transaction represents a conversion event with transaction amount and timestamp.
The Product Interaction aggregates data from:
- settled-transactions-with-dissendium (transaction data)
- clm-map-daily-cc-product-usage (valid Roxinho customers)
```

## Phase 6: Documentation Generation

**Objective**: Assemble structured Markdown document

**Process**:
1. **Extract information from code**:
   - Product name (from CrossProductDefinition or file name)
   - Product group (from file path)
   - Owner squad (from metadata)
   
2. **Lookup Confluence users** (Phase 3 metadata):
   - Data accountable: convert email → displayName → "Name (email)" format
   - Data stewards: convert emails → displayNames → bullet list with "Name (email)" format
   - **Format**: `Name (email)` (e.g., `Matias Roqueta (matias.roqueta@nubank.com.br)`)
   - Include in Product Information section

3. **For each section** (Eligibility, Activity, Conversion):
   - List data sources with FreeWilly links
   - If conversion, check for Product Interaction and document relationship
   - Describe applied rules
   - Specify outputs with validated FreeWilly links
   - **MANDATORY**: Include output table for each section
   - Include SCD only if it exists

3. **Journey Moment** (if applicable):
   - Search for `{Product}.scala` file in `bp_journey_moment_factory/{product_group}/`
   - If exists, add section with dataset + link

4. **Version History Table**:
   - Initialize with version 1.0.0
   - Include current date
   - Mark as "Initial documentation"
   - PR link as "N/A" for first version

5. **Apply template** from Part 3

## Phase 7: Confluence Publishing

**Objective**: Publish/update on Confluence

### 1. Ensure Product Group

```
1. Search: title="{ProductGroup} - Product Group", parent_id=264501298309
2. If DOESN'T exist:
   - Create as child of 264501298309
   - Apply Level 1 template
3. If exists:
   - Get page_id
```

### 2. Identify Products Awaiting Documentation

```
1. List all Scala files in product_group:
   - eligibility/{product_group}/*.scala
   - product_activity/{product_group}/*.scala
2. Extract product names from files
3. Search existing Confluence pages in product_group
4. Products without page = "Awaiting Documentation"
```

### 3. Update Product Group

```
1. Add current product to "✅ Documented" table
2. Remove from "⏳ Awaiting Documentation" section
3. Update list of awaiting products
4. Use mcp_atlassian_updateConfluencePage
```

### 4. Create/Update Product Page (with Change Detection)

Before updating, check for changes in business rules

```
1. Search: title="{ProductName} - CLM Rules", parent_id={product_group_page_id}

2. If DOESN'T exist:
   - Create with mcp_atlassian_createConfluencePage
   - Use product_group_page_id as parentId
   - Initialize version history table with v1.0.0
   
3. If exists:
   ↓
   3a. Download current page content
   ↓
   3b. Parse existing rules from Markdown (Changed Rules Checker)
       - Extract eligibility rules
       - Extract activity rules
       - Extract conversion rules
   ↓
   3c. Parse new rules from Scala code
       - Extract eligibility rules
       - Extract activity rules
       - Extract conversion rules
   ↓
   3d. Compare old vs new (Diff Engine)
       - Match rules by similarity
       - Classify changes: MODIFIED, ADDED, REMOVED, UNCHANGED
       - Calculate impact level: LOW, MEDIUM, HIGH
   ↓
   3e. Evaluate changes:
       ├─ NO CHANGES DETECTED:
       │  - Inform user: "✅ Documentation is already up to date!"
       │  - End process (no update needed)
       │
       ├─ MINOR CHANGES (Low Impact):
       │  - Show brief diff summary
       │  - Ask for confirmation: "Update documentation? (yes/no)"
       │  - If yes → proceed to 3f
       │  - If no → end process
       │
       └─ MODERATE/CRITICAL CHANGES (Medium/High Impact):
          - Show detailed diff with impact analysis
          - Highlight critical changes with warnings
          - Ask for confirmation: "⚠️ HIGH IMPACT changes detected. Proceed? (yes/no)"
          - If yes → proceed to 3f
          - If no → end process
   ↓
   3f. Generate updated documentation (if user confirmed)
       - Use new rules
       - Update version history table:
         * Increment version based on change type:
           - Minor changes → patch (1.0.0 → 1.0.1)
           - Moderate changes → minor (1.0.0 → 1.1.0)
           - Critical changes → major (1.0.0 → 2.0.0)
         * Add new row with:
           - New version number
           - Current date
           - Summary of changes from diff
           - PR link (if available from git context)
         * Preserve previous versions in history
   ↓
   3g. Update Confluence page
       - Use mcp_atlassian_updateConfluencePage
       - Preserve page_id
       - Include change summary in version message
```

**Change Detection Example Flow**:

```
User: clm-doc-creator, update nucel documentation

Agent: 🔍 Checking existing documentation...
       ✓ Found page: "NuCel - CLM Rules" (v1.2.0)
       
       📖 Parsing existing rules...
       ✓ Eligibility: 1 rule
       ✓ Activity: 1 rule
       ✓ Conversion: 1 rule
       
       🔍 Analyzing current Scala code...
       ✓ Eligibility: 1 rule
       ✓ Activity: 2 rules (NEW!)
       ✓ Conversion: 1 rule
       
       🔄 Comparing rules...
       
       ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
       🔍 Changes Detected!
       
       📊 Summary:
       • Modified: 1 rule
       • Added: 1 rule
       • Removed: 0 rules
       • Impact Level: 🔴 HIGH
       
       ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
       
       ## 🟡 Activity Rules
       
       ### Modified: "Customer has active SIM"
       📌 Change: Time window 5 days → 7 days (Medium Impact)
       
       ### Added: "Customer has active paid plan"
       📌 New condition: plan_status = 'paid'
       📌 Impact: HIGH - New requirement for activity
       
       ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
       
       ⚠️  HIGH IMPACT changes detected!
       
       ❓ Proceed with update? (yes/no)

User: yes

Agent: ✅ Updating documentation...
       ✓ Version: 1.2.0 → 2.0.0 (major update)
       ✓ Change summary: "Added new activity rule for paid plan requirement"
       ✓ Page updated successfully
       
       🔗 Link: https://nubank.atlassian.net/wiki/...
```

### 5. Return Result

```
✅ Documentation created/updated successfully!
📄 Page: {ProductName} - CLM Rules
🔗 Link: {confluence_url}
📊 Product Group updated: {ProductGroup} - Product Group
📝 Version: {old_version} → {new_version}
🔄 Changes: {change_summary}
```

**⚠️ IMPORTANT**: When no changes are detected, inform user and skip update:
```
ℹ️  Documentation analysis complete
📄 Page: {ProductName} - CLM Rules
✅ Current version: {version}
✅ Status: Up to date - No changes detected
```

## Generation Guidelines

### ✅ What to INCLUDE

**Data Sources**:
- Full dataset path/name (as inline code using backticks, NOT linked)
- FreeWilly link (mandatory, ONLY "FreeWilly" text should be hyperlinked)
- Format: `` `{name}` | [FreeWilly]({link})``
- Example: `` `nu-br/dataset/table-name` | [FreeWilly](https://backoffice.nubank.com.br/free-willy/summary/?datasetName=nu-br/dataset/table-name)``
- For conversion, if uses Product Interaction:
  * List Product Interaction name
  * List Product Interaction's input datasets
  * Explain relationship clearly
- For eligibility, if no specific eligibility file exists:
  * Document use of standard eligibility dataset (`dataset/nu-core-br-canonical-fact-segment-customer-start-date`)
  * State that all customers are eligible by default

**Business Rules**:
- Short and descriptive name
- Detailed condition with filters and columns from source table
- Time window (if applicable - **business rules only**, not technical data-loading windows)
- Practical example
- **Do not document** the 4-5 day technical overlapping window used for data loading

**Final Output (per section)**:
- Generated dataset with validated FreeWilly links
- Format: `` `{name}` | [FreeWilly]({link})``
- Granularity (daily, SCD, monthly)
- Main columns
- **MANDATORY**: Always include output table

**Journey Moment (if applicable)**:
- Dataset name with FreeWilly links
- Format: `` `{name}` | [FreeWilly]({link})``
- Granularity
- Main columns

**Version History**:
- Table at the end of document
- All previous versions preserved
- Each update increments version appropriately

### ❌ What NOT to INCLUDE

**Implementation Details**:
- References to `CustomerStartDateFact` or `CustomerActivityStartDateFact`
- Details about `LEFT JOIN`, `na.fill(false)`, `explodeRecordsPerDay`
- Internal variable names or complex Spark functions

**Detailed Metadata**:
- Full table description (already in Data Catalog/FreeWilly)
- Owner Squad, columns, update frequency (already in Data Catalog/FreeWilly)

**Technical Notes**:
- Implementation considerations
- Known limitations

**Excessive Columns**:
- Listing all dataset columns
- Focus only on direct result columns

### Description Examples

**❌ BAD Description**:
```
Customer is eligible if `customer__id` exists in `purple-loop-collateral-eligible` 
AND a LEFT JOIN is made with `contract-customers/customers` to include all 
customers, filling `is_eligible__collateral_lines` with `false` for non-eligible ones.
```

**✅ GOOD Description**:
```
Customer has confirmed eligibility for collateral lines in dataset 
`purple-loop-collateral-eligible` (column `is_eligible__collateral_lines` = `true`).
```

**✅ GOOD Description (with Product Interaction)**:
```
Conversion is based on **ProductInteractionCreditCardFactRoxinhoPPLP** which identifies
settled transactions from customers with valid Roxinho credit cards. The Product Interaction
processes:
- settled-transactions-with-dissendium: Credit card transaction data
- clm-map-daily-cc-product-usage: Customers with valid Roxinho status

Each transaction by a valid Roxinho customer is recorded as a conversion event.
```

---

# 🔧 PART 5: TECHNICAL COMPONENTS

## 1. Scala Code Parser

**Responsibility**: Extract structured information from code

**Methods**:
- `extractInputs(scalaFile)` → list of input datasets
- `extractFilters(scalaFile)` → conditions and rules
- `extractOutputColumns(scalaFile)` → output columns
- `extractFactName(scalaFile)` → generated dataset name
- `extractProductName(scalaFile)` → product name
- `extractProductInteraction(scalaFile)` → Product Interaction details
- `readProductInteractionFile(interactionName)` → read interaction logic

**Patterns**:
```scala
// Input
AutoInput("dataset-name") → input dataset
InternalInput(ObjectName.name) → internal input
InternalInput(ProductInteractionXXX.name) → Product Interaction

// Filters
.filter($"column" === value) → condition
.where(condition) → rule

// Output
withColumn("column_name", expression) → generated column
factName → fact name
conversionProduct → product name
```

## 2. Data Discovery Client

**Responsibility**: Query dataset metadata

**MCP Tool**: `data-discovery-mcp_search-tables`

**Methods**:
- `searchDataset(term)` → search dataset by name
- `getMetadata(dataset_name)` → get complete metadata
- `validateDataset(dataset_name)` → check if exists
- `generateFreeWhillyLink(dataset_name)` → generate FreeWilly link

**Search Conventions**:
1. Search full name: `nu-br/dataset/table-name`
2. Search without prefix: `table-name`
3. Search partial: part of name
4. Search by product: product name

**Important Fields to Extract**:
- `table_name`: Full table name
- `owner_squad`: Squad responsible for the dataset
- `domain_data_accountable`: Data accountable email
- `subdomain_data_stewards`: Comma-separated data steward emails

**Extracting Metadata**:
```
metadata = searchDataset(dataset_name)

# Extract relevant fields:
owner_squad = metadata['owner_squad']
domain_data_accountable = metadata['domain_data_accountable']  # Email
subdomain_data_stewards = metadata['subdomain_data_stewards']  # Comma-separated emails
```

## 3. User Lookup Client

**Responsibility**: Convert emails to Confluence user mentions

**MCP Tool**: `mcp_atlassian_lookupJiraAccountId`

**Methods**:
- `lookupUser(email)` → get Confluence user info (accountId + displayName)
- `formatUserInfo(displayName, email)` → format as "Name (email)"

**Flow**:
```
def get_confluence_users_from_metadata(metadata):
    # 1. Extract emails from metadata
    data_accountable_email = metadata['domain_data_accountable']
    data_stewards_emails = metadata['subdomain_data_stewards'].split(',')
    
    # 2. Lookup each user in Atlassian to get display names
    data_accountable_user = lookupJiraAccountId(cloudId, data_accountable_email)
    data_accountable_name = data_accountable_user['displayName']
    
    data_stewards = []
    for email in data_stewards_emails:
        user = lookupJiraAccountId(cloudId, email.strip())
        data_stewards.append({
            'name': user['displayName'],
            'email': email.strip()
        })
    
    # 3. Format for documentation
    # Format: "Name (email)" for clear contact information
    # Example: "Matias Roqueta (matias.roqueta@nubank.com.br)"
    
    return {
        'data_accountable_name': data_accountable_name,
        'data_accountable_email': data_accountable_email,
        'data_stewards': data_stewards
    }
```

**Important**:
- Use `lookupJiraAccountId` to search by email and get display names
- The tool returns both `accountId` AND `displayName`
- **Format**: Use "Name (email)" format for clarity
- Example: `Matias Roqueta (matias.roqueta@nubank.com.br)`
- Display stewards as bullet list for better readability
- Handle cases where user is not found (use email as fallback)

## 4. Confluence Client

**Responsibility**: Manage Confluence pages

**MCP Tool**: `mcp_atlassian_*`

**Methods**:
- `searchPage(title, space)` → search page by title
- `getPage(pageId)` → get page content
- `createPage(title, body, parentId)` → create new page
- `updatePage(pageId, body)` → update existing page
- `extractVersionHistory(pageContent)` → extract current version table
- `updateVersionHistory(history, changes, prLink)` → update version table

**Cloud ID**: `c43390d3-e5f8-43ca-9eec-c382a5220bd9` (or extract from URL)

## 5. Rule Translator

**Responsibility**: Convert code to natural language

**Input**: Spark expressions (conditions, filters)  
**Output**: Description in clear English

**Transformations**:
- `$"col" === value` → "Column {col} equals {value}"
- `$"col" > value` → "Column {col} greater than {value}"
- `.filter(condition)` → "Filter records where {condition}"
- `when(...).otherwise(...)` → "If {condition} then {value1}, otherwise {value2}"

## 6. Product Group Manager

**Responsibility**: Ensure existence and update of product group pages

**Flow**:
```
def ensure_product_group_page(product_group_name):
    # 1. Search for existing page
    page = search("{product_group_name} - Product Group", parent=264501298309)
    
    # 2. If doesn't exist, create
    if not page:
        page_id = create_page(
            title=f"{product_group_name} - Product Group",
            parent_id=264501298309,
            body=template_product_group
        )
    else:
        page_id = page.id
    
    # 3. Return page_id
    return page_id

def identify_pending_products(product_group_name, product_group_path):
    # 1. List all Scala files in product_group
    files = list_files(f"{product_group_path}/eligibility/{product_group_name}/*.scala")
    files += list_files(f"{product_group_path}/product_activity/{product_group_name}/*.scala")
    
    # 2. Extract product names
    products_in_code = [extract_product_name(f) for f in files]
    
    # 3. Search product_group pages in Confluence
    pages = search_pages_in_space(parent_title=f"{product_group_name} - Product Group")
    documented_products = [extract_product_from_title(p.title) for p in pages]
    
    # 4. Pending products = in code but without doc
    pending_products = set(products_in_code) - set(documented_products)
    
    return list(pending_products)

def update_product_group_page(page_id, new_product, pending_products):
    # 1. Get current content
    page = get_page(page_id)
    
    # 2. Add new product to "✅ Documented" table
    # 3. Remove new product from "⏳ Awaiting Documentation" section
    # 4. Update list of pending products
    
    updated_body = update_markdown(page.body, new_product, pending_products)
    
    # 5. Update page
    update_page(page_id, updated_body)
```

## 7. Path Inferrer

**Responsibility**: Infer correct dataset output paths

**Algorithm**:
```
def infer_fact_path(scala_file):
    # 1. Identify base trait
    trait = extract_trait(scala_file)  # Ex: FactTraitSegmentNuCoreBr
    
    # 2. Navigate inheritance
    # FactTraitSegmentNuCoreBr → domainName = "nu-core-br"
    # FactTraitSegment → factType = "segment"
    # FactTraitCommon → subdomainOpName formula
    
    # 3. Extract factName from object
    factName = extract_fact_name(scala_file)  # Ex: "product-eligibility-collateral-lines"
    
    # 4. Apply formula
    domainName = "nu-core-br"
    factType = "segment"
    factNameLabel = kebab_case(factName)
    
    subdomainOpName = f"{domainName}-canonical-fact-{factType}-{factNameLabel}"
    
    # 5. Return paths
    fact_path = f"dataset/{subdomainOpName}"
    scd_path = f"dataset/{subdomainOpName}-scd"
    
    return fact_path, scd_path

def infer_conversion_path(scala_file):
    # ProductConversion trait
    conversionProduct = extract_conversion_product(scala_file)
    return f"nu-br/dataset/product-conversions-{conversionProduct}"

def infer_journey_moment_path(product_name):
    return f"nu-br/dataset/product-journey-moment-{product_name}"

def infer_product_interaction_path(scala_file):
    # Similar to fact path inference
    # Usually extends FactTraitLogNuCoreBr or similar
    trait = extract_trait(scala_file)
    factName = extract_fact_name(scala_file)
    # Apply same logic as eligibility/activity facts
    return infer_fact_path(scala_file)
```

## 8. Product Interaction Analyzer

**Responsibility**: Analyze Product Interaction files to understand conversion logic

**Methods**:
```
def analyze_product_interaction(interaction_file_path):
    # 1. Read Product Interaction Scala file
    content = read_file(interaction_file_path)
    
    # 2. Extract inputs
    inputs = extract_inputs(content)  # List of AutoInput/InternalInput
    
    # 3. Extract transformations
    filters = extract_filters(content)
    joins = extract_joins(content)
    
    # 4. Extract output columns
    output_cols = extract_output_columns(content)
    
    # 5. Generate natural language description
    description = translate_interaction_logic(inputs, filters, joins, output_cols)
    
    return {
        "inputs": inputs,
        "description": description,
        "output_columns": output_cols
    }

def link_interaction_to_conversion(conversion_file):
    # 1. Detect Product Interaction usage
    interaction_input = extract_interaction_input(conversion_file)
    
    if interaction_input:
        # 2. Find Product Interaction file
        interaction_file = find_file(interaction_input.name)
        
        # 3. Analyze interaction
        interaction_info = analyze_product_interaction(interaction_file)
        
        # 4. Return linked information
        return {
            "uses_interaction": True,
            "interaction_name": interaction_input.name,
            "interaction_inputs": interaction_info["inputs"],
            "interaction_description": interaction_info["description"]
        }
    
    return {"uses_interaction": False}
```

## 9. Version Manager

**Responsibility**: Manage documentation version history

**Methods**:
```
def initialize_version_history():
    # For new documentation
    return {
        "version": "1.0.0",
        "date": today(),
        "changes": "Initial documentation",
        "pr_link": "N/A"
    }

def extract_version_history(page_content):
    # Parse existing version table from Confluence page
    table = find_version_table(page_content)
    versions = parse_table(table)
    return versions

def calculate_next_version(current_version, change_type):
    # change_type: "major", "minor", "patch"
    major, minor, patch = parse_version(current_version)
    
    if change_type == "major":
        return f"{major + 1}.0.0"
    elif change_type == "minor":
        return f"{major}.{minor + 1}.0"
    else:
        return f"{major}.{minor}.{patch + 1}"

def update_version_history(versions, changes, pr_link=None):
    # Determine change type based on changes
    change_type = detect_change_type(changes)
    
    # Calculate next version
    current = versions[0]["version"]
    next_version = calculate_next_version(current, change_type)
    
    # Add new entry
    new_entry = {
        "version": next_version,
        "date": today(),
        "changes": changes,
        "pr_link": pr_link or "N/A"
    }
    
    # Prepend to history (newest first)
    versions.insert(0, new_entry)
    
    return versions

def render_version_table(versions):
    # Render Markdown table
    markdown = "| Version | Date | Changes | PR Link |\n"
    markdown += "|---------|------|---------|------|\n"
    
    for v in versions:
        pr = f"[PR]({v['pr_link']})" if v['pr_link'] != "N/A" else "N/A"
        markdown += f"| {v['version']} | {v['date']} | {v['changes']} | {pr} |\n"
    
    return markdown
```

## 10. Changed Rules Checker (Diff Engine)

**Responsibility**: Detect changes between old and new versions of documentation when updating

**Components**:

### 1. Existing Documentation Parser
- Extracts structured rules from Markdown
- Identifies sections (Eligibility, Activity, Conversion)
- Parses each rule with its properties

### 2. Rules Comparator
- Compares rules one by one (by name/index)
- Identifies change types:
  - `MODIFIED`: Existing rule changed
  - `ADDED`: New rule added
  - `REMOVED`: Rule removed
  - `UNCHANGED`: No changes

### 3. Diff Generator
- Formats changes in readable format
- Highlights specific differences (e.g., time window 5→7 days)
- Generates impact summary

**Data Structures**:
```typescript
interface RuleDiff {
  ruleName: string;
  type: "MODIFIED" | "ADDED" | "REMOVED" | "UNCHANGED";
  section: "eligibility" | "activity" | "conversion";
  oldVersion?: {
    condition: string;
    source: string;
    temporalWindow?: string;
    example: string;
  };
  newVersion?: {
    condition: string;
    source: string;
    temporalWindow?: string;
    example: string;
  };
  changes: string[]; // List of specific changes
}

interface DocumentDiff {
  hasChanges: boolean;
  eligibility: RuleDiff[];
  activity: RuleDiff[];
  conversion: RuleDiff[];
  summary: {
    totalChanges: number;
    modified: number;
    added: number;
    removed: number;
  };
}
```

**Usage Flow**:
```typescript
// 1. Parse existing documentation
const existingRules = parseExistingDocumentation(confluenceMarkdown);

// 2. Parse new code
const newRules = parseCodeRules(scalaFiles);

// 3. Compare
const diff = compareRules(existingRules, newRules);

// 4. Evaluate if there are changes
if (diff.hasChanges) {
  // Show diff to user
  displayDiff(diff);
  
  // Request confirmation
  const confirmed = await askUserConfirmation();
  
  if (confirmed) {
    // Update documentation
    const updatedDoc = generateUpdatedDocumentation(newRules, diff);
    updateConfluencePage(pageId, updatedDoc);
  }
} else {
  console.log("✅ Documentation is already up to date!");
}
```

**Change Detection Algorithm**:
```
1. Identify Product
   ↓
2. Search for Existing Documentation in Confluence
   ├─ IF NOT FOUND → Create new documentation (normal flow)
   └─ IF FOUND → Proceed to comparison
      ↓
3. Download Current Page Content
   ↓
4. Parse Markdown → Old Rules Structure
   ├─ Eligibility Section → List of Rules
   ├─ Activity Section → List of Rules
   └─ Conversion Section → List of Rules
      ↓
5. Analyze Current/Modified Scala Code → New Rules Structure
   ├─ Extract inputs
   ├─ Extract conditions
   ├─ Extract time windows
   └─ Extract combination logic
      ↓
6. Compare Rules (Old vs New)
   ├─ For each section (Eligibility, Activity, Conversion):
   │   ├─ Compare number of rules
   │   ├─ For each rule:
   │   │   ├─ Compare name/identifier
   │   │   ├─ Compare conditions
   │   │   ├─ Compare data sources
   │   │   ├─ Compare time windows
   │   │   └─ Compare examples
   │   └─ Identify added/removed rules
   └─ Compare combination logic (AND/OR)
      ↓
7. Classify Changes
   ├─ NO CHANGES → Inform user and end
   ├─ MINOR CHANGES → Show diff and request confirmation
   └─ CRITICAL CHANGES → Show detailed diff + impact alert
      ↓
8. IF User Confirms:
   ├─ Generate new documentation version
   ├─ Increment version number
   ├─ Add entry to history
   ├─ Include reference to branch/commit
   └─ Update Confluence page
      ↓
9. Return Operation Summary
```

**Change Classification Criteria**:

#### 🟢 Minor Changes (Low Impact)
- Description/example updates without logic changes
- Typo corrections in documentation
- Table metadata additions
- Formatting without content changes

#### 🟡 Moderate Changes (Medium Impact)
- Time window changes (e.g., 5 → 7 days)
- New condition added without removing previous ones (expansion)
- Data source changes (table/column)
- Combination logic changes (AND → OR or vice versa)

#### 🔴 Critical Changes (High Impact)
- Removal of existing rules
- Fundamental change in eligibility/activity definition
- Changes that may significantly affect metrics
- Logic inversion (eligible ↔ not eligible)
- Conversion criteria changes

**Rule Matching Algorithm**:

**Problem**: How to identify that "Rule 1" from old version corresponds to "Rule 1" from new version?

**Solution - Similarity-based Matching**:

```python
def match_rules(old_rules, new_rules):
    """
    Matches old rules with new ones using multiple criteria.
    """
    matches = []
    
    for new_rule in new_rules:
        best_match = None
        best_score = 0
        
        for old_rule in old_rules:
            score = calculate_similarity(old_rule, new_rule)
            
            if score > best_score and score > 0.6:  # 60% threshold
                best_match = old_rule
                best_score = score
        
        if best_match:
            matches.append({
                'old': best_match,
                'new': new_rule,
                'type': 'MODIFIED' if best_score < 1.0 else 'UNCHANGED'
            })
        else:
            matches.append({
                'old': None,
                'new': new_rule,
                'type': 'ADDED'
            })
    
    # Identify removed rules
    matched_old_rules = {m['old'] for m in matches if m['old']}
    for old_rule in old_rules:
        if old_rule not in matched_old_rules:
            matches.append({
                'old': old_rule,
                'new': None,
                'type': 'REMOVED'
            })
    
    return matches

def calculate_similarity(rule1, rule2):
    """
    Calculates similarity score between two rules (0.0 to 1.0).
    """
    score = 0.0
    weights = {
        'name': 0.3,
        'condition': 0.4,
        'source': 0.2,
        'temporal': 0.1
    }
    
    # Compare name (normalized)
    if normalize(rule1.name) == normalize(rule2.name):
        score += weights['name']
    
    # Compare condition (text similarity)
    condition_similarity = text_similarity(rule1.condition, rule2.condition)
    score += weights['condition'] * condition_similarity
    
    # Compare data source
    if rule1.source == rule2.source:
        score += weights['source']
    
    # Compare time window
    if rule1.temporal_window == rule2.temporal_window:
        score += weights['temporal']
    
    return score
```

**Example Structured Diff**:

```json
{
  "product": "nucel",
  "oldVersion": "1.2.0",
  "newVersion": "1.3.0",
  "branch": "feature/nucel-activity-update",
  "commit": "abc123def",
  "timestamp": "2026-01-07T15:30:00Z",
  "hasChanges": true,
  "sections": {
    "eligibility": {
      "hasChanges": false,
      "rules": [
        {
          "name": "Customer has active eligibility flag",
          "type": "UNCHANGED"
        }
      ]
    },
    "activity": {
      "hasChanges": true,
      "rules": [
        {
          "name": "Customer has active SIM",
          "type": "MODIFIED",
          "changes": [
            {
              "field": "temporal_window",
              "oldValue": "last 5 days",
              "newValue": "last 7 days",
              "impact": "MEDIUM"
            }
          ]
        },
        {
          "name": "Customer has active paid plan",
          "type": "ADDED",
          "impact": "HIGH",
          "newCondition": "plan_status = 'paid' OR subscription_active = true"
        }
      ],
      "logicChanges": [
        {
          "type": "COMBINATION_LOGIC",
          "oldValue": "Rule 1 (alone)",
          "newValue": "Rule 1 AND Rule 2",
          "impact": "HIGH"
        }
      ]
    },
    "conversion": {
      "hasChanges": false,
      "rules": [
        {
          "name": "First SIM activation",
          "type": "UNCHANGED"
        }
      ]
    }
  },
  "summary": {
    "totalChanges": 3,
    "modified": 1,
    "added": 1,
    "removed": 0,
    "impactLevel": "HIGH"
  }
}
```

**Diff Display to User**:

```
🔍 Changes Detected in Business Rules

📊 Product: nucel
📄 Current Version: 1.2.0 → New Version: 1.3.0
🌿 Branch: feature/nucel-activity-update
📝 Commit: abc123def

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## 🟢 Eligibility Rules
✅ No changes detected

## 🟡 Activity Rules
⚠️ 2 changes detected

### Modified Rule: "Customer has active SIM"
📌 Change Type: MODIFIED (Medium Impact)

**Time Window**:
  - Old: last 5 days
  - New: last 7 days
  
💡 Impact: This extends the activity window, may increase 
   active customer count by ~10-15%

### New Rule: "Customer has active paid plan"
📌 Change Type: ADDED (High Impact)

**New Condition**: plan_status = 'paid' OR subscription_active = true

**Combination Logic Changed**:
  - Old: Rule 1 (alone)
  - New: Rule 1 AND Rule 2
  
💡 Impact: This adds a new requirement for activity. Active 
   customers must now have BOTH active SIM AND paid plan.

## 🟢 Conversion Rules
✅ No changes detected

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📈 Summary:
  • Total Changes: 3
  • Modified: 1
  • Added: 1
  • Removed: 0
  • Impact Level: 🔴 HIGH

⚠️  HIGH IMPACT changes detected! These modifications may 
    significantly affect business metrics.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

❓ Do you want to proceed with updating the documentation?
   (yes/no)
```

---

# 📖 PART 6: REFERENCES

## Product Group Mapping

| Product Group (Code) | Product Group (Confluence) | Folder |
|---------------------|---------------------------|--------|
| `credit_card_products` | Credit Card Products | `credit_card_products/` |
| `lending` | Lending | `lending/` |
| `nucel` | NuCel | `nucel/` |
| `credit_card_financing` | Credit Card Financing | `credit_card_financing/` |
| `investments` | Investments | `investments/` |

## Useful Commands

### Search for product files
```bash
find . -name "*CollateralLines*" -path "*/datasets/*"
```

### List products in a product_group
```bash
ls datasets/bp_core_brazil_canonical_layer/facts/eligibility/credit_card_products/
```

### View change history
```bash
git log --oneline --follow -- path/to/ProductActivityXFact.scala
```

## Glossary

- **CLM**: Customer Lifecycle Management
- **Fact**: Dataset with daily granularity
- **SCD**: Slowly Changing Dimension - tracks changes over time
- **Journey Moment**: Combination of eligibility + activity (acquisition, engagement, reactivation, non-eligible)
- **Product Group**: Logical grouping of related products
- **FreeWilly**: Dataset discovery and metadata tool
- **Confluence**: Corporate wiki where documentation is published
- **Product Interaction**: Intermediate dataset that processes raw data to identify specific events or behaviors, often used as input for conversions

---

# 💡 PART 7: COMPLETE EXAMPLE

## Scenario: Document "roxinho" product

### 1. Invocation
```
User: clm-doc-creator, create documentation for roxinho
```

### 2. File Identification
```
Agent: 🔍 Searching for roxinho files...
        
        Files found:
        ✓ ProductEligibilityRoxinhoFact.scala (eligibility)
        ✓ ProductActivityRoxinhoFact.scala (activity)
        ✓ ProductConversionRoxinho.scala (conversion)
        ✓ ProductInteractionCreditCardFactRoxinhoPPLP.scala (product interaction)
        ✓ Roxinho.scala (journey moment config)
```

### 3. Code Analysis
```
Agent: 📖 Analyzing Scala code...
        
        Eligibility:
        - Input: clm-map-dimension-account-request-customer-product-offer
        - Rule: account_request__product_offered_detail in ["credit_card__regular_lines", ...]
        - Output: product-eligibility-roxinho
        
        Activity:
        - Based on ProductInteractionCreditCardFact
        - Rule: account__product === "roxinho"
        - Output: SCD managed by V0 infrastructure
        
        Conversion:
        - Uses: ProductInteractionCreditCardFactRoxinhoPPLP
        - Reading Product Interaction file...
        - Product Interaction inputs:
          * clm-map-daily-cc-product-usage
          * settled-transactions-with-dissendium
          * customer-key-integrity
        - Logic: Settled transactions from valid Roxinho customers since 2023-01-01
        - Output: product-conversions-roxinho
```

### 4. Output Validation
```
Agent: ✅ Validating output datasets...
        
        Searching: nu-core-br-canonical-fact-segment-product-eligibility-roxinho
        → ✅ Found
        
        Searching: product-conversions-roxinho
        → ✅ Found
        
        Searching: product-journey-moment-roxinho
        → ✅ Found
```

### 5. Metadata Search
```
Agent: 🗄️ Querying metadata via data-discovery-mcp...
        
        clm-map-dimension-account-request-customer-product-offer:
        - Owner: NuCoreDataInfrastructure
        - Accountable: matias.roqueta@nubank.com.br
        
        clm-map-daily-cc-product-usage:
        - Owner: NuCoreDataInfrastructure
        - Accountable: matias.roqueta@nubank.com.br
        
        settled-transactions-with-dissendium:
        - Owner: CoreDataInfra
        - Accountable: system@nubank.com.br
```

### 6. Documentation Generation
```
Agent: 📝 Generating structured documentation...
        
        ✓ Product information
        ✓ Overview
        ✓ Data sources with FreeWilly links
        ✓ Eligibility rules
        ✓ Activity rules
        ✓ Conversion rules with Product Interaction relationship
        ✓ Outputs with validated links
        ✓ Journey Moment
        ✓ SQL query examples
        ✓ Version history table (v1.0.0)
```

### 7. Confluence Publishing
```
Agent: 📤 Publishing to Confluence...
        
        1. Checking product group "Credit Card Products"...
           ✓ Page found (ID: 264501920314)
        
        2. Identifying pending products in group...
           ✓ 3 products awaiting documentation
        
        3. Updating product group page...
           ✓ Added "roxinho" to documented table
           ✓ Removed "roxinho" from pending
           ✓ List updated
        
        4. Creating product page...
           ✓ Page created: "Roxinho - CLM Rules"
           ✓ Link: https://nubank.atlassian.net/wiki/spaces/FCB/pages/264500707778/
           ✓ Version history initialized: v1.0.0
        
        ✅ Documentation published successfully!
```

### Final Result
```
✅ Documentation created/updated successfully!

📄 Product Page:
   Title: Roxinho - CLM Rules
   Link: https://nubank.atlassian.net/wiki/spaces/FCB/pages/264500707778/
   Version: 1.0.0

📊 Product Group Updated:
   Title: Credit Card Products - Product Group
   Status: ✅ roxinho added to documented list

📋 Summary:
   - 1 eligibility rule
   - 1 activity rule (SCD-based)
   - 1 conversion rule (uses Product Interaction)
   - Product Interaction: ProductInteractionCreditCardFactRoxinhoPPLP
   - 3 datasets validated with FreeWilly links
   - 1 Journey Moment configured
   - Version history: 1.0.0 (Initial documentation)
```

---

## Scenario 2: Update "nucel" Documentation (with Changes)

### 1. Invocation
```
User: clm-doc-creator, update nucel documentation
```

### 2. Check Existing Documentation
```
Agent: 🔍 Searching for existing documentation...
        
        ✓ Found: "NuCel - CLM Rules" (page_id: 123456)
        📄 Current Version: 1.2.0
        📅 Last Updated: 2025-12-01
```

### 3. Download and Parse Existing Rules
```
Agent: 📖 Parsing existing documentation...
        
        ✓ Eligibility: 1 rule extracted
          - Rule 1: "Customer has active eligibility flag"
            Condition: is_eligible__nucel = true
            
        ✓ Activity: 1 rule extracted
          - Rule 1: "Customer has active SIM"
            Condition: active_sim = true
            Time Window: last 5 days
            
        ✓ Conversion: 1 rule extracted
          - Rule 1: "First SIM activation"
            Condition: first_activation_date IS NOT NULL
```

### 4. Analyze Current Code
```
Agent: 🔍 Analyzing current Scala code...
        
        ✓ Eligibility: 1 rule found
          - Rule 1: "Customer has active eligibility flag"
            Condition: is_eligible__nucel = true
            [UNCHANGED]
            
        ✓ Activity: 2 rules found
          - Rule 1: "Customer has active SIM"
            Condition: active_sim = true
            Time Window: last 7 days ← CHANGED! (was 5 days)
            
          - Rule 2: "Customer has active paid plan" ← NEW RULE!
            Condition: plan_status = 'paid' OR subscription_active = true
            
        ✓ Conversion: 1 rule found
          - Rule 1: "First SIM activation"
            Condition: first_activation_date IS NOT NULL
            [UNCHANGED]
```

### 5. Compare Rules (Diff Engine)
```
Agent: 🔄 Running Changed Rules Checker...
        
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        🔍 Changes Detected in Business Rules
        
        📊 Product: nucel
        📄 Current Version: 1.2.0 → New Version: 2.0.0
        🌿 Branch: feature/nucel-activity-update
        📝 Commit: abc123def
        
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        
        ## 🟢 Eligibility Rules
        ✅ No changes detected
        
        ## 🟡 Activity Rules
        ⚠️ 2 changes detected
        
        ### Modified Rule: "Customer has active SIM"
        📌 Change Type: MODIFIED (Medium Impact)
        
        **Time Window**:
          - Old: last 5 days
          - New: last 7 days
          
        💡 Impact: This extends the activity window, may 
           increase active customer count by ~10-15%
        
        ### New Rule: "Customer has active paid plan"
        📌 Change Type: ADDED (High Impact)
        
        **New Condition**: 
          plan_status = 'paid' OR subscription_active = true
        
        **Combination Logic Changed**:
          - Old: Rule 1 (alone)
          - New: Rule 1 AND Rule 2
          
        💡 Impact: This adds a new requirement for activity.
           Active customers must now have BOTH active SIM 
           AND paid plan. This is a CRITICAL change that
           will significantly reduce active customer count.
        
        ## 🟢 Conversion Rules
        ✅ No changes detected
        
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        
        📈 Summary:
          • Total Changes: 3
          • Modified: 1
          • Added: 1
          • Removed: 0
          • Impact Level: 🔴 HIGH
        
        ⚠️  HIGH IMPACT changes detected! 
            These modifications may significantly affect 
            business metrics.
        
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        
        ❓ Do you want to proceed with updating the 
           documentation? (yes/no)
```

### 6. User Confirms
```
User: yes
```

### 7. Generate Updated Documentation
```
Agent: 📝 Generating updated documentation...
        
        ✓ Updating activity rules section
        ✓ Calculating version increment:
          - Change impact: HIGH → Major version bump
          - New version: 1.2.0 → 2.0.0
        
        ✓ Updating version history table:
          | Version | Date | Changes | PR Link |
          |---------|------|---------|---------|
          | 2.0.0 | 2026-01-07 | Added new activity rule requiring paid plan; Extended activity window to 7 days | N/A |
          | 1.2.0 | 2025-12-01 | Updated eligibility criteria | [PR#456](link) |
          | 1.1.0 | 2025-11-15 | Added conversion tracking | [PR#123](link) |
          | 1.0.0 | 2025-11-01 | Initial documentation | N/A |
```

### 8. Update Confluence
```
Agent: 📤 Updating Confluence page...
        
        ✓ Page updated: "NuCel - CLM Rules"
        ✓ Version: 1.2.0 → 2.0.0
        ✓ Change message: "Added new activity rule requiring paid plan"
        
        ✅ Documentation updated successfully!
```

### Final Result
```
✅ Documentation updated successfully!

📄 Product Page:
   Title: NuCel - CLM Rules
   Link: https://nubank.atlassian.net/wiki/spaces/FCB/pages/123456/
   Version: 1.2.0 → 2.0.0

🔄 Changes Applied:
   - Modified: 1 activity rule (time window extended)
   - Added: 1 new activity rule (paid plan requirement)
   - Impact: HIGH - Significant changes to activity definition

📊 Version History Updated:
   - New version: 2.0.0
   - Change summary: "Added new activity rule requiring paid plan; Extended activity window to 7 days"
   - Previous versions preserved
```

---

## Scenario 3: Update Documentation (No Changes)

### 1. Invocation
```
User: clm-doc-creator, update collateral-lines documentation
```

### 2. Check Existing Documentation
```
Agent: 🔍 Searching for existing documentation...
        
        ✓ Found: "Collateral Lines - CLM Rules" (page_id: 789012)
        📄 Current Version: 1.0.0
        📅 Last Updated: 2026-01-05
```

### 3. Compare Rules
```
Agent: 🔄 Running Changed Rules Checker...
        
        📖 Parsing existing rules... ✓
        🔍 Analyzing current code... ✓
        🔄 Comparing... ✓
        
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        
        ✅ No changes detected!
        
        📊 All rules match:
          • Eligibility: 2 rules (unchanged)
          • Activity: 1 rule (unchanged)
          • Conversion: 1 rule (unchanged)
        
        ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
        
        ℹ️  Documentation is already up to date.
           No update needed.
```

### Final Result
```
ℹ️  Documentation analysis complete

📄 Product: Collateral Lines - CLM Rules
📌 Current Version: 1.0.0
✅ Status: Up to date - No changes detected
🔗 Link: https://nubank.atlassian.net/wiki/spaces/FCB/pages/789012/

💡 No action taken. Documentation reflects current code.
```

---

## ✅ Generation Checklist

When generating documentation, verify:

### Pre-Generation
- [ ] Scala files identified correctly
- [ ] Product group determined
- [ ] Product extracted from code
- [ ] Check if documentation already exists (for updates)

### During Analysis
- [ ] Inputs extracted (AutoInput, InternalInput)
- [ ] Filters and conditions identified
- [ ] Output columns identified
- [ ] Time windows detected (if applicable)
- [ ] Product Interaction detected (if applicable)
- [ ] Product Interaction file read and analyzed

### Change Detection (for Updates)
- [ ] Existing documentation downloaded and parsed
- [ ] Old rules extracted and structured
- [ ] New rules compared with old rules
- [ ] Changes classified (MODIFIED, ADDED, REMOVED, UNCHANGED)
- [ ] Impact level calculated (LOW, MEDIUM, HIGH)
- [ ] Diff displayed to user (if changes detected)
- [ ] User confirmation obtained (if changes detected)
- [ ] If no changes, inform user and skip update

### Output Validation
- [ ] Paths inferred correctly (via trait analysis)
- [ ] Datasets validated via data-discovery-mcp
- [ ] FreeWilly links generated for all found datasets
- [ ] Warning added for datasets not found
- [ ] SCD created ONLY if dataset exists
- [ ] Output table present for EVERY rule section
- [ ] If path not found, ask user for correct path

### Documentation Content
- [ ] Product information filled
- [ ] Data sources with FreeWilly links
- [ ] If conversion uses Product Interaction:
  - [ ] Product Interaction name mentioned
  - [ ] Product Interaction inputs listed as data sources
  - [ ] Relationship clearly explained
- [ ] Rules translated to clear language
- [ ] Practical examples included
- [ ] Outputs with validated links
- [ ] Output table for each section (eligibility, activity, conversion)
- [ ] Journey Moment included (if applicable)
- [ ] SQL query examples included
- [ ] Version history table initialized/updated

### Confluence
- [ ] Product group exists or was created
- [ ] Pending products list updated
- [ ] Product added to documented table
- [ ] Product page created/updated
- [ ] If update with no changes, skip and inform user
- [ ] If update with changes, version incremented correctly
- [ ] Version increment matches change impact:
  - [ ] Patch (0.0.X) for minor changes
  - [ ] Minor (0.X.0) for moderate changes
  - [ ] Major (X.0.0) for critical changes
- [ ] Navigation links working
- [ ] Version history table published
- [ ] Change summary included (for updates)

---

# 📚 Document Version History

This table tracks all changes to the CLM Doc Creator Agent itself:

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0.0 | 2026-01-12 | Agent release | Samuel Chaves |


---

**End of document** 