# PCI-DSS Compliance Framework

## Overview
Payment Card Industry Data Security Standard compliance for organizations handling cardholder data.

> **Implementation Note**: This PCI-DSS compliance framework is a specialized example for organizations handling payment card data. Only implement if your organization is subject to PCI-DSS requirements. Adapt the complexity to match your implementation tier:
> - **Tier 1 (Basic)**: Simple guidelines to avoid cardholder data in prompts
> - **Tier 2 (Intermediate)**: PCI-DSS-aware prompt review process with data detection
> - **Tier 3 (Advanced)**: Formal PCI-DSS compliance verification in prompt lifecycle
> - **Tier 4 (Expert)**: Comprehensive PCI-DSS compliance with automated cardholder data detection and protection

## Scope of Application
- Merchants accepting card payments
- Payment processors
- Service providers
- Financial institutions
- Any entity storing, processing, or transmitting cardholder data

## Cardholder Data Elements

### Primary Account Number (PAN)
- 13-19 digit payment card number
- Must be rendered unreadable when stored
- Encryption or tokenization required

### Sensitive Authentication Data
- Full magnetic stripe data
- Card verification codes (CVV/CVC)
- PIN data
- Never store after authorization

## 12 PCI-DSS Requirements

### Build and Maintain Secure Networks
1. **Install and maintain firewall configuration**
   - Network segmentation
   - Firewall rule documentation
   - Regular configuration reviews

2. **Do not use vendor-supplied defaults**
   - Change default passwords
   - Remove unnecessary accounts
   - Disable unused services

### Protect Cardholder Data
3. **Protect stored cardholder data**
   - Data retention policies
   - Secure deletion procedures
   - Encryption of stored data

4. **Encrypt transmission of cardholder data**
   - Strong cryptography protocols
   - Secure key management
   - Network transmission protection

### Maintain Vulnerability Management
5. **Protect systems against malware**
   - Anti-virus software deployment
   - Regular signature updates
   - Malware detection procedures

6. **Develop and maintain secure systems**
   - Patch management processes
   - Security update procedures
   - System hardening standards

### Implement Strong Access Controls
7. **Restrict access by business need-to-know**
   - Role-based access controls
   - Least privilege principle
   - Access approval processes

8. **Identify and authenticate access to system components**
   - Unique user identification
   - Strong authentication methods
   - Multi-factor authentication

9. **Restrict physical access to cardholder data**
   - Physical security controls
   - Visitor management
   - Media handling procedures

### Regularly Monitor and Test Networks
10. **Track and monitor access to network resources**
    - Audit trail implementation
    - Log monitoring procedures
    - Daily log review processes

11. **Regularly test security systems and processes**
    - Vulnerability scanning
    - Penetration testing
    - Security assessment procedures

### Maintain Information Security Policy
12. **Maintain policy that addresses information security**
    - Comprehensive security policies
    - Risk assessment procedures
    - Security awareness training

## Compliance Validation

### Self-Assessment Questionnaire (SAQ)
- SAQ A: Card-not-present merchants
- SAQ B: Imprint machines or standalone terminals
- SAQ C: Payment application systems
- SAQ D: All other merchants

### On-site Assessment
- Qualified Security Assessor (QSA) audit
- Report on Compliance (ROC)
- Attestation of Compliance (AOC)
- Remediation planning

## Compliance Levels

### Level 1
- 6+ million transactions annually
- Quarterly network scans
- Annual on-site assessment

### Level 2
- 1-6 million transactions annually
- Quarterly network scans
- Annual self-assessment

### Level 3
- 20,000-1 million e-commerce transactions
- Quarterly network scans
- Annual self-assessment

### Level 4
- Less than 20,000 e-commerce transactions
- Annual self-assessment
- Quarterly network scans (if applicable)

## Implementation Strategy
1. Scope definition and data flow mapping
2. Gap analysis and risk assessment
3. Remediation planning and prioritization
4. Control implementation and testing
5. Documentation and evidence collection
6. Validation and compliance reporting

## Penalties for Non-Compliance
- Monthly fines ($5,000-$100,000)
- Card replacement costs
- Forensic investigation expenses
- Legal liability exposure
- Reputational damage