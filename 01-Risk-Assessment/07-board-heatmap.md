# Board Risk Heatmap — Executive Summary

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Audience:** Board of Directors, Executive Leadership
**Format:** Board-ready presentation (this document serves as the briefing memo + slide deck content)
**Date:** Q1 2026

---

## Executive Summary

NexPay Financial engaged in a comprehensive risk assessment across all critical systems. The assessment identified **10 top risks** representing a combined **$70.9M Annualized Loss Expectancy (ALE)** — nearly 1.8× the company's $40M Series B funding.

**Key findings:**
- 8 of 10 top risks are rated **Critical** (risk score 15–25)
- **4 risks account for 76% of total ALE:** ML model theft, DB privilege escalation, payment key compromise, and PII data breach
- **$150K in security controls** can reduce total ALE by an estimated 85%
- **Current cyber insurance coverage gap:** Standard policies do not cover IP theft ($18.4M ALE from ML model theft)

---

## Risk Heatmap — Visual

```
                    I M P A C T
                    Low     Medium   High   Critical
                    (1-2)   (3-4)    (5-8)  (9-10)
              ┌────────────────────────────────────┐
     Almost   │                                    │
     Certain  │             ┌───┐                   │
     (5)      │             │PII│  Key Vault │
              │             │DB │  Compromise│
              │             │Esc│  ┌───┐      │
              ├─────────────┤al.├──┤   │      │
     Likely   │             │   │  │   │      │
     (4)      │  Secrets    └───┘  │DD │      │
L             │  in Repo          │oS │      │
I             │  ML Model    ┌───┐ │   │      │
K     Possible│  Theft       │Mal│ └───┘      │
E     (3)     │             │PR │            │
L             │             │   │            │
I             ├─────────────┤   ├────────────┤
N     Unlikely│             │JWT│            │
K     (2)     │  Internal   │Frg│            │
              │  MITM       │   │            │
              │             └───┘            │
     Rare     │                                    │
     (1)      │                                    │
              └────────────────────────────────────┘
```

| Color | Zone | Count | Total ALE |
|-------|------|-------|-----------|
| Red | Critical (15–25) | 8 | $58,503,500 |
| Orange | High (10–14) | 2 | $18,482,000 |
| Yellow | Medium (5–9) | 0 | $0 |
| Green | Low (1–4) | 0 | $0 |

---

## Top 5 Risks — Board Summary

### #1 — ML Model Theft ($18.4M ALE)

| Aspect | Detail |
|--------|--------|
| What's at risk | Proprietary fraud detection ML models — 5 years of training data and research |
| How it happens | Engineer with broad S3 permissions exports model files |
| Why it matters | Our competitive moat disappears — competitors (and fraudsters) replicate detection capability |
| Fix | S3 access logging, file-level ACLs, KMS encryption, DLP monitoring |
| Cost to fix | $5K one-time |
| Timeline | 2 weeks |

### #2 — DB Privilege Escalation ($12.4M ALE)

| Aspect | Detail |
|--------|--------|
| What's at risk | 1.2M user records including SSNs, bank accounts, and KYC documents |
| How it happens | Over-permissioned DB role exploited by internal actor or compromised engineer |
| Why it matters | GDPR fines (4% of revenue = $12.8M), mandatory breach notification, customer exodus |
| Fix | Row-level security, revoke excessive privileges, just-in-time access |
| Cost to fix | $10K |
| Timeline | 4 weeks |

### #3 — Payment Key Compromise ($12.3M ALE)

| Asset | Detail |
|--------|--------|
| What's at risk | All payment signing keys, API credentials, TLS private keys |
| How it happens | Attacker authenticates to Vault without MFA — all keys exposed |
| Why it matters | PCI DSS violation, fraudulent transactions, payment system trust destroyed |
| Fix | MFA on Vault, HSM deployment, path-restricted tokens |
| Cost to fix | $15K |
| Timeline | 2 weeks (MFA), 2 months (HSM) |

### #4 — PII Data Breach via SQL Injection ($11.1M ALE)

| Aspect | Detail |
|--------|--------|
| What's at risk | Customer PII accessible through public API endpoints |
| How it happens | WAF deployed without SQLi ruleset — standard SQL injection attack succeeds |
| Why it matters | $11M+ in regulatory fines, breach response, and customer churn |
| Fix | Deploy WAF OWASP SQLi ruleset, run DAST scanner |
| Cost to fix | $5K |
| Timeline | 2 weeks |

### #5 — Secrets in Public Repository ($6.0M ALE)

