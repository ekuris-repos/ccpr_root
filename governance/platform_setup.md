# CCPR Platform Setup Guide

## Overview
This guide provides comprehensive setup instructions for implementing the Central Controlled Prompt Repository (CCPR) across different Git-compatible platforms, enabling organizations to choose the platform that best fits their infrastructure and requirements.

> **Implementation Note**: This platform setup guide represents a comprehensive example for enterprise-grade implementations. Organizations should adapt the complexity and requirements to match their implementation tier:
> - **Tier 1 (Basic)**: Simple Git repository with basic folder structure
> - **Tier 2 (Intermediate)**: Hosted Git service with branch protection and basic workflows
> - **Tier 3 (Advanced)**: Enterprise Git platform with automated workflows and integration
> - **Tier 4 (Expert)**: Multi-platform federation with comprehensive security and compliance integration

## Platform Selection Criteria

### Technical Requirements
- Git version control support
- Branch protection capabilities
- Access control and permissions
- Pull/merge request workflows
- Automated workflow support
- API access for integrations

### Enterprise Requirements
- Security and compliance features
- Audit and logging capabilities
- Integration with existing tools
- Scalability and performance
- Support and maintenance
- Cost considerations

### Compliance Requirements
- Data residency controls
- Encryption capabilities
- Audit trail maintenance
- Access logging and monitoring
- Backup and recovery
- Regulatory compliance support

## Platform-Specific Setup Instructions

## 1. GitHub Enterprise (GHE)

### Prerequisites
- GitHub Enterprise license
- Domain configuration
- SSL certificate setup
- LDAP/SAML integration (optional)

### Initial Setup

#### 1.1 Organization Configuration
```bash
# Create organization (via web interface)
# Navigate to GitHub Enterprise → Organizations → New Organization
Organization Name: [YourCompany]-CCPR
Billing Email: [admin@yourcompany.com]
Plan: Enterprise
```

#### 1.2 Repository Creation
```bash
# Create main CCPR repository
Repository Name: ccpr_root
Visibility: Private (Internal)
Initialize with: README, .gitignore (Python), License (MIT)
```

#### 1.3 Access Control Setup
```yaml
# .github/CODEOWNERS
# Global owners
* @ccpr-administrators @compliance-team

# Specific directory owners
/prompts/ @content-creators @prompt-reviewers
/compliance/ @compliance-team @legal-team
/governance/ @governance-team @administrators
/standards/ @standards-committee @domain-experts
```

#### 1.4 Branch Protection Rules
```yaml
# Branch: main
Settings:
  - Require pull request reviews before merging
  - Required approving reviews: 2
  - Dismiss stale PR approvals when new commits are pushed
  - Require review from code owners
  - Require status checks to pass before merging
  - Require branches to be up to date before merging
  - Include administrators in restrictions
```

#### 1.5 Automated Workflows
```yaml
# .github/workflows/ccpr-validation.yml
name: CCPR Validation
on:
  pull_request:
    branches: [ main ]
  push:
    branches: [ main ]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Validate Templates
        run: |
          # Template compliance validation
          python scripts/validate_templates.py
      - name: Compliance Check
        run: |
          # Compliance requirement validation
          python scripts/compliance_check.py
      - name: Quality Assessment
        run: |
          # Quality metrics evaluation
          python scripts/quality_check.py
```

### Security Configuration

#### 1.6 Security Settings
- Enable dependency vulnerability alerts
- Configure secret scanning
- Enable code scanning (CodeQL)
- Set up security advisories
- Configure two-factor authentication enforcement

#### 1.7 Integration Setup
```bash
# Integrate with LDAP/Active Directory
# Admin Settings → Authentication → LDAP
LDAP Host: ldap.yourcompany.com
Search User: cn=github,ou=service,dc=yourcompany,dc=com
User Search Base: ou=users,dc=yourcompany,dc=com
```

## 2. Azure DevOps (ADO)

### Prerequisites
- Azure DevOps Services or Server license
- Azure Active Directory integration
- Project collection configuration

### Initial Setup

#### 2.1 Project Creation
```bash
# Via Azure DevOps web interface
Organization: https://dev.azure.com/yourcompany
Project Name: CCPR-Central
Visibility: Private
Work Item Process: Agile
Version Control: Git
```

#### 2.2 Repository Configuration
```bash
# Create repository
Repository Name: ccpr_root
Initialize with: README.md
Add .gitignore: Python
```

#### 2.3 Branch Policies
```json
{
  "type": "Microsoft.VisualStudio.Services.Git.Repository",
  "settings": {
    "defaultBranch": "refs/heads/main",
    "policies": [
      {
        "type": "RequirePullRequestReview",
        "minimumApproverCount": 2,
        "creatorVoteCounts": false,
        "allowDownvotes": true,
        "resetOnSourcePush": true
      },
      {
        "type": "RequireUpToDate",
        "enabled": true
      },
      {
        "type": "RequireCommentResolution",
        "enabled": true
      }
    ]
  }
}
```

