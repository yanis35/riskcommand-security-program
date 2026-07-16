# Board Report — Q1 2026 Security Program Update

**Phase:** 6 — Executive Reporting & KRIs
**Audience:** Board of Directors
**Prepared by:** CISO
**Date:** April 2026
**Classification:** Confidential — Board Materials

---

## Executive Summary

The security program completed its first quarter of operation. Significant foundational work was completed: risk assessment, policy framework, BCP/DR planning, security awareness program launch, and vendor risk management initiation. The organization's overall security maturity is assessed at CMMI Level 1.8 (between Initial and Managed), with a target of Level 2.8 by year end.

**Key metrics:**
- Security program budget utilization: 31% ($175K of $570K spent)
- Risk reduction achieved (est.): $13.6M ALE reduction (25% of target)
- Security incidents: 0 confirmed incidents in Q1
- ROSI: 7,694% (Q1 cumulative)

---

## Risk Posture Update

### Current Risk Profile

| Risk Level | Count (Start of Q1) | Count (End of Q1) | Change |
|------------|---------------------|-------------------|--------|
| Critical | 8 | 5 | −3 (controls deployed for R-05, R-07, R-10) |
| High | 2 | 4 | +2 (residual risk recalculated after control deployment) |
| Medium | 0 | 1 | +1 |
| Low | 0 | 0 | — |
| **Total ALE** | **$75.9M** | **$62.3M** | **−$13.6M (18% reduction)** |

### Top 5 Residual Risks

| Risk | Residual Score | Owner | Status |
|------|---------------|-------|--------|
| ML Model Theft ($18.4M ALE) | High | VP Eng | Controls in progress (S3 logging, KMS) |
| Payment Key Compromise ($12.3M ALE) | High | CTO | Vault MFA enabled, HSM deployment Q2 |
| DB Escalation ($12.4M ALE) | High | CTO | Row-level security in progress |
| PII Data Breach ($11.1M ALE) | High | CTO | WAF OWASP ruleset deployed, retesting |
| Secrets in Repo ($6.0M ALE) | Medium | VP Eng | Secret scanning deployed, credential rotation complete |

---

## Milestones Achieved (Q1)

| Milestone | Status | Completion |
|-----------|--------|------------|
| Crown jewels analysis | Done | January |
| STRIDE threat modeling (4 critical systems) | Done | January |
| FAIR quantitative risk assessment | Done | January |
| Risk register with 10 top risks | Done | January |
| Board heatmap presentation | Done | January |
| Information Security Policy (Master) | Done | January |
| 11 domain security policies | Done | February |
| NIST CSF control mapping | Done | February |
| RACI matrix | Done | February |
| Business Impact Analysis | Done | February |
| 4 DR runbooks | Done | February |
| Tabletop exercise (ransomware + key person) | Done | March |
| Tabletop after-action report | Done | March |
| GoPhish deployment | Done | March |
| Wave 1 (generic phish) | Done | March |
| Wave 2 (spear phish) | Done | March |
| Wave 3 (BEC) — targeted at finance | Done | March |
| Wave 4 (credential harvest) | Done | March |
| Vendor tiering (31 vendors) | Done | March |
| KRI dashboard | Done | March |
| CMMI maturity assessment | Done | March |

---

## Q2 Plan

| Milestone | Target | Owner |
|-----------|--------|-------|
| HSM deployment for payment keys | May | CTO |
| Cross-region DR infrastructure (Terraform) | May | CTO |
| DR technical test (T1 systems) | June | CTO |
| All Critical vendor assessments complete | May | Security Team |
| Vendor risk scoring operational | May | Security Team |
| Hardware MFA tokens for Finance team | April | CTO |
| Security Champions program launch | April | CISO |
| SIEM exfiltration detection rules | April | Security Team |
| Automated access reviews (privileged accounts) | May | CTO |
| Quarterly board security report | April | CISO |

---

## Budget Utilization

| Category | Annual Budget | Q1 Spend | Remaining |
|----------|--------------|----------|-----------|
| People (existing) | $150,000 | $37,500 | $112,500 |
| Technical controls | $205,000 | $85,000 | $120,000 |
| External assessments | $60,000 | $25,000 | $35,000 |
| Training & awareness | $33,000 | $10,000 | $23,000 |
| DR infrastructure | $57,000 | $0 | $57,000 |
| Cyber insurance | $15,000 | $15,000 | $0 |
| Reserves (incident response) | $50,000 | $0 | $50,000 |
| **Total** | **$570,000** | **$175,000** | **$395,000** |

---

## Risk Acceptance Requests

| Risk | ALE | Justification | Proposed Term | 
|------|-----|---------------|---------------|
| Tabletop finding — Backup MFA single point of failure | Included in DB risk | Compensating control: alternate recovery path via AWS support | 30 days |
| CI/CD Vault token scope (path restriction pending) | $3.6M | Compensating: CI/CD runs in ephemeral containers with no persistent access | 60 days |

**Board action requested:** Approve risk acceptance for above items.

---

## Board Decisions Required

| # | Decision | Recommendation |
|---|----------|---------------|
| 1 | Approve Q2 security program plan and budget allocation | Approve |
| 2 | Approve risk acceptance for tabletop finding (30-day term) | Approve |
| 3 | Approve risk acceptance for CI/CD token scope (60-day term) | Approve |
| 4 | Note: Cyber insurance renewal due Q3 — recommend $20M coverage limit | Note |

---

## Appendix — KRI Dashboard (Q1)

```
KRI                               Q1 Actual   Status
─────────────────────────────────────────────────────
Patch Compliance                  92%          🟡
Phishing Click Rate               33.4%        🔴
Open Critical Vulns               2            🟡
MTTD                              2.5 hrs      🟡
MTTR                              6 hrs        🟡
Vendor Risk Score (Avg)           48           🟡
Access Review Compliance          83%          🔴
Training Completion               94%          🟡
Phishing Report Rate              12%          🔴
DR Test Success Rate              N/A          ⚪
```
