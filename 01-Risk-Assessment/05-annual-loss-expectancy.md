# Annual Loss Expectancy — ALE/SLE/ARO Calculations

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Objective:** Provide granular SLE (Single Loss Expectancy), ARO (Annualized Rate of Occurrence), and ALE (Annualized Loss Expectancy) for board-level risk acceptance and insurance planning
**Framework:** FAIR → ALE = SLE × ARO
**Scope:** Top 15 risks ranked by ALE

---

## Calculation Methodology

| Metric | Formula | Description |
|--------|---------|-------------|
| AV (Asset Value) | Market replacement + data value | Total value of the asset to the business |
| EF (Exposure Factor) | % of asset value lost per incident | Determined by scenario severity |
| SLE (Single Loss Expectancy) | AV × EF | Cost of one incident |
| ARO (Annualized Rate of Occurrence) | Frequency estimate | How many times per year |
| **ALE (Annualized Loss Expectancy)** | SLE × ARO | Annual financial risk exposure |

---

## Asset Valuation Table

| Asset | Replacement Cost | Data Value | IP Value | Total AV | Basis |
|-------|-----------------|------------|----------|----------|-------|
| Customer PII Database | $250,000 | $8,000,000 | $0 | $8,250,000 | $6.67/user × 1.2M users |
| Payment Key Vault | $100,000 | $12,000,000 | $0 | $12,100,000 | PCI fines + fraud liability |
| Transaction Engine | $750,000 | $0 | $5,000,000 | $5,750,000 | 6 months dev effort to rebuild |
| Source Code Repository | $50,000 | $0 | $15,000,000 | $15,050,000 | 3 years of engineering IP |
| ML Fraud Models | $200,000 | $0 | $10,000,000 | $10,200,000 | 5 years of training data + research |
| Production Environment | $1,500,000 | $0 | $0 | $1,500,000 | AWS monthly burn × 12 × 1.5x overhead |
| Corporate Email | $150,000 | $2,000,000 | $0 | $2,150,000 | BEC risk, board comms, contracts |

---

## Detailed ALE Calculations

### 1. Payment Key Compromise (Vault)

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $12,100,000 | Key value = PCI fines + fraud liability + system trust |
| EF | 85% | Key compromise = near-total loss of payment trust |
| SLE | $10,285,000 | $12,100,000 × 0.85 |
| ARO | 1.2 | From FAIR analysis |
| **ALE** | **$12,342,000** | $10,285,000 × 1.2 |

### 2. Customer PII Data Breach (SQLi)

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $8,250,000 | PII value based on GDPR fines ($20M or 4% revenue) + customer churn |
| EF | 90% | Full database exfiltration likely if SQLi succeeds |
| SLE | $7,425,000 | $8,250,000 × 0.90 |
| ARO | 1.5 | From FAIR (reduced from 7.8 — assuming partial success filtering) |
| **ALE** | **$11,137,500** | $7,425,000 × 1.5 |

### 3. ML Model Theft

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $10,200,000 | 5 years R&D, competitive moat |
| EF | 60% | Model theft = loss of competitive advantage, not total IP loss |
| SLE | $6,120,000 | $10,200,000 × 0.60 |
| ARO | 3.0 | From FAIR |
| **ALE** | **$18,360,000** | $6,120,000 × 3.0 |

### 4. DB Privilege Escalation

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $8,250,000 | Same PII database |
| EF | 75% | Escalation likely enables limited exfiltration (not full dump) |
| SLE | $6,187,500 | $8,250,000 × 0.75 |
| ARO | 2.0 | From FAIR |
| **ALE** | **$12,375,000** | $6,187,500 × 2.0 |

### 5. Malicious PR / Supply Chain Attack

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $15,050,000 | Full source code + ML models + payment integration |
| EF | 40% | Backdoored code detected before full compromise in most cases |
| SLE | $6,020,000 | $15,050,000 × 0.40 |
| ARO | 1.05 | From FAIR |
| **ALE** | **$6,321,000** | $6,020,000 × 1.05 |

