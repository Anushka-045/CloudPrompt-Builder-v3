# Example Output: Step 0 — Account Discovery

> **Scenario:** Fresh AWS account, 3 months old, one developer, no compliance framework yet.  
> *Account ID and region are fictional for illustration.*

---

## AI Response to Step 0 Questions

The AI asked:

> Before I begin, I need a few details about your AWS account:
> 
> 1. AWS Account ID (12-digit)?
> 2. Primary AWS region?
> 3. Account type — Standalone or part of AWS Organizations?
> 4. Environment — Dev / Staging / Production / Mixed?
> 5. Monthly AWS budget?
> 6. Target compliance framework — CIS Level 1, CIS Level 2, PCI-DSS, SOC 2, or None?
> 7. Do you use Terraform?
> 8. Any existing security tooling already enabled?

**User answered:**
```
1. 123456789012
2. ap-south-1
3. Standalone
4. Production
5. $150/month
6. CIS Level 1
7. Yes
8. None
```

---

## Section 0.1 — Identity Inventory

```
aws iam generate-credential-report
aws iam get-credential-report --query 'Content' --output text | base64 -d
```

**Findings:**

| User | MFA Enabled | Last Activity | Admin Policy | Flag |
|------|-------------|---------------|--------------|------|
| root | ❌ No | 14 days ago | N/A | 🔴 CRITICAL |
| dev-user | ❌ No | 2 days ago | AdministratorAccess | 🔴 CRITICAL |
| deploy-ci | ✅ Yes | Today | PowerUserAccess | ✅ OK |

- Root access keys: **Active** 🔴 CRITICAL — root should never have active access keys
- Root MFA: **Not enabled** 🔴 CRITICAL
- Password policy: **Not configured** 🟠 HIGH

---

## Section 0.2 — Logging & Detection Gaps

| Service | Status | Details |
|---------|--------|---------|
| CloudTrail | ❌ Not enabled | No trails found in ap-south-1 |
| GuardDuty | ❌ Not enabled | No detectors found |
| AWS Config | ❌ Not enabled | No recorders found |
| Security Hub | ❌ Not enabled | — |
| VPC Flow Logs | ❌ Not enabled | Default VPC has no flow logs |

---

## Section 0.3 — Public Exposure Scan

| Resource | Issue | Severity |
|----------|-------|----------|
| S3: my-app-assets | Public read ACL enabled | 🔴 CRITICAL |
| S3: dev-backups-2024 | No public access block | 🟠 HIGH |
| SG: sg-0abc123 | Port 22 open to 0.0.0.0/0 | 🔴 CRITICAL |
| SG: sg-0def456 | Port 3389 open to 0.0.0.0/0 | 🔴 CRITICAL |

---

## Section 0.4 — Encryption Coverage

| Resource | Encrypted | Details |
|----------|-----------|---------|
| EBS default encryption | ❌ Off | New volumes unencrypted by default |
| RDS instances | ✅ N/A | No RDS found |
| S3 default encryption | ❌ Off | Buckets use no default encryption |
| KMS CMK | ❌ None | Only AWS-managed keys in use |

---

## Section 0.5 — Risk Summary

| Finding | Severity | CIS Control | Recommended Fix |
|---------|----------|-------------|-----------------|
| Root MFA not enabled | 🔴 Critical | CIS 1.5 | Enable virtual MFA on root immediately |
| Root access keys active | 🔴 Critical | CIS 1.4 | Delete root access keys |
| CloudTrail not enabled | 🔴 Critical | CIS 3.1 | Create multi-region trail |
| GuardDuty not enabled | 🔴 Critical | CIS 4.1 | Enable in all regions |
| S3 bucket publicly readable | 🔴 Critical | CIS 2.1.5 | Enable block public access |
| SSH open to 0.0.0.0/0 | 🔴 Critical | CIS 5.2 | Restrict to known IP range |
| No MFA on IAM users | 🟠 High | CIS 1.10 | Enforce MFA for all users |
| EBS encryption not default | 🟠 High | CIS 2.2.1 | Enable account-level default encryption |
| No password policy | 🟠 High | CIS 1.8 | Apply CIS Level 1 policy |
| No VPC Flow Logs | 🟡 Medium | CIS 3.9 | Enable on default VPC |

**Scores:**
- 🔢 Security Maturity Score: **18 / 100**
- 📊 CIS Level 1 Coverage: **12%**
- 📊 CIS Level 2 Coverage: **8%**
- 🚨 Critical Risks: **6**
- ⏱️ Estimated Remediation Time: **~75 minutes**

> **AI:** I've completed the discovery phase. The account has 6 critical findings, most of which can be resolved quickly. Shall I proceed with the remediation plan? Type **APPROVE** to begin Section 1.