| Aspect | Detail |
|--------|--------|
| What's at risk | Cloud credentials, API keys, database passwords in source code |
| How it happens | Developer commits credentials to GitHub (accidental) |
| Why it matters | Full production environment exposed — data theft, resource abuse, cryptomining |
| Fix | Secret scanning in CI/CD, enforced pre-commit hooks, credential rotation |
| Cost to fix | $1K |
| Timeline | 1 week |

---

## Risk Treatment Roadmap (30-60-90 Day)

### Next 30 Days ($36K investment)

| Risk | Action | Cost | ALE Reduction |
|------|--------|------|---------------|
| R-05 JWT Forgery | Rotate keys, enforce quarterly rotation | $3K | $1.7M → $400K |
| R-07 CI/CD Token | Path-restrict Vault tokens per pipeline | $2K | $3.6M → $800K |
| R-10 Secrets | CI/CD secret scanning, credential rotation | $1K | $6.0M → $1.5M |
| R-01 SQLi | WAF OWASP ruleset + DAST scan | $5K | $11.1M → $2.8M |
| R-02 Vault MFA | Enable MFA on Vault authentication | $2K | $12.3M → $4.0M |
| R-04 Malicious PR | Branch protection enforcement | $0 | $6.3M → $1.6M |
| R-09 ML Model | S3 access logging + ACLs + KMS | $5K | $18.4M → $4.6M |
| R-03 DB Escalation | Row-level security, revoke privileges | $10K | $12.4M → $3.1M |
| R-06 DDoS | Shield Advanced + WAF DDoS rules | $8K/mo | $3.1M → $800K |

**Total 30-day investment:** $36K one-time + $8K/month ongoing
**Projected ALE reduction:** $75.9M → $19.0M (75% reduction)

### 60-Day Window ($50K investment)

| Action | Cost | Description |
|--------|------|-------------|
| HSM deployment | $30K | Hardware security module for payment keys |
| mTLS mesh implementation | $20K | Encrypt all internal service traffic |
| Phishing platform deployment | $0 (tool) | GoPhish setup + first campaign |

### 90-Day Window ($64K investment)

| Action | Cost | Description |
|--------|------|-------------|
| SIEM deployment | $40K | Security information and event management |
| EDR rollout | $24K/yr | Endpoint detection and response (200 endpoints at $10/endpoint/month) |
| First external penetration test | $25K | Third-party pentest of all critical systems |

---

## Budget Request

| Category | One-Time | Monthly Recurring | Annual Total |
|----------|----------|-------------------|--------------|
| Immediate controls (30-day) | $36,000 | $8,000 | $132,000 |
| Near-term controls (60-day) | $50,000 | $0 | $50,000 |
| Ongoing operations (90-day) | $65,000 | $5,333 | $129,000 |
| Cyber insurance premium | $0 | $0 | $15,000 |
| **Total** | **$151,000** | **$13,333** | **$326,000** |

**Remaining budget:** $174,000 of $500K allocation
**Recommended reserve:** For incident response retainer ($50K/year) and unanticipated findings from pentest

---

## Board Action Items

| # | Action | Owner | Due |
|---|--------|-------|-----|
| 1 | **Approve** $151K security control investment | Board | This meeting |
| 2 | **Approve** $8K/month AWS Shield Advanced DDoS protection | Board | This meeting |
| 3 | **Approve** $15K/year cyber insurance policy upgrade | Board | This meeting |
| 4 | **Direct** CTO to implement 30-day controls immediately | Board | Next meeting update |
| 5 | **Review** risk register monthly — next update at Q2 board meeting | CISO | Ongoing |

---

## Risk Appetite Statement (Proposed)

"NexPay Financial will accept residual risks rated Medium (score 1–9) after cost-effective controls are implemented. Risks rated High (10–14) must have active remediation plans with identified owners. Risks rated Critical (15+) must be remediated or explicitly accepted by the Board with documented rationale. Annual aggregate residual risk exposure shall not exceed $15M in quantified ALE."

---

## Appendix: Methodology

- **Qualitative assessment:** 5×5 matrix per ISO 31000 / NIST SP 800-30
- **Quantitative assessment:** FAIR (Factor Analysis of Information Risk) via OpenFAIR toolkit
- **Threat modeling:** Microsoft STRIDE per critical system
- **Asset valuation:** Replacement cost + data value + IP value
- **Consulting rate context:** ALE figures based on GDPR/CCPA fine structures, PCI DSS penalty schedules, industry breach cost data (IBM Cost of a Data Breach 2025), and financial services revenue benchmarks
