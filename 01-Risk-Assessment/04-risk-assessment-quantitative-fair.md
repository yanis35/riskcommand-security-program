# Risk Assessment — Quantitative (FAIR Methodology)

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Objective:** Quantify top 10 risks in financial terms using FAIR (Factor Analysis of Information Risk)
**Framework:** FAIR Institute — OpenFAIR Standard (ISO 27005 alignment)
**Tool:** OpenFAIR Toolkit (Excel-based)

---

## FAIR Model Overview

FAIR decomposes risk into dollar-denominated Loss Event Frequency (LEF) and Loss Magnitude (LM):

```
Risk ($/year) = Loss Event Frequency × Loss Magnitude

LEF = Threat Event Frequency × Vulnerability (probability of success)
LM = Primary Loss + Secondary Loss

Primary Loss = Direct costs (response, forensics, legal, notification)
Secondary Loss = Indirect costs (reputation, customer churn, regulatory fines, litigation)
```

---

## Top 10 Risks — FAIR Quantification

### R-01: Customer PII Exfiltrated via SQL Injection

**Scenario:** Attacker exploits missing WAF SQLi rules to query `customers` table via API endpoint

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 12/year | Unauthenticated internet-facing API; 1 attempt/month from automated scanners |
| Vulnerability | 65% | WAF lacks SQLi ruleset; application framework has known SQLi patterns |
| Loss Event Frequency | 7.8/year | 12 × 0.65 = 7.8 successful SQLi events per year |
| Primary Loss per Event | $45,000 | IR retainer ($15K), forensic investigation ($20K), legal hold ($10K) |
| Secondary Loss per Event | $1,200,000 | Regulatory fine ($800K GDPR), customer churn ($300K), breach notification ($100K) |
| **Annual Loss Expectancy** | **$9,711,000** | 7.8 × ($45,000 + $1,200,000) |

### R-02: Payment Keys Stolen via Vault Compromise

**Scenario:** Attacker authenticates to Vault without MFA and exports all payment signing keys

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 6/year | Internal attacker with Vault access; 0.5/month |
| Vulnerability | 40% | No MFA on Vault, but network access is partially restricted |
| Loss Event Frequency | 2.4/year | 6 × 0.40 |
| Primary Loss per Event | $180,000 | Key rotation ($50K), system rebuild ($100K), audit ($30K) |
| Secondary Loss per Event | $4,500,000 | PCI DSS fine ($500K), payment fraud liability ($3M), brand damage ($1M) |
| **Annual Loss Expectancy** | **$11,232,000** | 2.4 × ($180,000 + $4,500,000) |

### R-03: DB Privilege Escalation — Full Data Compromise

**Scenario:** Read-only user exploits DB vulnerability to become admin, exports entire PII dataset

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 4/year | Privileged internal users; quarterly attempted or accidental escalation |
| Vulnerability | 50% | Over-permissioned roles, no row-level security, no separation of duties |
| Loss Event Frequency | 2.0/year | 4 × 0.50 |
| Primary Loss per Event | $85,000 | Incident response ($40K), forensic analysis ($30K), legal ($15K) |
| Secondary Loss per Event | $2,500,000 | Regulatory fines ($800K), customer lawsuits ($1.2M), churn ($500K) |
| **Annual Loss Expectancy** | **$5,170,000** | 2.0 × ($85,000 + $2,500,000) |

### R-04: Malicious PR Merges Backdoor into Production

**Scenario:** Attacker submits malicious PR through compromised maintainer account, bypasses branch protection

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 3/year | Targeted supply chain attack on fintech startups is increasingly common |
| Vulnerability | 35% | Branch protection on main only; no code review enforcement on release branches |
| Loss Event Frequency | 1.05/year | 3 × 0.35 |
| Primary Loss per Event | $250,000 | Emergency code review ($50K), rollback ($30K), CI/CD cleaning ($20K), incident response ($150K) |
| Secondary Loss per Event | $3,000,000 | Customer data exposure ($1.5M), code integrity loss ($1M), reputation ($500K) |
| **Annual Loss Expectancy** | **$3,412,500** | 1.05 × ($250,000 + $3,000,000) |

### R-05: JWT Token Forged with Escalated Privileges

**Scenario:** Attacker extracts public key from client side and forges JWT with admin claims

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 6/year | API targets are continuously probed for JWT vulnerabilities |
| Vulnerability | 25% | RS256 signed, but public key exposed in client code; no key rotation |
| Loss Event Frequency | 1.5/year | 6 × 0.25 |
| Primary Loss per Event | $55,000 | Emergency key rotation ($15K), access audit ($25K), hotfix ($15K) |
| Secondary Loss per Event | $950,000 | Fraudulent transactions ($500K), data exposure ($300K), regulatory ($150K) |
| **Annual Loss Expectancy** | **$1,507,500** | 1.5 × ($55,000 + $950,000) |

### R-06: DDoS Takes Down Transaction Engine

**Scenario:** DDoS attack saturates API endpoint, blocking legitimate transactions for 4+ hours

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 8/year | Fintech is a common DDoS target; average 0.67 events/month |
| Vulnerability | 45% | CloudFront + basic rate limiting; no dedicated DDoS protection |
| Loss Event Frequency | 3.6/year | 8 × 0.45 |
| Primary Loss per Event | $35,000 | Engineering overtime ($15K), AWS DDoS mitigation costs ($20K) |
| Secondary Loss per Event | $210,000 | Revenue loss ($44,500/hour × 4 hours = $178K), SLA penalties ($32K) |
| **Annual Loss Expectancy** | **$882,000** | 3.6 × ($35,000 + $210,000) |

