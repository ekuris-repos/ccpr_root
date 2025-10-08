# Basic Prompt Creation Tutorial

## Overview
This step-by-step tutorial walks you through creating your first prompt in the CCPR system, from initial concept to final publication. Perfect for new content creators who want to understand the complete prompt development workflow.

## Prerequisites
- CCPR repository access
- Basic understanding of Markdown
- Familiarity with your organization's compliance requirements
- Text editor or IDE with Markdown support

## Tutorial Learning Objectives
By the end of this tutorial, you will:
- Understand the complete prompt creation process
- Know how to use CCPR templates effectively
- Be able to validate and test your prompts
- Understand the review and approval workflow
- Have published your first prompt to the repository

## Step-by-Step Guide

### Step 1: Planning Your Prompt
Before writing any code, plan your prompt thoroughly.

#### 1.1 Define the Purpose
```markdown
Prompt Purpose Checklist:
□ What specific task will this prompt accomplish?
□ Who is the target audience (technical level, role)?
□ What are the expected input types and formats?
□ What should the ideal output look like?
□ Are there any constraints or limitations?
```

#### 1.2 Choose the Right Category
```markdown
CCPR Categories:
- classification/     # Categorizing or labeling content
- extraction/         # Pulling specific information from text
- generation/         # Creating new content
- summarization/      # Condensing information
- transformation/     # Converting between formats or styles
```

#### 1.3 Research Existing Prompts
```bash
# Search for similar prompts
git log --oneline --grep="classification"
grep -r "sentiment analysis" prompts/
```

### Step 2: Setting Up Your Workspace

#### 2.1 Create Your Working Branch
```bash
# Create and switch to a new feature branch
git checkout -b feature/add-sentiment-analysis-prompt

# Verify you're on the correct branch
git branch
```

#### 2.2 Navigate to the Correct Directory
```bash
# For this tutorial, we'll create a sentiment analysis prompt
cd prompts/classification/
```

#### 2.3 Copy the Template
```bash
# Copy the base template
cp ../../templates/prompt_template.md label_sentiment_advanced.md
```

### Step 3: Developing Your Prompt

#### 3.1 Complete the Metadata Section
```yaml
---
title: "Advanced Sentiment Analysis with Confidence Scoring"
category: "classification"
subcategory: "sentiment_analysis"
author: "Your Name"
created_date: "2024-01-15"
version: "1.0.0"
tags: ["sentiment", "classification", "nlp", "confidence"]
difficulty: "intermediate"
estimated_time: "5-10 minutes"
compliance_frameworks: ["GDPR", "SOC2"]
data_classification: "internal"
review_status: "draft"
---
```

#### 3.2 Write the Purpose Section
```markdown
## Purpose
This prompt performs advanced sentiment analysis on text input, providing both sentiment classification (positive, negative, neutral) and confidence scores. It's designed for analyzing customer feedback, social media posts, and review data while maintaining privacy compliance.

**Use Cases:**
- Customer feedback analysis
- Social media monitoring
- Product review sentiment tracking
- Support ticket prioritization

**Target Audience:**
- Data analysts
- Customer success teams
- Marketing professionals
- Product managers
```

#### 3.3 Craft the Prompt Text
```markdown
## Prompt Text

Analyze the sentiment of the following text and provide your assessment in the specified format.

**Instructions:**
1. Read the provided text carefully
2. Determine the overall sentiment: positive, negative, or neutral
3. Assign a confidence score from 0.0 to 1.0
4. Identify key emotional indicators that influenced your decision
5. Consider context and nuance in your analysis

**Text to analyze:**
{input_text}

**Required Output Format:**
```json
{
  "sentiment": "[positive|negative|neutral]",
  "confidence": [0.0-1.0],
  "key_indicators": [
    "phrase or word 1",
    "phrase or word 2"
  ],
  "reasoning": "Brief explanation of your analysis"
}
```

**Guidelines:**
- Be objective and consider context
- Neutral sentiment should have confidence ≥ 0.7
- Flag ambiguous cases with lower confidence
- Ignore obviously sarcastic "positive" language in negative contexts
```

