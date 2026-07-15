# Vendor Risk Scoring Algorithm

**Phase:** 5 — Vendor Risk Management Program
**Objective:** Define the quantitative risk scoring algorithm for vendor risk assessment
**Framework:** FAIR-derived scoring — Risk = Probability × Impact

---

## Scoring Formula

```
Vendor Risk Score (0–100) = (Inherent Risk × 0.40) + (Control Effectiveness × 0.35) + (Business Criticality × 0.25)
```

### Component 1: Inherent Risk (0–100)

Based on the nature of data access and service:

| Factor | Weight | Scoring |
|--------|--------|---------|
| Data Classification | 50% | L1=10, L2=25, L3=50, L4=100 |
| Data Volume | 30% | <1K records=10, 1K-100K=30, 100K-1M=50, >1M=80, Unlimited=100 |
| Regulatory Impact | 20% | None=0, Low=20, Medium=50, High=80, Critical=100 |

### Component 2: Control Effectiveness (0–100)

Based on assessment results:

| Source | Weight | Scoring |
|--------|--------|---------|
| SIG Score | 40% | (<2.0)=100, (2.0–2.9)=70, (3.0–3.9)=40, (4.0–5.0)=10 |
| SOC 2 Opinion | 30% | Unqualified=10, Qualified=40, Adverse=80, No SOC 2=100 |
| Pentest Findings | 20% | None=0, Low=20, Medium=50, High=80, Critical=100 |
| Past Incidents (2yr) | 10% | 0=0, 1=30, 2=50, 3+=100 |

### Component 3: Business Criticality (0–100)

| Factor | Weight | Scoring |
|--------|--------|---------|
| Revenue Impact | 40% | None=0, <$10K/hr=20, $10-100K=50, $100K-1M=70, >$1M=100 |
| Replacement Difficulty | 30% | Easy=10, Moderate=30, Difficult=50, Very difficult=80, No alternative=100 |
| Integration Depth | 30% | Standalone=10, API integration=30, Deep integration=60, Critical dependency=100 |

---

## Risk Score Bands

| Score | Rating | Action Required |
|-------|--------|----------------|
| 0–20 | Low | Standard monitoring, annual review |
| 21–40 | Medium | Semi-annual review, specific gap remediation |
| 41–60 | High | Quarterly review, remediation plan within 90 days |
| 61–80 | Critical | Monthly review, immediate remediation, CISO oversight |
| 81–100 | Unacceptable | Termination plan triggered — find alternative vendor |

---

## Sample Scoring — Critical Tier Vendors

### Vendor: AWS

| Component | Factor | Score | Weighted |
|-----------|--------|-------|----------|
| Inherent Risk | Data L4=100, Volume=Unlimited=100, Regulatory=Critical=100 | 100 | 40.0 |
| Control Effectiveness | SIG=4.5→10, SOC2=Unqualified=10, Pentest=None→0, Incidents=0→0 | 8 | 2.8 |
| Business Criticality | Revenue=$480K/hr→70, Replacement=Very Difficult=80, Depth=Critical=100 | 81 | 20.3 |
| **Total Score** | | | **63.1** |

**Rating:** Critical (61–80)
**Action:** Monthly review, CISO oversight, maintain close relationship

### Vendor: Calendly (Low tier)

| Component | Factor | Score | Weighted |
|-----------|--------|-------|----------|
| Inherent Risk | Data L1=10, Volume=<1K=10, Regulatory=None=0 | 8 | 3.2 |
| Control Effectiveness | SIG=N/A (not assessed), Default Low tier score | 20 | 7.0 |
| Business Criticality | Revenue=None=0, Replacement=Easy=10, Depth=Standalone=10 | 6 | 1.5 |
| **Total Score** | | | **11.7** |

**Rating:** Low (0–20)
**Action:** Standard monitoring, contractual clauses only

---

## Vendor Portfolio Risk Distribution

Based on initial scoring of all 31 vendors:

| Rating | Count | % of Portfolio | Action Priority |
|--------|-------|---------------|----------------|
| Low (0–20) | 14 | 45% | Routine |
| Medium (21–40) | 10 | 32% | Standard |
| High (41–60) | 4 | 13% | Monitor |
| Critical (61–80) | 3 | 10% | Active management |
| Unacceptable (81+) | 0 | 0% | — |

---

## Scoring Cadence

| Trigger | Action |
|---------|--------|
| Initial assessment | Score calculated from assessment results |
| Quarterly | Automated score update (breach feeds, financial health) |
| Annual | Full re-assessment (refresh SIG, SOC 2, pentest) |
| Incident | Immediate score impact (add incident score) |
| Contract change | Re-calculate business criticality scores |
