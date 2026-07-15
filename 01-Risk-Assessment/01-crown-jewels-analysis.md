# Crown Jewels Analysis

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Objective:** Identify, classify, and prioritize the organization's most valuable and sensitive assets
**Frameworks:** NIST SP 800-53 (RA-2), ISO 27001 (A.8.2.1), CIA Triad

---

## Methodology

Crown jewels are assets whose compromise would cause severe business impact — regulatory fines, revenue loss, reputational damage, or operational shutdown. Each asset is evaluated across:

- **Confidentiality** — data classification level, regulatory implications of exposure
- **Integrity** — financial/operational impact of unauthorized modification
- **Availability** — revenue/customer impact of downtime
- **Dependencies** — systems and processes that rely on this asset
- **Regulatory** — compliance obligations tied to this asset (PCI DSS, SOC 2, GDPR)

---

## Crown Jewels Register

### Tier 1 — Critical (Compromise = existential threat)

| # | Asset | Owner | CIA Rating | Regulatory | Notes |
|---|-------|-------|------------|------------|-------|
| CJ-001 | Customer PII Database (PostgreSQL) | CTO | C: High, I: High, A: High | GDPR, CCPA, SOC 2 | 1.2M user records including SSNs, bank accounts, KYC docs |
| CJ-002 | Payment Processing Key Vault | CFO | C: Critical, I: Critical, A: High | PCI DSS, SOC 2 | HSMs, API signing keys, TLS private keys, tokenization secrets |
| CJ-003 | Core Transaction Engine | CTO | C: Medium, I: Critical, A: Critical | PCI DSS, SOC 2 | Processes $8M/month in transaction volume |
| CJ-004 | Source Code Repository | VP Eng | C: High, I: High, A: Medium | IP Protection | Proprietary ML fraud detection models, payment integration code |

### Tier 2 — High (Compromise = significant business disruption)

| # | Asset | Owner | CIA Rating | Regulatory | Notes |
|---|-------|-------|------------|------------|-------|
| CJ-005 | AWS Production Environment | CTO | C: High, I: High, A: Critical | SOC 2 | 200+ EC2 instances, RDS clusters, EKS clusters |
| CJ-006 | ML Fraud Detection Models | VP Eng | C: High, I: Critical, A: High | IP Protection | Trained on 5 years of transaction data; model theft = competitive advantage lost |
| CJ-007 | Employee Credentials & SSO | CTO | C: Critical, I: High, A: High | SOC 2 | 200 employees, Okta tenant, privileged access to all systems |
| CJ-008 | Corporate Email System | CTO | C: High, I: High, A: High | SOC 2, BEC risk | M365 tenant, board communications, customer contracts |

### Tier 3 — Moderate (Compromise = operational impact)

| # | Asset | Owner | CIA Rating | Regulatory | Notes |
|---|-------|-------|------------|------------|-------|
| CJ-009 | AWS S3 Data Lake | CTO | C: High, I: Medium, A: Medium | SOC 2 | Historical transaction data, analytics outputs |
| CJ-010 | Internal Financial Systems | CFO | C: High, I: Critical, A: High | SOC 2, GAAP | QuickBooks, payroll, AP automation |
| CJ-011 | Customer Support Platform | VP CS | C: High, I: Medium, A: Medium | SOC 2 | Zendesk with PII exposure |
| CJ-012 | Corporate Network Infrastructure | CTO | C: Low, I: Medium, A: High | SOC 2 | SD-WAN, firewalls, VPN, wireless |

---

## Dependency Map

```
Customer PII Database (CJ-001)
├── Depends on: AWS RDS, Vault (CJ-002), Production Environment (CJ-005)
├── Used by: Transaction Engine (CJ-003), Support Platform (CJ-011)
└── Regulated by: GDPR, CCPA, SOC 2

Payment Processing Key Vault (CJ-002)
├── Depends on: AWS KMS, HSM appliance
├── Used by: Transaction Engine (CJ-003), all API services
└── Regulated by: PCI DSS

Core Transaction Engine (CJ-003)
├── Depends on: PII DB (CJ-001), Key Vault (CJ-002), ML Models (CJ-006)
├── Used by: All customer-facing applications
└── Generates: 100% of company revenue
```

---

## Criticality Scoring Matrix

| Score | Label | Definition |
|-------|-------|------------|
| 9–10 | Critical | Compromise threatens company survival |
| 7–8 | High | Compromise causes major financial/reputational damage |
| 5–6 | Moderate | Compromise causes operational disruption |
| 3–4 | Low | Compromise causes minor inconvenience |
| 1–2 | Minimal | Compromise has negligible impact |

---

## Key Findings

1. **Concentration risk:** CJ-001, CJ-002, and CJ-003 all reside in the same AWS account with no account-level isolation
2. **Key management gap:** No hardware security module (HSM) — keys stored in software Vault with no audit of access
3. **ML model exposure:** Fraud detection models are not access-controlled at the file level; any engineer with S3 access can exfiltrate
4. **No data classification labels:** No automated or manual data classification applied to any crown jewel asset

---

## Immediate Actions

| Priority | Action | Owner | Timeline |
|----------|--------|-------|----------|
| P1 | Isolate production into separate AWS accounts (prod, staging, dev) | CTO | Month 1 |
| P2 | Deploy HSM for payment key storage | CTO | Month 2 |
| P3 | Implement S3 bucket access controls + encryption at rest for ML models | VP Eng | Month 1 |
| P4 | Deploy data classification tool (e.g., Spirion, Titus) | CISO | Month 3 |