#### 3.4 Create Comprehensive Examples
```markdown
## Examples

### Example 1: Clear Positive Sentiment
**Input:**
```
I absolutely love this new feature! It's exactly what I needed and works perfectly. The user interface is intuitive and the performance is fantastic. Great job!
```

**Output:**
```json
{
  "sentiment": "positive",
  "confidence": 0.95,
  "key_indicators": [
    "absolutely love",
    "exactly what I needed",
    "works perfectly",
    "fantastic",
    "great job"
  ],
  "reasoning": "Multiple strong positive indicators with no negative qualifiers"
}
```

### Example 2: Negative with Constructive Elements
**Input:**
```
The app crashes frequently and the loading times are terrible. However, I appreciate the effort the team is putting into regular updates. Hopefully these issues get fixed soon.
```

**Output:**
```json
{
  "sentiment": "negative",
  "confidence": 0.75,
  "key_indicators": [
    "crashes frequently",
    "loading times are terrible",
    "issues get fixed"
  ],
  "reasoning": "Primary complaints about functionality outweigh positive acknowledgment of team effort"
}
```

### Example 3: Neutral/Mixed Sentiment
**Input:**
```
The product has some useful features but also some limitations. It works for basic needs but lacks advanced functionality. Price point seems reasonable for what you get.
```

**Output:**
```json
{
  "sentiment": "neutral",
  "confidence": 0.85,
  "key_indicators": [
    "useful features",
    "some limitations",
    "works for basic needs",
    "lacks advanced functionality",
    "price point seems reasonable"
  ],
  "reasoning": "Balanced mix of positive and negative aspects with objective assessment"
}
```
```

#### 3.5 Add Usage Guidelines
```markdown
## Usage Guidelines

### When to Use This Prompt
- ✅ Customer feedback analysis
- ✅ Social media monitoring
- ✅ Product review analysis
- ✅ Support ticket triage

### When NOT to Use This Prompt
- ❌ Medical or health-related sentiment (use specialized healthcare prompts)
- ❌ Legal document analysis (requires legal expertise)
- ❌ Personal/private communications without consent

### Best Practices
1. **Batch Processing**: For large datasets, process in batches of 50-100 items
2. **Quality Control**: Review low-confidence predictions manually
3. **Context Awareness**: Consider domain-specific language and cultural context
4. **Bias Monitoring**: Regularly audit results for potential biases

### Performance Expectations
- **Accuracy**: ~85-90% on general text
- **Speed**: 1-3 seconds per analysis
- **Confidence Threshold**: Use 0.7+ for automated decisions
```

#### 3.6 Document Compliance Considerations
```markdown
## Compliance and Privacy

### Data Protection Notes
- This prompt processes text content that may contain personal opinions
- Ensure proper consent before analyzing customer communications
- Consider data retention policies for analyzed content
- Implement appropriate access controls for sentiment data

### GDPR Compliance
- Classify as "legitimate interest" for business improvement
- Provide opt-out mechanisms for customers
- Maintain audit trails of sentiment analysis activities
- Implement data minimization principles

### SOC2 Considerations
- Log all sentiment analysis requests for audit purposes
- Implement appropriate access controls
- Monitor for unusual usage patterns
- Maintain data integrity throughout the process
```

### Step 4: Testing and Validation

#### 4.1 Self-Test Your Prompt
```markdown
Testing Checklist:
□ Run through all provided examples
□ Test with edge cases (very short text, mixed languages)
□ Verify output format consistency
□ Check compliance with guidelines
□ Validate metadata completeness
```

#### 4.2 Use the Validation Script
```bash
# Run automated validation
python scripts/validate_prompt.py prompts/classification/label_sentiment_advanced.md

# Check for common issues
python scripts/check_quality.py prompts/classification/label_sentiment_advanced.md
```

#### 4.3 Manual Review
```markdown
Manual Review Checklist:
□ Clear and unambiguous instructions
□ Comprehensive examples covering edge cases
□ Proper output format specification
□ Complete metadata
□ Compliance considerations documented
□ No sensitive data in examples
□ Consistent writing style and tone
```

### Step 5: Submitting for Review

#### 5.1 Commit Your Changes
```bash
# Add your new file
git add prompts/classification/label_sentiment_advanced.md

# Commit with descriptive message
git commit -m "Add advanced sentiment analysis prompt with confidence scoring

- Includes positive, negative, and neutral classification
- Provides confidence scores and reasoning
- Comprehensive examples with edge cases
- GDPR and SOC2 compliance documentation
- Targets intermediate users for customer feedback analysis"
```

#### 5.2 Push to Remote Repository
```bash
# Push your branch to the remote repository
git push origin feature/add-sentiment-analysis-prompt
```

