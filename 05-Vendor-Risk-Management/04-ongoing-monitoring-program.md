# Vendor Risk — Ongoing Monitoring Program

**Phase:** 5 — Vendor Risk Management Program
**Objective:** Define continuous monitoring procedures for vendor security posture between annual assessments

---

## Monitoring Sources

| Source | Feed Type | Update Frequency | Coverage |
|--------|-----------|------------------|----------|
| Breach notification services (HaveIBeenPwned, Constella) | Automated | Continuous | All vendors |
| Vendor security blogs / status pages | Manual | Weekly | Critical + High vendors |
| SOC 2 / ISO certification status (AICPA, ANSI) | Automated | Monthly (via API) | Critical + High vendors |
| Financial health (SEC filings, D&B alerts) | Automated | Monthly | Critical vendors |
| News / dark web monitoring (brand monitoring) | Automated | Continuous | Critical vendors |
| Vendor SLA compliance data | Automated | Monthly | All vendors with SLAs |
| Vendor security portal review | Manual | Quarterly | Critical vendors |

---

## Monitoring Actions by Tier

### Critical Tier — Continuous Monitoring

| Frequency | Action | Owner |
|-----------|--------|-------|
| Daily | Automated breach notification feed scanning | Security Team |
| Weekly | Review vendor status pages, security advisories | Security Team |
| Monthly | Financial health check (SEC filings, D&B) | Procurement |
| Quarterly | Full risk score refresh + vendor portal review | Security Team |
| Annual | Full SIG re-assessment + SOC 2 report review + pentest review | CISO |

### High Tier — Regular Monitoring

| Frequency | Action | Owner |
|-----------|--------|-------|
| Weekly | Automated breach notification feed scanning | Security Team |
| Quarterly | Risk score update + vendor portal check | Security Team |
| Annual | SIG Lite re-assessment + SOC 2 report review | Security Team |

### Medium Tier — Periodic Monitoring

| Frequency | Action | Owner |
|-----------|--------|-------|
| Monthly | Automated breach notification feed | Security Team |
| Annual | Self-assessment questionnaire renewal | Vendor |
| Annual | Spot-check (10% of Medium vendors randomly selected) | Security Team |

### Low Tier — Passive Monitoring

| Frequency | Action | Owner |
|-----------|--------|-------|
| On incident | If breach notification affects a Low vendor, assess relevance | Security Team |

---

## Incident Response — Vendor Breach

When a vendor breach notification is received:

| Step | Action | Owner | Timeline |
|------|--------|-------|----------|
| 1 | Acknowledge receipt of breach notification | Security Team | ≤4 hours |
| 2 | Determine if NexPay data is affected | Security Team | ≤24 hours |
| 3 | If affected: classify incident per IR policy (POL-08) | CISO | ≤24 hours |
| 4 | Request breach details from vendor: what data, how many records, root cause, timeline | Security Team | ≤48 hours |
| 5 | Notify Legal, CISO, affected business owner | Security Team | ≤24 hours |
| 6 | Assess if vendor risk score needs immediate update | CISO | ≤48 hours |
| 7 | If Critical vendor: schedule emergency vendor review | CISO | ≤7 days |

---

## Monitoring Dashboard

| Metric | Critical | High | Medium | Low |
|--------|----------|------|--------|-----|
| Breach notifications (past 12mo) | 0 | 0 | 0 | 0 |
| Vendor risk score (avg) | 51 | 29 | 18 | 8 |
| Assessments overdue | 0 | 1 | 3 | N/A |
| Remediation items open | 2 | 4 | 0 | 0 |
| Score trend (QoQ) | Stable | Stable | Improving | Stable |
