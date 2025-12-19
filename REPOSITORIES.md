# Available Repositories

This document provides information about repositories available within the CCPR (Central Code Prompt Repository) ecosystem.

## Current Repository

### ccpr_root
- **URL**: https://github.com/ekuris-repos/ccpr_root
- **Description**: The main Central Code Prompt Repository (CCPR) - a comprehensive, Git-based repository system for centralized AI prompt management, governance, and compliance across enterprise environments
- **Purpose**: Root repository containing the complete CCPR framework including prompts, templates, standards, compliance, governance, and documentation
- **Access**: You are currently working in this repository

## Repository Structure

The `ccpr_root` repository contains:

### `/prompts/`
Organized prompt library by functional category:
- Generation (code generation, content creation, documentation)
- Classification (categorization, sentiment analysis, tagging)
- Transformation (text rephrasing, format conversion, style transformation)
- Summarization (conversation summaries, report condensation)
- Extraction (entity extraction, key point identification, data parsing)

### `/templates/`
Standardized templates for consistency:
- Prompt templates
- Response templates
- Lifecycle templates

### `/standards/`
Domain-specific guidelines and best practices:
- Software development standards
- Networking standards
- Project management standards
- Naming conventions

### `/compliance/`
Comprehensive regulatory framework support:
- Data protection (GDPR, HIPAA, FERPA)
- Financial compliance (PCI-DSS, SOX)
- Security (SOC2, access policies, audit procedures)
- Data handling policies

### `/governance/`
Repository management and quality assurance:
- Contribution guidelines
- Review processes
- Escalation policies
- Prompt lifecycle management
- Forking guide
- Platform setup guides

### `/docs/`
Comprehensive knowledge base:
- CCPR documentation (getting started, user guides, how-to guides, reference docs)
- AI integration patterns
- Shared standards and templates
- Troubleshooting guides

## Departmental Repositories

The CCPR architecture supports departmental customization through forking:

### Creating Department-Specific Repositories
Departments can create their own customized versions of CCPR by:
1. Forking the `ccpr_root` repository
2. Customizing prompts, templates, and standards for their specific needs
3. Maintaining alignment with enterprise governance standards
4. Following the guidance in `/governance/forking_guide.md`

### Example Department Fork Structure
```
ekuris-repos/ccpr_root              # Main enterprise repository
  ├── fork: ccpr_engineering        # Engineering department customization
  ├── fork: ccpr_marketing          # Marketing department customization
  ├── fork: ccpr_healthcare         # Healthcare department customization
  └── fork: ccpr_finance            # Finance department customization
```

## Related Repositories

### Platform-Specific Implementations
The CCPR framework can be deployed on multiple Git platforms:
- **GitHub Enterprise**: Advanced security and compliance features
- **Azure DevOps**: Microsoft ecosystem integration
- **GitLab**: Comprehensive DevOps capabilities
- **Bitbucket**: Atlassian tool integration
- **AWS CodeCommit**: Cloud-native AWS integration
- **Google Cloud Source**: GCP-integrated repositories

## Repository Access

### How to Access
- **Current Repository**: You have access to the `ccpr_root` repository at `/home/runner/work/ccpr_root/ccpr_root`
- **Remote URL**: https://github.com/ekuris-repos/ccpr_root

### Getting Help
- See `README.md` for comprehensive overview
- See `instructions.md` for role-specific guidance
- See `/docs/ccpr/getting-started/quick-start.md` for 5-minute setup guide
- See `/governance/` for contribution and review processes

## Future Repositories

The CCPR ecosystem is designed to grow with organizational needs. Future repositories may include:
- **Knowledge Base Domains**: Additional specialized knowledge bases (as outlined in `/docs/README.md`)
- **Integration Tools**: Repositories for CCPR integration with other systems
- **Custom Workflows**: Organization-specific automation and tooling
- **Community Contributions**: Open-source prompt libraries and templates

## Implementation Tiers

Repositories can be implemented at different tiers based on organizational needs:

### 🥉 Tier 1 - Basic
Essential prompt management with simple structure

### 🥈 Tier 2 - Intermediate
Enhanced governance, standards, and department customization

### 🥇 Tier 3 - Advanced
Full enterprise implementation with comprehensive compliance

### 🏆 Tier 4 - Expert
Innovation, optimization, and advanced analytics

## Questions?

If you have questions about repository access or need to create a new repository:
- Consult `/docs/ccpr/getting-started/` for getting started guides
- Review `/governance/platform_setup.md` for platform-specific setup
- See `/docs/ccpr/how-to/setup-fork.md` for creating department forks
- Contact repository administrators for access requests

---

**Last Updated**: 2025-12-19  
**Repository**: ekuris-repos/ccpr_root