#### 5.3 Create Pull Request
```markdown
Pull Request Template:

Title: Add Advanced Sentiment Analysis Prompt

Description:
This PR introduces a new sentiment analysis prompt designed for customer feedback analysis with the following features:

**Key Features:**
- Sentiment classification (positive/negative/neutral)
- Confidence scoring (0.0-1.0)
- Key indicator identification
- Detailed reasoning output

**Testing Completed:**
- [x] Automated validation scripts
- [x] Manual quality review
- [x] Example verification
- [x] Compliance check

**Compliance Frameworks:**
- [x] GDPR compliant
- [x] SOC2 considerations documented

**Target Users:**
- Data analysts
- Customer success teams
- Marketing professionals

Closes #123 (if applicable)
```

### Step 6: Review Process

#### 6.1 Respond to Reviewer Feedback
```markdown
Review Response Best Practices:
- Address all reviewer comments
- Make requested changes promptly
- Explain decisions if you disagree with suggestions
- Test changes thoroughly before re-submitting
- Thank reviewers for their time and insights
```

#### 6.2 Common Review Items
```markdown
Typical Reviewer Comments:
□ "Add more edge case examples"
□ "Clarify output format requirements"
□ "Update compliance documentation"
□ "Fix formatting issues"
□ "Improve prompt clarity"
```

### Step 7: Publication and Post-Publication

#### 7.1 Merge to Main Branch
Once approved, your prompt will be merged to the main branch and become available to all users.

#### 7.2 Monitor Usage and Feedback
```markdown
Post-Publication Monitoring:
- Check usage analytics (if available)
- Monitor feedback channels
- Watch for reported issues
- Plan improvements for next version
```

#### 7.3 Version Management
```markdown
Future Updates:
- Follow semantic versioning (1.0.0 → 1.1.0 for features)
- Document changes in commit messages
- Update version metadata
- Consider backward compatibility
```

## Common Challenges and Solutions

### Challenge 1: Unclear Output Format
**Problem:** Users aren't sure what format to expect from the AI.
**Solution:** Provide explicit JSON schema and multiple examples.

### Challenge 2: Inconsistent Results
**Problem:** The prompt produces varying results for similar inputs.
**Solution:** Add more specific guidelines and constraint instructions.

### Challenge 3: Compliance Confusion
**Problem:** Uncertainty about which compliance frameworks apply.
**Solution:** Consult with legal team and document all relevant considerations.

### Challenge 4: Poor Performance
**Problem:** The prompt doesn't work well in practice.
**Solution:** Gather user feedback, analyze failure cases, and iterate.

## Next Steps

### Immediate Actions
1. **Practice**: Create 2-3 more prompts using this process
2. **Review Others**: Study highly-rated prompts in the repository
3. **Join Community**: Participate in prompt review discussions
4. **Learn Advanced Techniques**: Explore prompt engineering best practices

### Advanced Topics to Explore
- **Chain-of-Thought Prompting**: For complex reasoning tasks
- **Few-Shot Learning**: Using examples to guide AI behavior
- **Prompt Optimization**: A/B testing different prompt variations
- **Integration Patterns**: How prompts work with larger systems

### Resources for Continued Learning
- [Advanced Prompt Engineering Guide](../reference/advanced-techniques.md)
- [Community Best Practices](../contributing/best-practices.md)
- [Prompt Template Documentation](../reference/templates.md)
- [Compliance Guidelines](../../compliance/)

## Conclusion

Congratulations! You've successfully created, tested, and submitted your first CCPR prompt. This tutorial covered the complete workflow from planning to publication. 

Remember that prompt creation is an iterative process - your first version doesn't need to be perfect. Focus on solving real problems for your users, and improve based on feedback and usage data.

The skills you've learned here will help you contribute effectively to the CCPR repository and create high-quality prompts that benefit your entire organization.

## Quick Reference Card

```markdown
Prompt Creation Checklist:
□ Plan purpose and audience
□ Choose appropriate category
□ Copy and customize template
□ Complete all metadata fields
□ Write clear instructions
□ Create comprehensive examples
□ Document compliance considerations
□ Run validation scripts
□ Test thoroughly
□ Submit pull request
□ Respond to review feedback
□ Monitor post-publication usage
```

For questions or support, contact the CCPR team at [ccpr-support@company.com](mailto:ccpr-support@company.com) or visit our internal documentation portal.