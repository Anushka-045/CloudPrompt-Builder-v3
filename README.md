# ☁️ CloudPrompt Builder
### AI Prompts for Faster AWS Infrastructure

> **Agentic · Adaptive · Production-Ready**  
> Submitted to the [AWS Prompt the Planet Challenge 2026](https://awspromptheplanet.com)

---

## What is CloudPrompt Builder?

CloudPrompt Builder is a structured AI prompt system that turns any AI assistant (Claude, ChatGPT, etc.) into a **virtual AWS security architect**.

Instead of blindly running commands, the AI:
1. **Discovers** the current state of your AWS account
2. **Assesses** gaps against CIS, SOC 2, or PCI-DSS benchmarks
3. **Prioritises** risks by business impact and remediation effort
4. **Recommends** a tiered roadmap — Quick Wins → High Impact → Long-Term
5. **Waits for your approval** before making any changes

No scripts to run. No infrastructure to deploy. Just paste the prompt and go.

---

## 🚀 Quick Start

1. Copy the contents of [`prompt-v3.md`](./prompt-v3.md)
2. Paste it into Claude, ChatGPT, or any capable AI assistant
3. Answer the 8 Step 0 questions when the AI asks
4. Review the risk summary and approve the remediation plan
5. Work through sections 1–9 at your own pace

---

## 📋 What the Prompt Covers

| Section | What It Does |
|---------|-------------|
| **Step 0** | Collects 8 inputs — Account ID, region, budget, compliance target, etc. |
| **Section 0** | Full account discovery: identity, logging, public exposure, encryption |
| **Section 0.6** | 🆕 Security Roadmap Generator — 3-tier prioritised improvement plan |
| **Section 1** | Root hardening + IAM groups, password policy, SCPs |
| **Section 2** | CloudTrail multi-region logging + S3 log storage + CloudWatch alarms |
| **Section 3** | GuardDuty threat detection across all regions |
| **Section 4** | AWS Config compliance rules + intelligent AI-recommended extras |
| **Section 5** | KMS Customer Managed Key for all security data encryption |
| **Section 6** | Security Hub unified posture + standards alignment |
| **Section 7** | VPC security groups, flow logs, NACL hardening |
| **Section 8** | Billing anomaly detection + budget alarms auto-calibrated to your budget |
| **Section 9** | Final security posture report with before/after scores |

---

## 🛡️ Compliance Coverage

| Framework | Coverage |
|-----------|----------|
| CIS AWS Foundations Benchmark Level 1 | ~100% |
| CIS AWS Foundations Benchmark Level 2 | ~85% |
| SOC 2 Type II (Security Trust Service Criteria) | Strong foundation |
| PCI DSS | Significant coverage (logging, encryption, access controls) |

---

## ☁️ AWS Services Used

IAM · CloudTrail · GuardDuty · Security Hub · AWS Config · KMS · S3 · VPC · CloudWatch · SNS · AWS Budgets

---

## 💰 Estimated Monthly Cost

| Service | Cost |
|---------|------|
| GuardDuty | ~$1–$4/month (30-day free trial) |
| AWS Config | ~$2–$8/month |
| Security Hub | ~$0–$5/month (30-day free trial) |
| CloudTrail | First trail free; S3 ~$0.023/GB |
| **Total** | **~$5–$20/month** for a typical small account |

---

## ⚡ Key Features

- **Discovery-first**: never modifies anything without showing you the current state first
- **Safety gates**: `CONFIRM-SCP` and `CONFIRM-OBJECT-LOCK` required before irreversible actions
- **Adaptive**: skips sections already compliant; only remediates actual gaps
- **Dual output**: every step provides Console path + AWS CLI + Terraform HCL
- **Scored results**: Security Maturity Score (0–100), CIS coverage %, risk count — before and after
- **Roadmap generator**: ranks all risks by business impact × remediation effort into 3 tiers

---

## 📁 Repository Structure

```
cloudprompt-builder/
├── README.md               ← You are here
├── prompt-v3.md            ← The full copy-paste prompt (v3, latest)
├── LICENSE                 ← MIT License
└── examples/
    ├── step0-output.md     ← Example: Step 0 discovery output
    ├── risk-summary.md     ← Example: Section 0.5 risk table output
    └── roadmap-output.md   ← Example: Section 0.6 roadmap output
```

---

## 🏆 Well-Architected Alignment

| Pillar | How This Prompt Addresses It |
|--------|------------------------------|
| **Security** | Primary focus — IAM, logging, detection, encryption, network |
| **Operational Excellence** | CloudWatch alarms, Config drift detection, structured runbook |
| **Cost Optimization** | Budget alarms auto-calibrated; security tooling cost estimates provided |
| **Reliability** | Multi-region logging, Config continuous recording, S3 Object Lock |

---

## 📝 Prerequisites

- AWS account with root or IAM Administrator access
- AWS CLI v2 configured (`aws configure`)
- Terraform ≥ 1.5.0 *(optional — prompt adapts output based on your answer)*
- Python 3.9+ with `boto3` *(for discovery scripts)*

---

## 👤 Author

**Anushka Pandey**  
[GitHub](https://github.com/Anushka-045) · [LinkedIn](https://www.linkedin.com/in/anushka-pandey-b8b16b329)

---

*Contributed to the AWS Startups Prompt Library · AWS Prompt the Planet Challenge 2026*
