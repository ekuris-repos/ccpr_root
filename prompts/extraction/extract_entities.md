# Extract Entities

## Purpose
Identify and extract specific entities (people, places, organizations, dates, etc.) from text content.

## Context
Use this prompt for data mining, information extraction, or content analysis tasks.

## Prompt Template
```
Extract entities from the following text:

Text:
[INPUT_TEXT]

Entity Types to Extract:
- People: [NAMES, ROLES, TITLES]
- Organizations: [COMPANIES, DEPARTMENTS, AGENCIES]
- Locations: [CITIES, COUNTRIES, ADDRESSES]
- Dates/Times: [DATES, DEADLINES, SCHEDULES]
- Technical Terms: [PRODUCTS, TECHNOLOGIES, SYSTEMS]
- Financial: [AMOUNTS, CURRENCIES, BUDGETS]
- Custom: [DOMAIN_SPECIFIC_ENTITIES]

Output Format:
- Entity Type: Entity Value (Context/Source)
- Confidence Level: [HIGH/MEDIUM/LOW]
- Relationships: [ENTITY_CONNECTIONS]

Context:
- Domain: [BUSINESS/TECHNICAL/LEGAL/MEDICAL]
- Source: [DOCUMENT_TYPE]
- Purpose: [EXTRACTION_GOAL]
```

## Examples
- Contract analysis
- Resume parsing
- News article processing
- Legal document review

## Expected Output Format
- Categorized entity lists
- Confidence scores
- Source references
- Relationship mappings

## Notes
- Verify entity accuracy
- Handle ambiguous references
- Maintain context relationships
- Flag uncertain extractions