#### 2.4 Build Pipeline
```yaml
# azure-pipelines.yml
trigger:
  branches:
    include:
      - main
      - feature/*
      - review/*

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Validation
  jobs:
  - job: TemplateValidation
    steps:
    - task: UsePythonVersion@0
      inputs:
        versionSpec: '3.9'
    - script: |
        pip install -r requirements.txt
        python scripts/validate_ccpr.py
      displayName: 'CCPR Validation'

- stage: Compliance
  jobs:
  - job: ComplianceCheck
    steps:
    - script: |
        python scripts/compliance_validation.py
      displayName: 'Compliance Validation'
```

#### 2.5 Security Configuration
```bash
# Security settings
Project Settings → Repositories → Security
- Contribute: Allow for Content-Creators group
- Create Branch: Allow for Content-Creators group
- Force Push: Deny for all except Administrators
- Manage Permissions: Allow for Administrators only
```

## 3. GitLab

### Prerequisites
- GitLab license (CE, EE, or GitLab.com)
- Runner configuration
- LDAP/SAML setup (optional)

### Initial Setup

#### 3.1 Group and Project Creation
```bash
# Create group
Group Name: ccpr-organization
Visibility Level: Private
Description: Central Controlled Prompt Repository Organization
```

```bash
# Create project
Project Name: ccpr_root
Project Path: ccpr-organization/ccpr_root
Visibility Level: Private
Initialize with README: Yes
```

#### 3.2 Branch Protection
```yaml
# Project Settings → Repository → Push Rules
Branch Name Pattern: main
Allowed to push: Maintainers
Allowed to merge: Maintainers
Allowed to force push: No one
Required approvals: 2
Reset approvals on push: Yes
```

#### 3.3 CI/CD Pipeline
```yaml
# .gitlab-ci.yml
stages:
  - validate
  - compliance
  - quality

variables:
  PIP_CACHE_DIR: "$CI_PROJECT_DIR/.cache/pip"

cache:
  paths:
    - .cache/pip/
    - venv/

before_script:
  - python -V
  - pip install virtualenv
  - virtualenv venv
  - source venv/bin/activate
  - pip install -r requirements.txt

template_validation:
  stage: validate
  script:
    - python scripts/validate_templates.py
  only:
    - merge_requests
    - main

compliance_check:
  stage: compliance
  script:
    - python scripts/compliance_check.py
  only:
    - merge_requests
    - main

quality_assessment:
  stage: quality
  script:
    - python scripts/quality_metrics.py
  artifacts:
    reports:
      junit: quality-report.xml
  only:
    - merge_requests
    - main
```

#### 3.4 Access Control
```bash
# Project Settings → Members
Role Assignments:
- Administrators: Owner
- Content-Creators: Developer
- Reviewers: Maintainer
- Compliance-Team: Maintainer
- General-Users: Reporter
```

## 4. Bitbucket

### Prerequisites
- Bitbucket license (Cloud or Server)
- Jira integration setup
- User directory integration

### Initial Setup

#### 4.1 Workspace and Repository
```bash
# Create workspace
Workspace Name: ccpr-workspace
Workspace ID: ccpr-org
```

```bash
# Create repository
Repository Name: ccpr_root
Access Level: Private
Include README: Yes
Include .gitignore: Python
```

#### 4.2 Branch Permissions
```json
{
  "pattern": "main",
  "users": [],
  "groups": ["administrators"],
  "type": "require_approvals_to_merge",
  "value": 2
}
```

#### 4.3 Pipeline Configuration
```yaml
# bitbucket-pipelines.yml
image: python:3.9

pipelines:
  default:
    - step:
        name: CCPR Validation
        caches:
          - pip
        script:
          - pip install -r requirements.txt
          - python scripts/validate_ccpr.py
  
  pull-requests:
    '**':
      - step:
          name: Template Validation
          script:
            - python scripts/validate_templates.py
      - step:
          name: Compliance Check
          script:
            - python scripts/compliance_check.py
```

## 5. AWS CodeCommit

### Prerequisites
- AWS account with appropriate permissions
- IAM user/role configuration
- AWS CLI setup

### Initial Setup

#### 5.1 Repository Creation
```bash
# Using AWS CLI
aws codecommit create-repository \
    --repository-name ccpr_root \
    --repository-description "Central Controlled Prompt Repository"
```

#### 5.2 IAM Policy Configuration
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::ACCOUNT:group/CCPR-ContentCreators"
      },
      "Action": [
        "codecommit:BatchGet*",
        "codecommit:Get*",
        "codecommit:Describe*",
        "codecommit:List*",
        "codecommit:GitPull",
        "codecommit:GitPush"
      ],
      "Resource": "arn:aws:codecommit:REGION:ACCOUNT:ccpr_root"
    }
  ]
}
```

#### 5.3 CodeBuild Integration
```yaml
# buildspec.yml
version: 0.2

