# Common Issues and Solutions

## Overview
This troubleshooting guide addresses the most frequently encountered issues in the CCPR system, providing step-by-step solutions and prevention strategies for users across all roles.

## Access and Permission Issues

### Issue: Cannot Access Repository

#### Symptoms
- "Repository not found" errors
- "Permission denied" when cloning or pushing
- Unable to see repository in organization
- Authentication failures

#### Diagnosis Steps
1. **Verify Account Status**
   ```bash
   # Check if you're logged into the correct account
   git config --global user.name
   git config --global user.email
   
   # For GitHub
   gh auth status
   
   # For Azure DevOps
   az account show
   ```

2. **Check Repository URL**
   ```bash
   # Verify the repository URL is correct
   git remote -v
   
   # Check if repository exists (if you have any access)
   curl -I https://github.com/organization/repository-name
   ```

3. **Validate Permissions**
   - Check organization membership
   - Verify team assignments
   - Confirm repository access levels

#### Solutions

##### Solution 1: Authentication Issues
```bash
# Re-authenticate with Git platform
# For GitHub
gh auth login

# For Azure DevOps  
az login

# For GitLab
# Update stored credentials through Git credential manager
git credential-manager-core configure
```

##### Solution 2: Incorrect Remote URL
```bash
# Update remote URL if incorrect
git remote set-url origin https://github.com/organization/correct-repository-name.git

# Or for SSH
git remote set-url origin git@github.com:organization/correct-repository-name.git
```

##### Solution 3: Missing Organization Access
**Contact Required**: Repository administrator or IT support
**Information to Provide**:
- Your username/email
- Repository name you need access to
- Your role (content creator, reviewer, etc.)
- Business justification for access

#### Prevention
- Bookmark correct repository URLs
- Use SSH keys for more reliable authentication
- Regularly verify team memberships
- Keep authentication tokens current

### Issue: Insufficient Permissions for Actions

#### Symptoms
- Cannot create branches
- Unable to submit pull requests
- Cannot merge approved changes
- "Write access required" errors

#### Diagnosis Steps
1. **Check Current Permissions**
   - Review your role in the repository settings
   - Verify team membership and permissions
   - Check if repository has special restrictions

2. **Identify Required Permission Level**
   ```yaml
   Permission Requirements:
     read_repository: "Read access"
     create_branches: "Write access"
     submit_pull_requests: "Write access"
     approve_reviews: "Review permissions"
     merge_changes: "Maintain or Admin access"
     modify_settings: "Admin access"
   ```

#### Solutions

##### Solution 1: Request Permission Upgrade
**Contact**: Repository administrator
**Template Request**:
```markdown
Subject: Repository Permission Request - [Repository Name]

Dear [Administrator Name],

I am requesting elevated permissions for the [Repository Name] repository.

Current Permission: [Current Level]
Requested Permission: [Desired Level]
Role: [Content Creator/Reviewer/etc.]
Justification: [Business reason for upgrade]

My username is [username] and email is [email].

Thank you for your consideration.
```

##### Solution 2: Use Correct Workflow
- Ensure you're following the correct branch workflow
- Submit pull requests instead of direct pushes
- Request reviews from authorized personnel

#### Prevention
- Understand permission requirements for your role
- Follow established workflows and procedures
- Communicate permission needs during onboarding

## Git and Version Control Issues

### Issue: Merge Conflicts

#### Symptoms
- "Merge conflict" errors during pull or merge
- Conflicting changes indicators in files
- Unable to complete merge automatically

#### Diagnosis Steps
1. **Identify Conflict Type**
   ```bash
   # Check status to see conflicted files
   git status
   
   # View conflict details
   git diff
   
   # See conflict markers in files
   grep -n "<<<<<<< HEAD" filename.md
   ```

2. **Understand Conflict Source**
   - Simultaneous edits to same sections
   - Different branch modifications
   - Upstream changes conflicting with local work

#### Solutions

