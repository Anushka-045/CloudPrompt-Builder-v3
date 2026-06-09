# Example Output: Section 0.6 — Security Roadmap Generator

> **Scenario:** Continuing from the discovery in `step0-output.md`  
> The AI has assessed all findings and is now acting as a virtual security architect.

---

## AI-Generated Security Roadmap

Based on my analysis of your account, I've ranked all findings by **Business Impact** (what an attacker could do if this is exploited) and **Remediation Effort** (time + complexity to fix). Here is your prioritised improvement roadmap:

---

### 🟢 TIER 1 — Quick Wins *(under 30 minutes, high impact)*

| # | Risk | Business Impact | Effort | Timeline |
|---|------|----------------|--------|----------|
| 1 | Root access keys active | Full account takeover if leaked | 2 min | **Do this now** |
| 2 | Root MFA not enabled | Root account unprotected | 5 min | **Do this now** |
| 3 | S3 bucket public read (my-app-assets) | Data exposure / exfiltration | 3 min | **Do this now** |
| 4 | SSH open to 0.0.0.0/0 (2 SGs) | Direct server compromise | 5 min | **Do this now** |
| 5 | Enable EBS default encryption | All new volumes unencrypted | 2 min | Today |
| 6 | Enable S3 default encryption | New objects unencrypted | 2 min | Today |

---

### 🟡 TIER 2 — High Impact Fixes *(significant risk reduction, medium effort)*

| # | Risk | Business Impact | Effort | Timeline |
|---|------|----------------|--------|----------|
| 7 | CloudTrail not enabled | No audit trail — blind to attacks | 15 min | Today |
| 8 | GuardDuty not enabled | No threat detection | 10 min | Today |
| 9 | No IAM password policy | Weak credentials | 5 min | Today |
| 10 | No MFA on IAM users | Account takeover on credential leak | 20 min | This week |
| 11 | AWS Config not enabled | No compliance drift detection | 20 min | This week |
| 12 | No VPC Flow Logs | Blind to network-level attacks | 10 min | This week |

---

### 🔵 TIER 3 — Long-Term Improvements *(architecture-level, strategic)*

| # | Risk | Business Impact | Effort | Timeline |
|---|------|----------------|--------|----------|
| 13 | No KMS CMK | Limited control over encryption keys | 30 min | This month |
| 14 | Security Hub not enabled | No unified compliance view | 20 min | This month |
| 15 | No SCPs (future org expansion) | No guardrails if multi-account later | 1 hr | Next quarter |
| 16 | Long-lived IAM user credentials | Replace with IAM Identity Center | 2–4 hrs | Next quarter |

---

### ⚠️ Dependency Sequencing Constraints

The AI flagged these sequencing requirements — these steps **must** happen in order:

```
1. KMS CMK (Section 5) 
   └─► CloudTrail S3 encryption (Section 2.3) — needs the key ARN
       └─► S3 bucket creation — needs encryption configured first

2. SNS "security-alerts" topic
   └─► CloudWatch Alarms (Section 2.4) — need the topic ARN
   └─► GuardDuty findings routing (Section 3.3) — need the topic ARN
   └─► Security Hub routing (Section 6.3) — need the topic ARN

3. CloudTrail enabled (Section 2)
   └─► KMS key policy with EncryptionContext — CloudTrail needs to exist
       to generate the correct ARN pattern for the condition
```

> **AI recommendation:** Start with Tier 1 items 1–4 right now (root keys + MFA + S3 + SSH). These take under 15 minutes total and eliminate your highest-probability attack vectors. Then work through Tier 2 in order. Shall I begin Section 1?
