# AWS Config Security Compliane Lab
## Overview
This project demonstrates a hands-on AWS security compliance assessment using AWS Config to identify, investigate, remediate, and verify cloud security configuration issues
The lab focused on IAM password security and EC2 security group configurations.
## Objectives
- Configure AWS Config
- Impliment AWS Config managed rules
- Identify non-compliant resources
- Investigate security findings
- Remediate security configuration issues
- Re-evaluate AWS Config rules
- Verify the final compliance status
## AWS Services Used
- AWS Config
- AWS Identity and Access Management (IAM)
- Amazon EC2
- EC2 Security Groups
- Amazon S3
## AWS Config Rules
The following managed rules were configured:
1. `iam-password-policy`
2. `restricted-common-ports`
3. `restricted-ssh`
4. `s3-bucket-public-read-prohibited`
## Initial Security Findings
### 1. IAM Password Policy
The AWS account was initially using the default IAM password policy.
The default configuration included:
- Minimum password length: 8 characters
- Passwords never expired
- Only three of four character types were required
Aws Config therefore reported the account as **NON_COMPLIANT**
### 2. Restricted Common Ports
AWS Config identified an unrestricted inbound RDP rule:
- Protocol: TCP
- Port: 3389
- Source: `0.0.0.0/0`
This exposed RDP to the public internet.
### 3. Restricted SSH
AWS Config identified an unrestricted inbound SSH rule:
- Protocol: TCP
- Port: 22
- Source: `0.0.0.0/0`
This exposed SSH to the public internet.
### 4. S3 Public Read
The `s3-bucket-public-read-prohibited` rule was compliant.
## Remediation
### IAM Password Policy
The default password policy was replaced with a customized security policy.
The following controls were enabled:
- Minimum password length: 14 characters
- Uppercase characters required
- Lowercase characters required
- Numbers required
- Non-alphanumeric characters required
- Password expiration: 90 days
- Password reuse prevention: 24 previous paswwords
- Users allowed to change their own passwords
### RDP Security
The unrestricted RDP rule was changed from:
`0.0.0.0/0`
to a restricted source using the administrator's IP address.
### SSH Security
The unrestricted SSH rule was changed from:
`0.0.0.0/0`
to a restricted source using the administrator's IP address.
## Verification
After remediation, the AWS Config rules were re-evaluated.
### Final Compliance Result
- **4 compliant rules**
- **0 non-compliant rules**
- **5 compliant resources**
- **0 non-compliant resources**

The environment achieved full compliance with all four configured AWS Config rules.
## Security Lessons Learned
This lab demonstrated that:
- AWS Config can continiously evaluate AWS resource configurations.
- Security misconfigurations can exist even when services are functioning normally.
- SSH and RDP should not be unnecessarily exposed to the entire internet.
- Strong IAM password policies improves account security.
- Security remediation should always be followed by re-evaluation.
- Compliance monitoring is an important part of cloud security operations.
# Security Workflow
```text
Configure
   ↓
Detect
   ↓
Investigate
   ↓
Remediate
   ↓
Re-evaluate
   ↓
Verify
```
Project Outcome
The lab successfully demonstrated practical skills in:
- Cloud security
- AWS Config
- IAM security
- Security group hardening
- Security compliance monitoring
- Security remediation
- Configuration assessment

## Evidence / Screenshots

The following screenshots document the key stages and results of the AWS Config security compliance lab

[Initial Compliance Dashboard.png](evidence/01-initial-compliance-dashboard.png)

[Config Rule Initial Status.png](evidence/02-config-rules-initial-status.png)

[IAM Password Policy - Initial.png](evidence/03-iam-password-policy-initial.png)

[RDP 3389 Initial Vulnerability.png](evidence/04-rdp-3389-initial-vulnerability.png)

[SSH 22 Initial Vulnerability.png](evidence/05-ssh-22-initial-vulnerability.png)

[RDP 3389 Remediated.png](evidence/06-rdp-3389-remediated.png)

[SSH 22 Remediated.png](evidence/07-ssh-22-remediated.png)

[IAM Password Policy Remediated.png](evidence/08-iam-password-policy-remediated.png)

[Final Compliance Dashboard](evidence/09-final-compliance-dashboard.png)


Security Disclaimer

This project was performed in an authorized AWS lab environment for cybersecurity learning and portfolio development.

No passwords, access keys, or other sensitive credentials are included in this repository.
