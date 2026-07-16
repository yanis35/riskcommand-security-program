# Vendor Risk Scorecard

**Phase:** 5 — Vendor Risk Management Program
**Objective:** Consolidated scorecard displaying assessed vendor risk scores, findings, and remediation status across the portfolio
**Review Cadence:** Quarterly board review, monthly update by Security Team

---

## Portfolio Overview

| Metric | Value |
|--------|-------|
| Total Vendors | 31 |
| Annual Vendor Spend | $1.12M |
| Assessed (YTD) | 14 of 31 |
| Critical or High Tier Vendors ^[Tier classifications based on data sensitivity and criticality to business operations, not risk scores.] | 14 |
| Overdue Assessments | 2 |
| Open Remediation Items | 10 |
| Portfolio Risk Score (Weighted Avg) | **27.4 / 100 (Medium)** |

---

## Vendor Scorecard — All Tiers

### Critical Tier (Score 9–10)

| Vendor | Service | Tier Score | Risk Score | Rating | Last Assessed | Next Review | Status |
|--------|---------|:----------:|:----------:|:------:|:-------------:|:-----------:|:------:|
| AWS | Cloud infrastructure | 10 | 63.1 | **Critical** | Q1 2026 | Q2 2026 | ✅ On track |
| Okta | Identity & SSO | 10 | 58.4 | **Critical** | Q1 2026 | Q2 2026 | ⚠️ Remediation |
| Stripe | Payment processing | 10 | 61.2 | **Critical** | Q4 2025 | Q2 2026 | ✅ On track |
| Twilio/SendGrid | Transactional email | 9 | 45.8 | High | Q1 2026 | Q3 2026 | ✅ On track |
| Datadog | Monitoring & SIEM | 9 | 42.1 | High | Q1 2026 | Q3 2026 | ✅ On track |
| Vercel | Web hosting | 9 | 35.6 | Medium | Q1 2026 | Q3 2026 | ✅ On track |

### High Tier (Score 7–8)

| Vendor | Service | Tier Score | Risk Score | Rating | Last Assessed | Next Review | Status |
|--------|---------|:----------:|:----------:|:------:|:-------------:|:-----------:|:------:|
| GitHub | Source code, CI/CD | 8 | 38.2 | Medium | Q1 2026 | Q3 2026 | ✅ On track |
| Zendesk | Customer support | 8 | 41.5 | High | Q4 2025 | Q2 2026 | 🔴 Overdue |
| Rippling | HR, payroll, devices | 8 | 33.0 | Medium | Q1 2026 | Q3 2026 | ✅ On track |
| M365 | Email, office productivity | 7 | 28.4 | Medium | Q1 2026 | Q3 2026 | ✅ On track |
| Confluence | Internal wiki | 7 | 18.6 | Low | Q1 2026 | Q3 2026 | ✅ On track |
| Jira | Project management | 7 | 21.3 | Medium | Q1 2026 | Q3 2026 | ✅ On track |
| Slack | Communication | 7 | 16.5 | Low | Q1 2026 | Q3 2026 | ✅ On track |
| 1Password | Password management | 8 | 30.2 | Medium | Q1 2026 | Q3 2026 | ✅ On track |

### Medium Tier (Score 4–6)

| Vendor | Service | Tier Score | Risk Score | Rating | Last Assessed | Next Review | Status |
|--------|---------|:----------:|:----------:|:------:|:-------------:|:-----------:|:------:|
| HubSpot | CRM | 6 | 18.2 | Low | Q4 2025 | Q2 2026 | 🔴 Overdue |
| Salesforce | Sales | 6 | 20.5 | Medium | — | Q2 2026 | ⏳ Pending |
| Google Analytics | Analytics | 5 | 12.4 | Low | — | Q3 2026 | ⏳ Pending |
| Mailchimp | Marketing email | 5 | 14.1 | Low | Q1 2026 | Q3 2026 | ✅ On track |
| DocuSign | E-signature | 5 | 15.8 | Low | Q1 2026 | Q3 2026 | ✅ On track |
| Zoom | Video conferencing | 5 | 11.3 | Low | — | Q3 2026 | ⏳ Pending |
| Asana | Task management | 4 | 8.5 | Low | — | Q4 2026 | ⏳ Pending |
| Loom | Video messaging | 4 | 7.2 | Low | — | Q4 2026 | ⏳ Pending |
| Notion | Notes & docs | 5 | 10.8 | Low | — | Q3 2026 | ⏳ Pending |
| Figma | Design | 4 | 9.1 | Low | — | Q4 2026 | ⏳ Pending |

### Low Tier (Score 1–3)

