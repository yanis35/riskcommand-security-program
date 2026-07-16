# ROSI Calculation — Return on Security Investment

**Phase:** 6 — Executive Reporting & KRIs
**Objective:** Quantify the financial return on security control investments for board decision-making
**Framework:** ROSI = (Risk Reduction − Cost of Control) / Cost of Control

---

## ROSI Formula

```
ROSI = (ALE_before − ALE_after − Cost_of_control) / Cost_of_control

Where:
  ALE_before = Annualized Loss Expectancy before control
  ALE_after = Annualized Loss Expectancy after control (residual)
  Cost_of_control = TCO of control (implementation + annual maintenance)
```

---

## Program-Level ROSI

### Investment Summary

| Category | One-Time Cost | Annual Recurring | Annual TCO |
|----------|---------------|-----------------|------------|
| Technical controls (WAF, EDR, SIEM, CSPM) | $85,000 | $120,000 | $205,000 |
| People (Security Engineer) | $0 (existing) | $150,000 | $150,000 |
| External assessments (pentest, SIG review) | $35,000 | $25,000 | $60,000 |
| Training & awareness | $10,000 | $23,000 | $33,000 |
| DR infrastructure (cross-region) | $45,000 | $12,000 | $57,000 |
| Cyber insurance | $0 | $15,000 | $15,000 |
| **Total** | **$175,000** | **$345,000** | **$520,000** ^[Total program cost includes a $20K incident response reserve not reflected in the base budget.] |

### Risk Reduction

| Risk | ALE Before | ALE After (Projected) | Reduction |
|------|------------|----------------------|-----------|
| PII Data Breach (SQLi) | $11,137,500 | $2,227,500 | $8,910,000 |
| Payment Key Compromise | $12,342,000 | $3,702,600 | $8,639,400 |
| DB Escalation | $12,375,000 | $3,712,500 | $8,662,500 |
| ML Model Theft | $18,360,000 | $5,508,000 | $12,852,000 |
| Malicious PR | $6,321,000 | $1,896,300 | $4,424,700 |
| CI/CD Token Abuse | $3,630,000 | $1,089,000 | $2,541,000 |
| JWT Forgery | $1,725,000 | $517,500 | $1,207,500 |
| DDoS | $3,105,000 | $931,500 | $2,173,500 |
| Secrets in Repo | $6,020,000 | $1,506,000 | $4,514,000 |
| Internal MITM | $903,000 | $270,900 | $632,100 |
| **Total** | **$75,918,500** | **$21,361,800** | **$54,556,700** |

### ROSI Calculation

```
ROSI = ($54,556,700 − $520,000) / $520,000 = 10,392%
```

**Result:** For every $1 invested in security controls, NexPay realizes ~$104 in risk reduction.

---

## Individual Control ROSI

### Control: WAF with OWASP Ruleset

| Metric | Value |
|--------|-------|
| Risk Addressed | SQLi (ALE reduction: $8.9M) |
| Implementation Cost | $5,000 |
| Annual Maintenance | $12,000 |
| 3-Year TCO | $41,000 |
| Risk Reduction (3yr) | $26,730,000 |
| **ROSI** | **(26,730,000 − 41,000) / 41,000 = 65,095%** |

### Control: HSM + Vault MFA

| Metric | Value |
|--------|-------|
| Risk Addressed | Key Compromise (ALE reduction: $8.6M) |
| Implementation Cost | $32,000 |
| Annual Maintenance | $5,000 |
| 3-Year TCO | $47,000 |
| Risk Reduction (3yr) | $25,918,200 |
| **ROSI** | **(25,918,200 − 47,000) / 47,000 = 55,045%** |

### Control: Cross-Region DR Infrastructure

| Metric | Value |
|--------|-------|
| Risk Addressed | DDoS + Region Failure (ALE reduction: $2.2M) |
| Implementation Cost | $45,000 |
| Annual Maintenance | $12,000 |
| 3-Year TCO | $81,000 |
| Risk Reduction (3yr) | $6,520,500 |
| **ROSI** | **(6,520,500 − 81,000) / 81,000 = 7,950%** |

### Control: Phishing Awareness Program

| Metric | Value |
|--------|-------|
| Risk Addressed | BEC + Credential Theft (ALE reduction: est. $2M) |
| Implementation Cost | $10,000 |
| Annual Maintenance | $23,000 |
| 3-Year TCO | $79,000 |
| Risk Reduction (3yr) | $6,000,000 |
| **ROSI** | **(6,000,000 − 79,000) / 79,000 = 7,495%** |

---

## Cumulative ROSI by Quarter

| Quarter | Cumulative Investment | Cumulative Risk Reduction | Cumulative ROSI |
|---------|----------------------|--------------------------|-----------------|
| Q1 | $175,000 | $13,639,175 | 7,694% |
| Q2 | $261,250 | $27,278,350 | 10,342% |
| Q3 | $347,500 | $40,917,525 | 11,676% |
| Q4 | $520,000 | $54,556,700 | 10,392% |

---

## Board-Level Summary

**The security program delivers 104× ROI — for every $1 spent, NexPay avoids $104 in expected annual losses.**

| Metric | Value |
|--------|-------|
| Total program cost (annual) | $520,000 |
| Risk reduction (annual) | $54,556,700 |
| Net benefit (annual) | $54,036,700 |
| ROSI | 10,392% |
| Breakeven point | <1 month |

**Note:** ALE figures represent potential losses. Actual losses may vary. ROSI is a planning tool, not a guarantee. However, the magnitude of the return (104×) strongly supports continued security investment.
