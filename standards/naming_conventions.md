# Naming Conventions

Standardized naming conventions for consistent organization and discoverability across the Central Prompt Library.

## 📁 Directory Structure

### Root Level
```
/prompts/           # Core prompt content
/templates/         # Reusable templates
/standards/         # Guidelines and standards
/compliance/        # Regulatory frameworks
/governance/        # Management procedures
```

### Subdirectory Patterns
```
/prompts/{category}/{subcategory}/
/standards/{domain}/
/compliance/{regulation}/
/governance/{process_type}/
```

## 📄 File Naming

### Format Pattern
```
{action}_{subject}_{modifier}.md
```

### Examples
- `generate_code_python.md`
- `categorize_ticket_priority.md`
- `summarize_meeting_technical.md`
- `extract_entities_medical.md`

### Components

#### Action (Required)
Primary function of the prompt:
- `generate` - Create new content
- `categorize` - Classify or organize
- `summarize` - Condense information
- `extract` - Pull specific data
- `transform` - Modify format/style
- `analyze` - Examine or evaluate
- `review` - Assess quality/compliance
- `escalate` - Raise to higher level

#### Subject (Required)
Target of the action:
- `code` - Programming code
- `ticket` - Support/issue tickets
- `document` - Written content
- `meeting` - Meeting content
- `email` - Email communication
- `report` - Formal reports
- `data` - Structured data
- `conversation` - Dialogue content

#### Modifier (Optional)
Additional specificity:
- Technology: `python`, `javascript`, `sql`
- Domain: `medical`, `financial`, `technical`
- Complexity: `basic`, `advanced`, `complex`
- Priority: `urgent`, `high`, `standard`
- Format: `json`, `xml`, `csv`

## 🏷️ Category Structure

### Primary Categories
```
/prompts/
├── generation/          # Content creation
├── classification/      # Categorization tasks
├── transformation/      # Format/style changes
├── summarization/       # Content condensation
├── extraction/          # Data extraction
├── analysis/           # Content analysis
└── review/             # Quality assessment
```

### Subcategory Examples
```
/prompts/generation/
├── code/               # Code generation
├── content/            # Written content
├── documentation/      # Technical docs
└── communication/      # Messages, emails

/prompts/classification/
├── priority/           # Priority assignment
├── sentiment/          # Sentiment analysis
├── category/           # Content categorization
└── risk/              # Risk assessment
```

## 📊 Metadata Naming

### Required Fields
```yaml
purpose: "Brief description"
category: "primary_category"
subcategory: "sub_category"
domain: "application_domain"
complexity: "simple|moderate|complex"
tags: ["tag1", "tag2", "tag3"]
```

### Tag Standards
Use lowercase, underscore-separated tags:
- **Technology**: `python`, `javascript`, `sql_server`
- **Domain**: `healthcare`, `financial_services`, `network_ops`
- **Function**: `code_generation`, `data_analysis`, `compliance_check`
- **Urgency**: `time_sensitive`, `standard_process`, `low_priority`

## 🔗 Cross-Reference Naming

### Internal Links
```markdown
[Related Prompt](../category/subcategory/prompt_name.md)
[Standard Reference](../../standards/domain/standard_name.md)
[Compliance Guide](../../compliance/regulation/guideline_name.md)
```

### Anchor Links
```markdown
[Section Reference](#section-name)
[Subsection Link](#sub-section-name)
```

## 📝 Variable Naming

### Prompt Variables
Use descriptive, snake_case variables:
```
{user_input}
{document_type}
{priority_level}
{compliance_requirement}
{output_format}
```

### Template Placeholders
```
{DOMAIN_SPECIFIC_CONTEXT}
{REGULATORY_FRAMEWORK}
{TECHNICAL_REQUIREMENTS}
{BUSINESS_OBJECTIVE}
```

## 📋 Version Control

### File Versioning
Include version information in metadata:
```yaml
version: "1.2.0"
last_updated: "2024-01-15"
changelog: "See version_history section"
```

### Branch Naming
```
feature/add-{category}-{subject}
fix/update-{specific-issue}
docs/improve-{documentation-area}
compliance/update-{regulation}
```

## 🎯 Quality Standards

### Clarity Requirements
- Use clear, descriptive names
- Avoid abbreviations unless standard
- Include sufficient context
- Maintain consistency across related items

### Consistency Rules
- Follow established patterns
- Use standard terminology
- Maintain hierarchical logic
- Document exceptions clearly

### Discoverability Guidelines
- Include relevant keywords
- Use searchable terms
- Provide multiple access paths
- Enable tag-based filtering

## 🔍 Search Optimization

### Keyword Strategy
Include primary search terms in:
- File names
- Directory structure
- Metadata tags
- Content headers

### Synonym Management
Document alternative terms:
```yaml
aliases: ["alternative_name", "common_abbreviation"]
related_terms: ["synonym1", "synonym2"]
```

## 📈 Maintenance

### Regular Reviews
- Monthly naming consistency audits
- Quarterly pattern effectiveness assessment
- Annual convention updates
- Ongoing user feedback integration

### Evolution Process
1. Identify naming issues or opportunities
2. Propose convention updates
3. Review with stakeholders
4. Implement with migration plan
5. Update documentation and training

## ❌ Common Mistakes

### Avoid These Patterns
- Inconsistent case usage
- Overly generic names
- Unclear abbreviations
- Missing category information
- Redundant information
- Special characters in names

### Examples of Poor Naming
```
❌ prompt1.md
❌ GenerateCode.md
❌ ticket_cat.md
❌ sum-meeting@2024.md
❌ extract_stuff_from_things.md
```

### Corrected Examples
```
✅ generate_code_python.md
✅ categorize_ticket_priority.md
✅ summarize_meeting_technical.md
✅ extract_entities_medical.md
```

## 📞 Support

For naming convention questions:
- Review existing examples in each category
- Consult the governance team
- Reference domain-specific standards
- Follow the contribution guidelines