# Vendor Tiering Classification

**Phase:** 5 — Vendor Risk Management Program
**Objective:** Classify all 30+ vendors into risk tiers based on data access, system criticality, and regulatory impact
**Framework:** NIST SP 800-161 (Supply Chain Risk Management), ISO 27001:2022 A.5.19–A.5.22

---

## Tiering Methodology

Vendors are classified using a composite score based on 4 dimensions:

| Dimension | Weight | Scoring (1–10) |
|-----------|--------|----------------|
| Data Access Level | 40% | L1=1, L2=3, L3=6, L4=10 |
| System Criticality | 30% | Non-critical=1, T3=3, T2=6, T1=10 |
| Regulatory Impact | 20% | None=1, Low=3, Medium=6, High=10 |
| Financial Exposure | 10% | <$10K/yr=1, $10-100K=3, $100K-1M=6, >$1M=10 |

**Score:** 0–3 = Low, 4–6 = Medium, 7–8 = High, 9–10 = Critical

---

## Complete Vendor Register (31 Vendors)

### Tier 1 — Critical (Score 9–10)

| Vendor | Service | Data Access | Tier Score | Annual Spend |
|--------|---------|-------------|------------|--------------|
| AWS | Cloud infrastructure | L4 | 10 | $480,000 |
| Okta | Identity & SSO | L4 | 10 | $36,000 |
| Stripe | Payment processing | L4 | 10 | $120,000 |
| Twilio/SendGrid | Transactional email | L3 | 9 | $24,000 |
| Datadog | Monitoring & SIEM | L3 | 9 | $60,000 |
| Vercel | Web hosting | L3 | 9 | $12,000 |
| **Total Critical** | **6 vendors** | | | **$732,000** |

### Tier 2 — High (Score 7–8)

| Vendor | Service | Data Access | Tier Score | Annual Spend |
|--------|---------|-------------|------------|--------------|
| GitHub | Source code, CI/CD | L3 | 8 | $24,000 |
| Zendesk | Customer support | L3 | 8 | $18,000 |
| Rippling | HR, payroll, devices | L3 | 8 | $60,000 |
| M365 | Email, office productivity | L3 | 7 | $48,000 |
| Confluence | Internal wiki | L2 | 7 | $6,000 |
| Jira | Project management | L2 | 7 | $12,000 |
| Slack | Communication | L2 | 7 | $30,000 |
| 1Password | Password management | L3 | 8 | $6,000 |
| **Total High** | **8 vendors** | | | **$204,000** |

### Tier 3 — Medium (Score 4–6)

| Vendor | Service | Data Access | Tier Score | Annual Spend |
|--------|---------|-------------|------------|--------------|
| HubSpot | CRM | L2 | 6 | $36,000 |
| Salesforce | Sales | L2 | 6 | $60,000 |
| Google Analytics | Analytics | L2 | 5 | $0 (free) |
| Mailchimp | Marketing email | L2 | 5 | $12,000 |
| DocuSign | E-signature | L2 | 5 | $6,000 |
| Zoom | Video conferencing | L2 | 5 | $18,000 |
| Asana | Task management | L1 | 4 | $12,000 |
| Loom | Video messaging | L1 | 4 | $3,000 |
| Notion | Notes & docs | L2 | 5 | $6,000 |
| Figma | Design | L1 | 4 | $6,000 |
| **Total Medium** | **10 vendors** | | | **$159,000** |

### Tier 4 — Low (Score 1–3)

| Vendor | Service | Data Access | Tier Score | Annual Spend |
|--------|---------|-------------|------------|--------------|
| Calendly | Scheduling | L1 | 2 | $2,000 |
| Typeform | Forms/surveys | L1 | 2 | $1,000 |
| Canva | Design | L1 | 2 | $2,000 |
| Google Workspace (non-prof) | Email routing | L1 | 2 | $0 |
| LinkedIn Sales Nav | Sales tool | L1 | 1 | $8,000 |
| Zapier | Automation | L1 | 2 | $3,000 |
| Clerk/Janitorial | Office services | None | 1 | $12,000 |
| **Total Low** | **7 vendors** | | | **$28,000** |

---

## Tier Distribution

```
Tier Distribution by Count        Tier Distribution by Spend
┌──────────────────┐              ┌──────────────────┐
│                  │              │                  │
│  Low    7 (23%)  │              │  Critical        │
│                  │              │  22%             │
│  Medium 10 (32%) │              │  ($732K)         │
│                  │              │                  │
│  High   8 (26%)  │              │  High  6%        │
│                  │              │  ($204K)         │
│  Critical 6 (19%)│              │                  │
│                  │              │  Medium 5%       │
└──────────────────┘              │  ($159K)         │
                                  │                  │
  Total: 31 vendors               │  Low   1%        │
  Total spend: $1.12M             │  ($28K)          │
                                  └──────────────────┘
```

---

## Assessment Requirements by Tier

| Tier | Assessment Type | Frequency | Documentation |
|------|----------------|-----------|---------------|
| Critical | Full SIG + SOC 2 Type II + Pentest Results + On-site | Annual | All docs reviewed by CISO |
| High | SIG Lite + SOC 2 Report + Attestation | Annual | Reviewed by Security Team |
| Medium | Self-Assessment Questionnaire | Annual | Self-certified, spot-checked |
| Low | Contractual Clauses Only | At contract signature | Reviewed by Legal |

---

## Risk Appetite

- **Critical tier vendors:** Risk appetite is LOW — must score "Effective" or better on SIG controls. Any deficiency must be remediated or accepted by CISO.
- **High tier vendors:** Risk appetite is MODERATE — major deficiencies must have remediation plans within 90 days.
- **Medium tier vendors:** Risk appetite is HIGH — self-assessed, periodic spot checks.
- **Low tier vendors:** Risk appetite is VERY HIGH — contractual protections only.

---

## Tier Review Cadence

| Trigger | Action |
|---------|--------|
| Annual | Full tier review for all vendors |
| Contract renewal | Re-assess tier and update assessment |
| Security incident | Immediate tier review for affected vendor |
| New vendor onboarding | Classify tier before contract execution |
| Vendor M&A or acquisition | Immediate re-assessment |
| Change in service scope | Re-assess tier and update assessment |