### R-07: Over-Scoped CI/CD Token Reads All Vault Secrets

**Scenario:** CI/CD pipeline breached; attacker uses Vault token with full KV mount scope to export all secrets

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 4/year | CI/CD pipelines regularly targeted; 1 attempt/quarter |
| Vulnerability | 30% | Token scoped to KV mount (too broad), no path restriction |
| Loss Event Frequency | 1.2/year | 4 × 0.30 |
| Primary Loss per Event | $95,000 | Secret rotation ($40K), pipeline rebuild ($35K), audit ($20K) |
| Secondary Loss per Event | $1,800,000 | Key compromise ($1M), data breach ($500K), fraud loss ($300K) |
| **Annual Loss Expectancy** | **$2,274,000** | 1.2 × ($95,000 + $1,800,000) |

### R-08: Payment Key Tampering

**Scenario:** Attacker intercepts key retrieval and replaces legitimate payment API key with malicious one

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 2/year | Extremely targeted attack; assumes insider threat or deep compromise |
| Vulnerability | 20% | No integrity verification on key retrieval at application layer |
| Loss Event Frequency | 0.4/year | 2 × 0.20 |
| Primary Loss per Event | $500,000 | Forensic investigation ($200K), system-wide key rotation ($300K) |
| Secondary Loss per Event | $5,000,000 | Payment fraud ($3M), PCI compliance loss ($1M), regulatory ($1M) |
| **Annual Loss Expectancy** | **$2,200,000** | 0.4 × ($500,000 + $5,000,000) |

### R-11: ML Model Exfiltrated from S3

**Scenario:** Employee or external attacker with S3 read access downloads proprietary ML fraud detection model

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 5/year | Multiple engineers have broad S3 access; accidental or malicious exfil |
| Vulnerability | 60% | S3 bucket has no access logging, no file-level ACLs, default encryption only |
| Loss Event Frequency | 3.0/year | 5 × 0.60 |
| Primary Loss per Event | $25,000 | Investigation ($15K), model retraining ($10K) |
| Secondary Loss per Event | $1,500,000 | Competitive advantage loss ($1M), IP theft ($500K) |
| **Annual Loss Expectancy** | **$4,575,000** | 3.0 × ($25,000 + $1,500,000) |

### R-17: Internal Service Traffic Not Encrypted

**Scenario:** Attacker with internal network access performs MITM between microservices

| FAIR Factor | Input | Rationale |
|-------------|-------|-----------|
| Threat Event Frequency | 3/year | Internal network is flat; attacker with initial foothold can sniff traffic |
| Vulnerability | 40% | Some internal comms are plaintext HTTP, some use mTLS |
| Loss Event Frequency | 1.2/year | 3 × 0.40 |
| Primary Loss per Event | $75,000 | Investigation ($30K), mTLS deployment ($45K emergency) |
| Secondary Loss per Event | $600,000 | Data interception ($300K), transaction manipulation ($300K) |
| **Annual Loss Expectancy** | **$810,000** | 1.2 × ($75,000 + $600,000) |

---

## FAIR Summary Table

| Rank | Risk | ALE (annualized) | % of Total |
|------|------|------------------|------------|
| 1 | R-02 — Vault key compromise | $11,232,000 | 26.7% |
| 2 | R-01 — SQLi PII exfil | $9,711,000 | 23.1% |
| 3 | R-03 — DB escalation | $5,170,000 | 12.3% |
| 4 | R-11 — ML model theft | $4,575,000 | 10.9% |
| 5 | R-04 — Malicious PR backdoor | $3,412,500 | 8.1% |
| 6 | R-07 — CI/CD Vault token | $2,274,000 | 5.4% |
| 7 | R-08 — Payment key tampering | $2,200,000 | 5.2% |
| 8 | R-05 — JWT forgery | $1,507,500 | 3.6% |
| 9 | R-06 — DDoS | $882,000 | 2.1% |
| 10 | R-17 — Internal MITM | $810,000 | 1.9% |
| | **Total Top 10 ALE** | **$41,774,000** | 100% |

---

## ROSI (Return on Security Investment) Analysis

**Example — Remediation of R-01 (SQLi):**

| Item | Value |
|------|-------|
| Current ALE | $9,711,000 |
| Residual ALE after control (estimated 90% reduction) | $971,100 |
| Risk reduction | $8,739,900 |
| Cost of control (WAF, ruleset, testing, annual maintenance) | $35,000 |
| **ROSI** | **($8,739,900 − $35,000) / $35,000 = 24,871%** |

---

## Key Takeaways for the Board

1. **Top 10 risks from FAIR analysis represent $41.8M in annual loss expectancy** — exceeding the company's $40M funding round *(Note: The comprehensive ALE analysis covering all crown jewel risks yields a $75.9M baseline — see ALE/SLE/ARO Calculations for the complete picture.)*
2. **Four risks account for 73% of total ALE:** Vault compromise, SQLi, DB escalation, and ML model theft
3. **$150K in security controls** can reduce total ALE by an estimated 72%, from $75.9M to $21.4M (see ALE/SLE/ARO Calculations for detailed ROI)
4. **Risk transfer (cyber insurance)** covers an estimated $10M in secondary losses — but does not cover regulatory fines or competitive loss from IP theft
5. **Recommended budget:** $150K one-time for immediate controls, $50K/year for ongoing operations