### 6. DDoS — Transaction Engine Outage

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $5,750,000 | Engine replacement cost + daily revenue |
| EF | 15% | DDoS causes outage, not destruction |
| SLE | $862,500 | $5,750,000 × 0.15 |
| ARO | 3.6 | From FAIR |
| **ALE** | **$3,105,000** | $862,500 × 3.6 |

### 7. CI/CD Vault Token Abuse

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $12,100,000 | Same key vault value |
| EF | 25% | Pipeline can read but not export all keys; partial compromise |
| SLE | $3,025,000 | $12,100,000 × 0.25 |
| ARO | 1.2 | From FAIR |
| **ALE** | **$3,630,000** | $3,025,000 × 1.2 |

### 8. JWT Forgery — Privilege Escalation

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $5,750,000 | Transaction engine |
| EF | 20% | Admin access enables fraudulent transactions but not full system loss |
| SLE | $1,150,000 | $5,750,000 × 0.20 |
| ARO | 1.5 | From FAIR |
| **ALE** | **$1,725,000** | $1,150,000 × 1.5 |

### 9. Internal MITM Attack

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $15,050,000 | Source code + transaction data combined |
| EF | 5% | Limited visibility; would need to chain with other attacks |
| SLE | $752,500 | $15,050,000 × 0.05 |
| ARO | 1.2 | From FAIR |
| **ALE** | **$903,000** | $752,500 × 1.2 |

### 10. Secrets Committed to Public Repo

| Factor | Value | Notes |
|--------|-------|-------|
| AV | $15,050,000 | If cloud creds are committed, entire infrastructure is at risk |
| EF | 10% | Secrets are typically revoked quickly (assuming monitoring exists) |
| SLE | $1,505,000 | $15,050,000 × 0.10 |
| ARO | 4.0 | From qualitative assessment + industry data |
| **ALE** | **$6,020,000** | $1,505,000 × 4.0 |

---

## ALE Ranking — All Risks

| Rank | Risk Scenario | SLE | ARO | ALE | Cumulative |
|------|--------------|------|-----|-----|------------|
| 1 | ML Model Theft | $6,120,000 | 3.0 | $18,360,000 | $18,360,000 |
| 2 | DB Privilege Escalation | $6,187,500 | 2.0 | $12,375,000 | $30,735,000 |
| 3 | Payment Key Compromise | $10,285,000 | 1.2 | $12,342,000 | $43,077,000 |
| 4 | PII Data Breach (SQLi) | $7,425,000 | 1.5 | $11,137,500 | $54,214,500 |
| 5 | Secrets Committed to Repo | $1,505,000 | 4.0 | $6,020,000 | $60,234,500 |
| 6 | Malicious PR / Supply Chain | $6,020,000 | 1.05 | $6,321,000 | $66,555,500 |
| 7 | CI/CD Vault Token Abuse | $3,025,000 | 1.2 | $3,630,000 | $70,185,500 |
| 8 | DDoS Transaction Engine | $862,500 | 3.6 | $3,105,000 | $73,290,500 |
| 9 | JWT Forgery | $1,150,000 | 1.5 | $1,725,000 | $75,015,500 |
| 10 | Internal MITM | $752,500 | 1.2 | $903,000 | $75,918,500 |
| | **Total** | | | **$75,918,500** | |

---

## Key Findings for Insurance

1. **Total ALE for top 10 risks: $75.9M** — nearly 2× the $40M funding round
2. **Cyber insurance limit recommendation:** $20M (covers 26% of total ALE — policy cost ~$15K/year)
3. **ML model theft is the #1 risk ($18.4M ALE)** — standard cyber insurance does not cover IP theft
4. **Mitigation ROI:** Spending $150K on controls reduces ALE from $75.9M to an estimated $11.4M (85% reduction) — over 400× ROI
5. **Self-insured retention (SIR):** Recommended $250K — balances premium cost with manageable out-of-pocket exposure