##### Solution 1: Manual Conflict Resolution
```bash
# Step 1: Pull latest changes
git pull origin main

# Step 2: Open conflicted files and look for conflict markers
# <<<<<<< HEAD
# Your changes
# =======
# Conflicting changes
# >>>>>>> branch-name

# Step 3: Edit files to resolve conflicts
# Remove conflict markers and choose/combine changes

# Step 4: Stage resolved files
git add resolved-file.md

# Step 5: Complete the merge
git commit -m "Resolve merge conflicts in [file names]"
```

##### Solution 2: Use Merge Tools
```bash
# Configure a merge tool (one-time setup)
git config --global merge.tool vimdiff  # or your preferred tool

# Use merge tool to resolve conflicts
git mergetool

# Complete the merge
git commit -m "Resolve conflicts using merge tool"
```

##### Solution 3: Abort and Retry
```bash
# If conflicts are too complex, abort the merge
git merge --abort

# Try a different approach or get help
git stash  # Save your changes
git pull origin main  # Get latest
git stash pop  # Reapply your changes
```

#### Prevention
- Pull latest changes before starting work
- Use feature branches for development
- Communicate with team about overlapping work
- Keep changes focused and atomic

### Issue: Accidentally Committed Wrong Files

#### Symptoms
- Sensitive information in commit history
- Large files causing repository bloat
- Personal files not intended for repository

#### Diagnosis Steps
```bash
# Check what was committed
git log --oneline -5

# See files in specific commit
git show --name-only [commit-hash]

# Check file content in commit
git show [commit-hash]:path/to/file
```

#### Solutions

##### Solution 1: Remove from Latest Commit (Not Pushed)
```bash
# Remove file from commit but keep in working directory
git reset --soft HEAD~1
git reset HEAD unwanted-file.txt
git commit -m "Original commit message without unwanted file"

# Or amend the commit
git reset HEAD unwanted-file.txt
git commit --amend
```

##### Solution 2: Remove from History (Not Pushed)
```bash
# Use git filter-branch to remove file from history
git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch unwanted-file.txt' \
--prune-empty --tag-name-filter cat -- --all
```

##### Solution 3: Already Pushed (Requires Coordination)
**WARNING**: This rewrites history and affects other users
```bash
# Contact team before proceeding
# Force push after history rewrite (dangerous)
git push origin main --force-with-lease
```

##### Solution 4: Sensitive Data (Immediate Action Required)
1. **Immediately**: Contact security team
2. **Remove**: Use git-filter-repo or BFG Repo-Cleaner
3. **Rotate**: Change any exposed credentials
4. **Audit**: Review access logs for potential exposure

#### Prevention
- Use .gitignore file properly
- Review changes before committing
- Use git add selectively instead of git add .
- Set up pre-commit hooks for sensitive data detection

## Content and Template Issues

### Issue: Template Validation Failures

#### Symptoms
- Automated checks failing on pull requests
- "Required section missing" errors
- Metadata validation failures
- Formatting errors in templates

#### Diagnosis Steps
1. **Check Validation Output**
   ```bash
   # Review CI/CD pipeline output
   # Look for specific validation error messages
   # Check which sections are failing validation
   ```

2. **Compare Against Template**
   ```bash
   # Compare your file against the standard template
   diff your-prompt.md templates/prompt_template.md
   
   # Check metadata format
   head -20 your-prompt.md
   ```

#### Solutions

##### Solution 1: Fix Missing Sections
```markdown
# Ensure all required sections are present:
- Purpose
- Prompt Text  
- Examples
- Guidelines
- Compliance Notes

# Add any missing sections using the template
```

##### Solution 2: Correct Metadata Format
```yaml
# Ensure YAML front matter is properly formatted
---
title: "Proper Title Format"
category: "valid_category"  # Must be from approved list
author: "Your Name"
created_date: "2025-10-08"  # ISO format
version: "1.0.0"  # Semantic versioning
compliance_frameworks: ["GDPR"]  # Array format
tags: ["tag1", "tag2"]  # Array of strings
---
```