phases:
  install:
    runtime-versions:
      python: 3.9
  pre_build:
    commands:
      - pip install -r requirements.txt
  build:
    commands:
      - python scripts/validate_ccpr.py
      - python scripts/compliance_check.py
  post_build:
    commands:
      - echo Build completed
```

## 6. Google Cloud Source Repositories

### Prerequisites
- Google Cloud Platform account
- Project setup with appropriate APIs enabled
- IAM configuration

### Initial Setup

#### 6.1 Repository Creation
```bash
# Using gcloud CLI
gcloud source repos create ccpr_root
gcloud source repos clone ccpr_root
```

#### 6.2 IAM Configuration
```bash
# Grant access to teams
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="group:ccpr-content-creators@yourcompany.com" \
    --role="roles/source.writer"

gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="group:ccpr-administrators@yourcompany.com" \
    --role="roles/source.admin"
```

#### 6.3 Cloud Build Integration
```yaml
# cloudbuild.yaml
steps:
  - name: 'python:3.9'
    entrypoint: 'pip'
    args: ['install', '-r', 'requirements.txt']
  
  - name: 'python:3.9'
    entrypoint: 'python'
    args: ['scripts/validate_ccpr.py']
  
  - name: 'python:3.9'
    entrypoint: 'python'
    args: ['scripts/compliance_check.py']

triggers:
  - github:
      owner: 'your-organization'
      name: 'ccpr_root'
      push:
        branch: '^main$'
```

## Common Configuration Elements

### Required Scripts

#### Template Validation Script
```python
# scripts/validate_templates.py
import os
import yaml
from pathlib import Path

def validate_prompt_templates():
    """Validate all prompt files against template requirements"""
    prompt_dirs = ['prompts/generation', 'prompts/classification', 
                   'prompts/transformation', 'prompts/summarization', 
                   'prompts/extraction']
    
    for prompt_dir in prompt_dirs:
        if os.path.exists(prompt_dir):
            for file_path in Path(prompt_dir).rglob('*.md'):
                validate_single_template(file_path)

def validate_single_template(file_path):
    """Validate individual template compliance"""
    with open(file_path, 'r') as f:
        content = f.read()
    
    # Check for required sections
    required_sections = ['# Purpose', '## Input Parameters', 
                        '## Example Usage', '## Output Format']
    
    for section in required_sections:
        if section not in content:
            raise ValueError(f"Missing required section '{section}' in {file_path}")

if __name__ == "__main__":
    validate_prompt_templates()
    print("All templates validated successfully")
```

#### Compliance Check Script
```python
# scripts/compliance_check.py
import os
import re
from pathlib import Path

def check_compliance_requirements():
    """Validate compliance requirements across all prompts"""
    compliance_patterns = {
        'PII': r'\b(ssn|social security|credit card|phone number)\b',
        'PHI': r'\b(patient|medical record|diagnosis|treatment)\b',
        'Financial': r'\b(account number|routing number|payment)\b'
    }
    
    for file_path in Path('prompts').rglob('*.md'):
        check_file_compliance(file_path, compliance_patterns)

def check_file_compliance(file_path, patterns):
    """Check individual file for compliance issues"""
    with open(file_path, 'r') as f:
        content = f.read().lower()
    
    for category, pattern in patterns.items():
        if re.search(pattern, content):
            print(f"Compliance review required for {file_path}: {category} detected")

if __name__ == "__main__":
    check_compliance_requirements()
    print("Compliance check completed")
```

## Platform Migration

### Migration Between Platforms
1. **Export Repository**: Create complete backup including history
2. **Platform Setup**: Configure new platform per guidelines above
3. **Import Repository**: Restore with full history preservation
4. **Access Migration**: Transfer user accounts and permissions
5. **Integration Update**: Reconfigure workflows and integrations
6. **Validation**: Verify all features work correctly

### Migration Checklist
- [ ] Repository content and history
- [ ] Branch protection rules
- [ ] Access control and permissions
- [ ] Automated workflows/pipelines
- [ ] Integration configurations
- [ ] Documentation updates
- [ ] User training and communication

## Best Practices

### Security
- Enable two-factor authentication
- Regular access reviews
- Audit logging configuration
- Secret management integration
- Vulnerability scanning setup

### Performance
- Repository size monitoring
- Large file management
- Clone optimization
- Search indexing
- Backup strategies

### Maintenance
- Regular platform updates
- Performance monitoring
- Capacity planning
- Disaster recovery testing
- Documentation maintenance

## Support and Resources

### Platform-Specific Documentation
- GitHub Enterprise: https://docs.github.com/enterprise
- Azure DevOps: https://docs.microsoft.com/azure/devops
- GitLab: https://docs.gitlab.com
- Bitbucket: https://confluence.atlassian.com/bitbucket
- AWS CodeCommit: https://docs.aws.amazon.com/codecommit
- Google Cloud: https://cloud.google.com/source-repositories/docs

### Community Resources
- Platform-specific forums and communities
- Best practice sharing groups
- User conferences and training
- Professional services and support