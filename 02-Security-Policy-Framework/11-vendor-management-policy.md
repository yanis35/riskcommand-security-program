# Vendor Management Policy

**Document ID:** POL-10
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CISO
**Review Cycle:** Annual

---

## 1. Purpose

Define requirements for assessing, selecting, monitoring, and off-boarding third-party vendors who access, process, or store NexPay data.

---

## 2. Scope

All vendors, service providers, contractors, and business partners with access to NexPay systems or data. Applies to new engagements and existing vendor reviews.

---

## 3. Vendor Tiering

| Tier | Definition | Examples | Assessment Requirements |
|------|------------|----------|------------------------|
| Critical | Access to L4 data or critical infrastructure | Cloud provider, payment processor, data center, SIEM vendor | Full SIG questionnaire + SOC 2 Type II report review + pentest results + on-site visit |
| High | Access to L3 data or production systems | HR system, CRM, monitoring tools, CDN | SIG Lite + SOC 2 report + security attestation |
| Medium | Access to L2 data or internal tools | Office productivity, project management, marketing tools | Self-assessment questionnaire |
| Low | No data access, peripheral services | Office supplies, cleaning, catering | Contractual clauses only |

---

## 4. Assessment Process

### 4.1 Onboarding
- All vendors must complete a Security Assessment before contract execution.
- Assessment tier determined by data classification and system criticality.
- Results reviewed by CISO. Findings must be remediated or accepted before go-live.

### 4.2 Contract Requirements
All vendor contracts must include:
- Data protection and confidentiality obligations
- Breach notification requirement (≤24 hours for Critical, ≤72 hours for High)
- Right to audit
- Data processing terms aligned with GDPR/CCPA
- Data return and destruction requirements upon termination
- SLAs for security-relevant metrics (uptime, incident response)

### 4.3 Ongoing Monitoring
- Critical vendors: quarterly security review + annual full reassessment
- High vendors: semi-annual review + annual SIG Lite update
- Medium vendors: annual self-assessment renewal
- All vendors: breach notification feed monitoring (continuous)
- Vendor risk score updated quarterly based on: breach history, financial health, security findings, SLA performance

### 4.4 Off-Boarding
- Vendor off-boarding process initiated 90 days before contract end.
- Data return or destruction confirmed in writing.
- Access revoked within 24 hours of contract termination.
- Final security assessment confirming data removal.

---

## 5. Vendor Risk Scoring Algorithm

Risk Score = (Data Sensitivity Score × 0.35) + (Breach History Score × 0.25) + (Financial Stability × 0.20) + (Control Effectiveness × 0.20)

| Component | Scale | Data Source |
|-----------|-------|-------------|
| Data Sensitivity | 1–10 (L1=1, L4=10) | Vendor tiering classification |
| Breach History | 0–10 (10 = multiple breaches in 2 years) | Breach notification feeds, news |
| Financial Stability | 0–10 (10 = bankruptcy risk) | D&B rating, financial statements |
| Control Effectiveness | 0–10 (10 = no controls) | SIG questionnaire scoring |

**Scoring Bands:** 0–3 = Low Risk, 4–6 = Medium Risk, 7–8 = High Risk, 9–10 = Critical Risk

---

## 6. Related Documents

POL-01 (Information Security Policy), POL-03 (Data Classification & Handling Policy), Vendor Risk Management Program