##### Solution 3: Fix Markdown Formatting
```bash
# Use a Markdown linter to check formatting
npx markdownlint your-prompt.md

# Common fixes needed:
# - Add blank lines before/after headers
# - Fix list formatting
# - Correct code block syntax
# - Ensure proper link formatting
```

#### Prevention
- Use template as starting point
- Validate locally before submitting
- Set up local linting tools
- Review template documentation

### Issue: Prompt Performance Problems

#### Symptoms
- Inconsistent outputs from prompts
- Low accuracy or quality scores
- User complaints about prompt effectiveness
- High revision rates during review

#### Diagnosis Steps
1. **Analyze Prompt Structure**
   - Review instruction clarity
   - Check example quality and coverage
   - Assess complexity level
   - Validate test cases

2. **Gather Performance Data**
   ```yaml
   Performance Metrics to Check:
     accuracy_rate: "< 80% indicates issues"
     consistency_score: "High variance indicates problems"
     user_satisfaction: "< 3.5/5 needs attention"
     revision_requests: "> 3 iterations suggests issues"
   ```

#### Solutions

##### Solution 1: Improve Instructions
```markdown
# Make instructions more specific and actionable
# Before:
Analyze the text and provide insights.

# After:
Analyze the customer feedback text and provide:
1. Sentiment classification (positive/negative/neutral)
2. Key themes mentioned (list top 3)
3. Specific actionable recommendations
4. Confidence score for your analysis
```

##### Solution 2: Enhance Examples
```markdown
# Add diverse, high-quality examples
# Include edge cases and boundary conditions
# Show both good and problematic inputs
# Provide clear expected outputs
```

##### Solution 3: Refine Guidelines
```markdown
# Add specific quality criteria
# Include common pitfalls to avoid
# Provide troubleshooting steps
# Set clear success metrics
```

#### Prevention
- Test thoroughly during development
- Get feedback from intended users
- Monitor performance metrics post-deployment
- Iterate based on real-world usage

## Review and Approval Issues

### Issue: Stuck in Review Process

#### Symptoms
- Reviews taking longer than expected timeline
- No feedback from reviewers
- Conflicting feedback from multiple reviewers
- Reviews failing without clear reasons

#### Diagnosis Steps
1. **Check Review Status**
   - Verify who is assigned as reviewers
   - Check review timeline and expectations
   - Look for any blocking issues or dependencies

2. **Review Feedback Quality**
   - Ensure all reviewer feedback is addressed
   - Check if feedback is actionable
   - Verify if additional clarification is needed

#### Solutions

##### Solution 1: Follow Up with Reviewers
```markdown
# Professional follow-up message template:
Subject: Review Status Check - [Prompt Name]

Hi [Reviewer Name],

I submitted [Prompt Name] for review on [Date], and wanted to check on the status. The review timeline indicates [X days], and we're currently at [Y days].

Is there any additional information I can provide to facilitate the review? Are there any blocking issues I should address?

Please let me know if you need any clarification or if there's anything I can do to help move this forward.

Thank you for your time and consideration.
```

##### Solution 2: Address Conflicting Feedback
1. **Document the conflicts clearly**
2. **Request clarification from reviewers**
3. **Escalate to governance team if needed**
4. **Propose compromise solutions**

##### Solution 3: Escalate Appropriately
**When to escalate**:
- Reviews exceed stated timelines significantly
- Conflicting requirements from different reviewers
- Unclear or unreasonable feedback
- Process blockers outside your control

**How to escalate**:
```markdown
Subject: Review Process Escalation - [Prompt Name]

Dear [Governance Team/Team Lead],

I am escalating an issue with the review process for [Prompt Name]:

Issue: [Clear description of the problem]
Timeline: [Expected vs actual timeline]
Steps Taken: [What you've tried to resolve]
Impact: [Business impact of delay]

I would appreciate guidance on how to proceed.

Attachments:
- Original submission
- Review feedback received
- Correspondence with reviewers
```

#### Prevention
- Set clear expectations with reviewers upfront
- Provide high-quality submissions to minimize revisions
- Follow up proactively within reasonable timeframes
- Build relationships with review team members

## Platform-Specific Issues

