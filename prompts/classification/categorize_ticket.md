# Categorize Ticket

## Purpose
Automatically classify support tickets into appropriate categories and priority levels.

## Context
Use this prompt for triaging incoming support requests and routing them to appropriate teams.

## Prompt Template
```
Analyze the following support ticket and provide classification:

Ticket Content:
[TICKET_DESCRIPTION]

Classify the ticket with:
1. Category: [HARDWARE/SOFTWARE/NETWORK/ACCESS/OTHER]
2. Priority: [LOW/MEDIUM/HIGH/CRITICAL]
3. Department: [IT/HR/FINANCE/OPERATIONS/SECURITY]
4. Estimated Resolution Time: [TIME_ESTIMATE]
5. Required Skills: [SKILL_SET]

Additional Context:
- User Role: [USER_ROLE]
- System Environment: [ENVIRONMENT]
- Business Impact: [IMPACT_LEVEL]
```

## Examples
- IT helpdesk tickets
- Customer support requests
- Internal service requests
- Bug reports

## Expected Output Format
- Structured classification data
- Confidence level for each classification
- Reasoning for categorization
- Recommended next steps

## Notes
- Include escalation triggers
- Consider business hours and SLA requirements
- Factor in user permissions and access levels