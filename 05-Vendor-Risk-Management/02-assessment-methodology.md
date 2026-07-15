# Vendor Risk Assessment Methodology

**Phase:** 5 — Vendor Risk Management Program
**Objective:** Define the assessment methodology, questionnaire templates, and scoring for each vendor tier

---

## Tier Classification → Assessment Mapping

| Tier | Assessment | Effort | Reviewer |
|------|------------|--------|----------|
| Critical | Full SIG (200+ questions) + SOC 2 Type II + Pentest + On-site | 2–3 weeks | CISO |
| High | SIG Lite (50 questions) + SOC 2 Type II + Attestation | 1–2 weeks | Security Team |
| Medium | Self-Assessment Questionnaire (15 questions) | 2 days | Vendor (self) |
| Low | Contractual clauses only | 1 day | Legal |

---

## Critical Tier — Full SIG Assessment

### Assessment Components

| Component | Weight | Description |
|-----------|--------|-------------|
| SIG Questionnaire | 50% | Standardized Information Gathering questionnaire covering all 18 NIST CSF domains |
| SOC 2 Type II Report | 20% | Auditor opinion on controls — review for exceptions, deficiencies |
| Penetration Test Results | 15% | External pentest report within 12 months — review findings and remediation |
| Financial Stability | 10% | D&B rating, recent funding rounds, revenue trends |
| Contractual Review | 5% | Data protection, breach notification, SLA terms, right to audit |

### SIG Scoring Rubric

| Maturity Level | Score | Definition |
|----------------|-------|------------|
| Optimizing | 5 | Process is mature, automated, continuously improving |
| Managed | 4 | Process is measured, monitored, quantitatively managed |
| Defined | 3 | Process is documented, standardized, consistently followed |
| Partial | 2 | Process exists but is ad-hoc, inconsistent, or undocumented |
| Not Implemented | 1 | No process exists |

**Total SIG Score:** Average across all domains (target: ≥3.5 for Critical tier)

---

## High Tier — SIG Lite Assessment

### Assessment Components

| Component | Weight | Description |
|-----------|--------|-------------|
| SIG Lite Questionnaire | 60% | 50-question subset covering: access control, data protection, incident response, compliance, BCP |
| SOC 2 Report | 25% | SOC 2 Type II or Type I — review for adverse opinions |
| Attestation Letter | 15% | Signed attestation from vendor CISO or equivalent |

### SIG Lite Scoring

| Band | Score | Action |
|------|-------|--------|
| 4.0 – 5.0 | Low Risk | No further action |
| 3.0 – 3.9 | Medium Risk | Follow-up on specific domain gaps |
| 2.0 – 2.9 | High Risk | Remediation plan required within 90 days |
| <2.0 | Critical Risk | Escalate to CISO — consider replacement |

---

## Medium Tier — Self-Assessment Questionnaire

### 15-Question Self Assessment

| # | Question | Yes/No | Evidence |
|---|----------|--------|----------|
| 1 | Does your organization have a published security policy? | | |
| 2 | Do you encrypt data at rest? | | |
| 3 | Do you encrypt data in transit? | | |
| 4 | Do you perform background checks on employees with data access? | | |
| 5 | Do you have multi-factor authentication for administrative access? | | |
| 6 | Do you have an incident response plan? | | |
| 7 | Will you notify NexPay within 72 hours of a security incident affecting our data? | | |
| 8 | Do you perform regular vulnerability scans? | | |
| 9 | Do you have a business continuity / disaster recovery plan? | | |
| 10 | Do you maintain access logs for systems processing our data? | | |
| 11 | Do you have a data retention and disposal policy? | | |
| 12 | Will you delete our data upon contract termination? | | |
| 13 | Do you conduct annual employee security awareness training? | | |
| 14 | Do you have a software development lifecycle process? (if applicable) | | |
| 15 | Do you use sub-processors for services involving our data? | | |

**Scoring:** 13–15 "Yes" = Low Risk, 10–12 = Medium Risk, <10 = High Risk (trigger SIG Lite)

---

## Low Tier — Contractual Clauses

Standard clauses included in all Low-tier vendor contracts:

1. **Data protection:** Vendor agrees to protect NexPay data with appropriate technical and organizational measures
2. **Confidentiality:** Vendor maintains confidentiality of any NexPay information accessed during service delivery
3. **Sub-processors:** Vendor must notify if they engage sub-processors for NexPay-related services
4. **Compliance with law:** Vendor agrees to comply with applicable data protection laws
5. **No security assessment required:** Waived for Low tier