### GitHub Enterprise Issues

#### Issue: Actions/Workflows Failing

#### Symptoms
- CI/CD pipelines failing unexpectedly
- Workflow permissions errors
- Runner availability issues

#### Solutions
```yaml
# Check workflow status
# Review action logs for specific errors
# Verify runner availability and permissions
# Update workflow dependencies if needed

Common Fixes:
  - Update action versions to latest
  - Check GitHub token permissions
  - Verify runner labels and availability
  - Review branch protection rule conflicts
```

### Azure DevOps Issues

#### Issue: Pipeline Authorization Problems

#### Solutions
```yaml
# Common Azure DevOps fixes:
Pipeline_Permissions:
  - Check service connection authorization
  - Verify agent pool permissions
  - Update pipeline security settings
  - Review resource authorization
```

### GitLab Issues

#### Issue: CI/CD Runner Problems

#### Solutions
```yaml
# GitLab-specific troubleshooting:
Runner_Issues:
  - Check runner registration
  - Verify runner tags and matching
  - Review pipeline permissions
  - Update GitLab CI configuration
```

## Performance and System Issues

### Issue: Slow Repository Operations

#### Symptoms
- Long clone/fetch times
- Slow web interface loading
- Timeout errors during operations

#### Solutions

##### Solution 1: Repository Optimization
```bash
# Clean up local repository
git gc --aggressive
git prune

# Reduce repository size
git filter-branch --tree-filter 'rm -rf large-file' HEAD
```

##### Solution 2: Network Optimization
- Use SSH instead of HTTPS when possible
- Configure Git to use multiple connections
- Consider using Git LFS for large files

#### Prevention
- Keep repository size manageable
- Use .gitignore effectively
- Regular repository maintenance
- Monitor and clean up large files

## Getting Additional Help

### Internal Support Channels

#### Repository Administrators
- **For**: Access issues, technical problems, system configuration
- **Contact**: [Admin email/channel]
- **Response Time**: 4-8 hours during business days

#### Governance Team
- **For**: Process questions, policy clarification, escalations
- **Contact**: [Governance email/channel]
- **Response Time**: 1-2 business days

#### Compliance Team
- **For**: Regulatory questions, compliance validation, risk assessment
- **Contact**: [Compliance email/channel]
- **Response Time**: 2-3 business days

### External Resources

#### Platform Documentation
- **GitHub**: https://docs.github.com/enterprise
- **Azure DevOps**: https://docs.microsoft.com/azure/devops
- **GitLab**: https://docs.gitlab.com

#### Community Forums
- **Git**: Git community forums and Stack Overflow
- **Platform-Specific**: Official community forums
- **Industry**: AI and prompt engineering communities

### Emergency Procedures

#### Security Incidents
1. **Immediate**: Stop using potentially compromised systems
2. **Report**: Contact security team immediately
3. **Document**: Record all relevant details
4. **Follow-up**: Cooperate with incident response procedures

#### Business-Critical Blockers
1. **Assess Impact**: Determine business criticality
2. **Escalate**: Contact appropriate stakeholders
3. **Document**: Record issue details and timeline
4. **Communicate**: Keep stakeholders informed of progress

## Issue Prevention Strategies

### Proactive Measures
- **Regular Training**: Keep skills current with system updates
- **Best Practices**: Follow established procedures consistently
- **Communication**: Maintain open communication with team members
- **Documentation**: Keep local documentation current
- **Monitoring**: Watch for early warning signs of issues

### Quality Assurance
- **Self-Review**: Always review your work before submission
- **Peer Review**: Get informal feedback before formal review
- **Testing**: Test thoroughly in development environments
- **Validation**: Use automated validation tools when available

### Continuous Improvement
- **Feedback**: Provide feedback on processes and tools
- **Learning**: Stay current with new features and capabilities
- **Sharing**: Share solutions and lessons learned with team
- **Contributing**: Contribute to documentation and process improvement

This troubleshooting guide is regularly updated based on user feedback and new issues discovered. If you encounter an issue not covered here, please document it and share with the team for inclusion in future updates.