| Vendor | Service | Tier Score | Risk Score | Rating | Assessment Type | Status |
|--------|---------|:----------:|:----------:|:------:|:---------------:|:------:|
| Calendly | Scheduling | 2 | 11.7 | Low | Contractual | ✅ Current |
| Typeform | Forms/surveys | 2 | 8.4 | Low | Contractual | ✅ Current |
| Canva | Design | 2 | 6.3 | Low | Contractual | ✅ Current |
| Google Workspace | Email routing | 2 | 5.1 | Low | Contractual | ✅ Current |
| LinkedIn Sales Nav | Sales tool | 1 | 4.8 | Low | Contractual | ✅ Current |
| Zapier | Automation | 2 | 9.5 | Low | Contractual | ✅ Current |
| Clerk/Janitorial | Office services | 1 | 3.2 | Low | Contractual | ✅ Current |

---

## Critical & High Tier — Detailed Findings

### Okta — SIG Score: 2.8 / 5.0 (Deficient)

| Finding | Severity | Status | Target Close |
|---------|----------|:------:|:------------:|
| No Just-In-Time (JIT) provisioning for admin roles — all admins have standing privileges | High | Remediating | Q2 2026 |
| MFA not enforced for support role — break-glass accounts exist without MFA policy | Critical | Remediating | Q2 2026 |
| Session timeout set to 24 hours — exceeds NexPay's 4-hour maximum policy | Medium | Remediating | Q2 2026 |
| No automated de-provisioning integration with NexPay's HRIS | Medium | Planned | Q3 2026 |

### AWS — SIG Score: 4.5 / 5.0 (Effective)

| Finding | Severity | Status | Target Close |
|---------|----------|:------:|:------------:|
| No organization-level SCP restricting root account usage | Low | Open | Q2 2026 |
| CloudTrail log integrity not verified (no log file validation enabled) | Low | Open | Q3 2026 |

### Stripe — SIG Score: 4.2 / 5.0 (Managed)

| Finding | Severity | Status | Target Close |
|---------|----------|:------:|:------------:|
| Shared API keys used in development — not scoped per service | Medium | Open | Q2 2026 |
| No formal quarterly access review process documented | Low | Closed | Q1 2026 |

### Zendesk — SIG Lite Score: 3.1 / 5.0 (At Risk)

| Finding | Severity | Status | Target Close |
|---------|----------|:------:|:------------:|
| Agent accounts not integrated with NexPay SSO — local passwords used | High | Open | Q2 2026 |
| No IP restriction on agent login — accessible from any network | Medium | Open | Q2 2026 |
| Data retention set to indefinite — no automated purge schedule | High | Open | Q3 2026 |

---

## Portfolio Risk Distribution

```
Vendor Risk Ratings (by count)        Vendor Spend at Risk
┌──────────────────────┐              ┌──────────────────────┐
│                      │              │                      │
│  Low        15 (48%) │              │  Critical   $732K    │
│                      │              │  (65% of spend)     │
│  Medium     10 (32%) │              │                      │
│                      │              │  High       $204K   │
│  High        4 (13%) │              │  (18% of spend)     │
│                      │              │                      │
│  Critical    2  (6%) │              │  Medium     $159K   │
│                      │              │  (14% of spend)     │
│  Unacceptable 0  (0%)│              │                      │
│                      │              │  Low         $28K   │
└──────────────────────┘              │  ( 3% of spend)     │
                                      └──────────────────────┘
```

---

## Remediation Tracking

| Vendor | Open Findings | Critical | High | Medium | Low | Days to Oldest |
|--------|:------------:|:--------:|:----:|:------:|:---:|:--------------:|
| Okta | 4 | 1 | 1 | 2 | 0 | 75 |
| Zendesk | 3 | 0 | 2 | 1 | 0 | 45 |
| AWS | 2 | 0 | 0 | 0 | 2 | 30 |
| Stripe | 1 | 0 | 0 | 1 | 0 | 15 |
| HubSpot | 0 | 0 | 0 | 0 | 0 | — |
| **Total** | **10** | **1** | **3** | **4** | **2** | |

---

## Key Risk Indicators

| KRI | Target | Current | Status |
|-----|--------|:-------:|:------:|
| % of Critical vendors assessed on time | 100% | 83% (5 of 6) | ⚠️ Attention |
| % of High vendors assessed on time | 100% | 88% (7 of 8) | ⚠️ Attention |
| Critical findings >30 days open | 0 | 1 | 🔴 Breach |
| High findings >90 days open | 0 | 0 | ✅ Met |
| Vendor risk score trend (quarterly) | Decreasing | +2.1 pts | 🔴 Worsening |

---

## Action Items

| Priority | Action | Owner | Due |
|----------|--------|-------|:---:|
| P1 | Escalate Okta MFA findings — request remediation plan with weekly status | CISO | 7 days |
| P1 | Complete Zendesk re-assessment (overdue) | Security Team | 14 days |
| P2 | Follow up on Stripe shared API key remediation | Security Team | 30 days |
| P2 | Schedule HubSpot self-assessment (overdue) | Vendor Manager | 30 days |
| P3 | Implement automated vendor risk score tracking in GRC tool | Security Team | Q3 2026 |
