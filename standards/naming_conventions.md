# Naming Conventions

**This document demonstrates comprehensive naming standards for enterprise CCPR implementations.** Adapt the complexity and requirements to match your CCPR implementation tier and organizational scale.

Standardized naming conventions for consistent organization and discoverability across the Central Prompt Library.

## 🎯 Important: Naming Complexity by Tier

- **🥉 Tier 1**: Use basic file naming and simple category structure
- **🥈 Tier 2**: Add domain-specific patterns and enhanced metadata
- **🥇 Tier 3**: Implement comprehensive tagging and cross-reference systems
- **🏆 Tier 4**: Add advanced versioning and optimization-focused naming

Choose the naming complexity that supports your organization without creating unnecessary overhead.

## 📁 Directory Structure (*Scale to your organizational needs*)

### Root Level (*Essential for all tiers*)
```
/prompts/           # Core prompt content (required)
/templates/         # Reusable templates (required)
/standards/         # Guidelines (Tier 2+)
/compliance/        # Regulatory frameworks (only if applicable)
/governance/        # Management procedures (Tier 2+)
```

### Subdirectory Patterns (*Implement structure that supports your scale*)
```
/prompts/{category}/                    # Tier 1: Simple structure
/prompts/{category}/{subcategory}/      # Tier 2+: Enhanced organization
/standards/{domain}/                    # Tier 2+: Domain-specific standards
/compliance/{regulation}/               # Only if compliance requirements apply
```

## 📄 File Naming (*Choose pattern appropriate to your complexity*)

### Basic Format Pattern (*Tier 1 - Simple and effective*)
```
{action}_{subject}.md
```
Examples: `generate_code.md`, `categorize_ticket.md`

### Enhanced Format Pattern (*Tier 2+ - More specific*)
```
{action}_{subject}_{modifier}.md
```
Examples: `generate_code_python.md`, `categorize_ticket_priority.md`

### Components (*Use what provides value for your organization*)

#### Action (*Required for all tiers*)
Primary function of the prompt:
- `generate` - Create new content
- `categorize` - Classify or organize  
- `summarize` - Condense information
- `extract` - Pull specific data
- `transform` - Modify format/style
- `analyze` - Examine or evaluate (*Tier 2+*)
- `review` - Assess quality/compliance (*Tier 3+*)

#### Subject (*Required for all tiers*)
Target of the action:
- `code` - Programming code
- `ticket` - Support/issue tickets
- `document` - Written content
- `meeting` - Meeting content
- `email` - Email communication
- `report` - Formal reports

#### Modifier (*Tier 2+ - Optional additional specificity*)
- Technology: `python`, `javascript`, `sql`
- Domain: `medical`, `financial`, `technical` (*only include domains you use*)
- Complexity: `basic`, `advanced` (*if helpful for users*)
- Format: `json`, `xml`, `csv` (*if relevant to your use cases*)

## 🏷️ Category Structure (*Implement categories that match your use cases*)

### Primary Categories (*Start with categories you need*)
```
/prompts/
├── generation/          # Content creation (common starting category)
├── classification/      # Categorization tasks (common starting category)
├── transformation/      # Format/style changes (Tier 2+)
├── summarization/       # Content condensation (common use case)
├── extraction/          # Data extraction (Tier 2+)
└── analysis/           # Content analysis (Tier 3+)
```

### Example Subcategory Implementation (*Tier 2+ - Add as needed*)
```
/prompts/generation/
├── code/               # Code generation (if relevant)
├── content/            # Written content
└── documentation/      # Technical docs (if needed)

/prompts/classification/
├── priority/           # Priority assignment
├── sentiment/          # Sentiment analysis (if relevant)
└── category/           # Content categorization
```

*Implement only the categories and subcategories that provide value for your organization*

## 📊 Metadata Naming (*Scale metadata to your tracking needs*)

### Essential Fields (*Tier 1 - Basic tracking*)
```yaml
purpose: "Brief description"
category: "primary_category"
```

### Enhanced Fields (*Tier 2+ - Better organization*)
```yaml
purpose: "Brief description"
category: "primary_category"
subcategory: "sub_category"          # Tier 2+
domain: "application_domain"         # Tier 2+ if using domain standards
complexity: "simple|moderate|complex" # If helpful for users
tags: ["tag1", "tag2"]              # Tier 2+ for searchability
```

### Advanced Fields (*Tier 3+ - Comprehensive tracking*)
```yaml
# Include additional fields only if they provide value:
author: "creator_name"               # If useful for your organization
version: "1.0.0"                    # If implementing versioning
compliance: ["framework1"]          # Only if compliance requirements apply
```

### Tag Standards (*Tier 2+ - Use tags relevant to your organization*)
Use lowercase, underscore-separated tags for domains you actually use:
- **Technology**: `python`, `javascript` (*only include technologies you use*)
- **Domain**: `healthcare`, `finance` (*only include domains relevant to your org*)
- **Function**: `code_generation`, `data_analysis` (*match your use cases*)

*Don't implement tags you won't use - they add complexity without value*

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

## 📞 Support (*Adapt support to your organization*)

For naming convention questions:
- Review existing examples in categories you're implementing
- Consult administrators or designated reviewers
- Reference standards that apply to your domains  
- Follow contribution guidelines appropriate to your tier

## 🎯 Remember: Start Simple, Grow Systematically

This document shows comprehensive naming patterns for mature CCPR implementations. **Start with basic patterns that solve immediate problems, then add complexity as your organization grows and needs more sophisticated organization.** 

The goal is consistent, discoverable content - not perfect adherence to every pattern shown here. Choose the naming complexity that supports your users without creating unnecessary overhead.