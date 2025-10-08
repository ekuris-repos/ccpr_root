# Transform Text Style

Transform text from one writing style to another while maintaining the core message and information.

## Metadata
- **Purpose**: Convert text between different writing styles (formal/casual, technical/plain language, etc.)
- **Category**: transformation
- **Domain**: communication, documentation
- **Complexity**: moderate
- **Last Updated**: 2024-01-15

## Prompt

```
Transform the following text from {source_style} to {target_style}, maintaining all key information and ensuring the message remains clear and accurate.

Source Style: {source_style}
Target Style: {target_style}
Audience: {target_audience}

Text to transform:
{input_text}

Requirements:
- Preserve all factual information
- Maintain the original intent and tone appropriateness
- Ensure clarity for the target audience
- Keep technical accuracy where applicable
- Format appropriately for the target style

Please provide:
1. The transformed text
2. A brief explanation of key changes made
3. Any important considerations for the target audience
```

## Example Usage

### Input:
```
Source Style: Technical documentation
Target Style: Plain language explanation
Audience: Non-technical users

Text: "The API endpoint utilizes RESTful architecture with JSON payload transmission via HTTP POST requests to facilitate data persistence in the backend database system."
```

### Expected Output:
```
**Transformed Text:**
The system receives information through a web interface. When you submit data, it sends the information to our servers where it's saved in our database for future use.

**Key Changes:**
- Removed technical jargon (API, RESTful, JSON payload)
- Simplified complex concepts into everyday language
- Used active voice and direct address ("you submit")
- Focused on what the user experiences rather than technical implementation

**Considerations:**
- Maintains accuracy while removing intimidating technical terms
- Uses familiar concepts (web interface, servers, database)
- Emphasizes user benefit and action rather than system mechanics
```

## Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `{source_style}` | Current writing style of the text | Yes | - |
| `{target_style}` | Desired output writing style | Yes | - |
| `{target_audience}` | Intended audience for transformed text | Yes | General audience |
| `{input_text}` | Text to be transformed | Yes | - |

## Style Options

### Source/Target Styles
- **Formal business** - Professional, structured, objective
- **Casual conversational** - Informal, friendly, personal
- **Technical documentation** - Precise, detailed, systematic
- **Plain language** - Simple, clear, accessible
- **Academic** - Scholarly, research-focused, analytical
- **Marketing** - Persuasive, benefit-focused, engaging
- **Legal** - Precise, comprehensive, risk-aware
- **Medical** - Clinical, accurate, patient-appropriate

## Guidelines

- Always verify that transformed content maintains factual accuracy
- Consider cultural and contextual appropriateness for target audience
- Preserve any regulatory or compliance requirements in the original text
- Test transformed content with representative audience members when possible
- Be particularly careful with technical, medical, or legal content transformations

## Related Prompts

- [Summarize Document](../summarization/summarize_document.md)
- [Generate Content](../generation/generate_content.md)
- [Review Content Quality](../review/review_content_quality.md)

## Compliance Notes

- Ensure transformed content meets any regulatory requirements from original
- Maintain confidentiality and privacy standards during transformation
- For medical content, verify clinical accuracy is preserved
- For legal content, ensure no liability implications from simplification

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2024-01-15 | Initial creation with comprehensive style options |