# Quarterly Improvement Metrics — Security Awareness Program

**Phase:** 4 — Security Awareness & Phishing Program
**Objective:** Track phishing program effectiveness and user behavior improvement over 4 quarters
**Period:** Q1 2026 (Baseline) → Q4 2026 (Target)
**Audience:** CISO, Board of Directors, Security Team

---

## Executive Summary

The security awareness program launched in Q1 2026 with 4 phishing simulation waves. Baseline metrics indicate the organization is at elevated risk — 27.3% click rate on generic phish and 23.7% credential submission rate on a cloned login page. While these are concerning, they provide clear targets for improvement. The program targets a 5% click rate and 50%+ report rate by Q4 2026.

---

## Phishing Campaign Results — Q1 Baseline

| Metric | W1 (Generic) | W2 (Spear) | W3 (BEC) | W4 (Cred Harvest) | Q1 Avg |
|--------|-------------|------------|----------|-------------------|--------|
| Open rate | 38.4% | 56.3% | 80.8% | 67.7% | 60.8% |
| Click rate | 27.3% | 30.7% | 30.8% | 44.9% | **33.4%** |
| Credential submission | N/A | N/A | 11.5% | 23.7% | **17.6%** |
| Report rate | 6.1% | 11.6% | 23.1% | 9.6% | **12.6%** |
| Mean time to click | 4.2 hrs | 2.8 hrs | 1.5 hrs | 1.8 hrs | 2.6 hrs |

---

## Quarterly Trend Targets

| Metric | Q1 (Actual) | Q2 (Target) | Q3 (Target) | Q4 (Target) |
|--------|-------------|-------------|-------------|-------------|
| Click rate | 33.4% | 18% | 10% | **5%** |
| Credential submission | 17.6% | 8% | 4% | **2%** |
| Report rate | 12.6% | 25% | 40% | **50%** |
| Mean time to click | 2.6 hrs | 4 hrs | 8 hrs | **24 hrs** |
| Repeat clicker rate | 68.9% | 40% | 20% | **5%** |
| Training completion | 93.7% | 95% | 98% | **100%** |

---

## Quarterly Snapshot Dashboard

```
Q1 2026 ──────────────────────────────────────────────────────
Click Rate:     ████████████████████████░░░  33.4% 🟡
Cred Submit:    █████████████░░░░░░░░░░░░░░  17.6% 🔴
Report Rate:    █████████░░░░░░░░░░░░░░░░░░  12.6% 🔴
Training Comp:  █████████████████████████░░░  93.7% 🟢

Q2 2026 Target ───────────────────────────────────────────────
Click Rate:     ████████████░░░░░░░░░░░░░░░  18% 🟡
Cred Submit:    ██████░░░░░░░░░░░░░░░░░░░░░  8% 🟡
Report Rate:    ██████████████████░░░░░░░░░░  25% 🟡
Training Comp:  ██████████████████████████░░  95% 🟢

Q4 2026 Target ───────────────────────────────────────────────
Click Rate:     ████░░░░░░░░░░░░░░░░░░░░░░░  5%  🟢
Cred Submit:    █░░░░░░░░░░░░░░░░░░░░░░░░░░  2%  🟢
Report Rate:    █████████████████████████████  50% 🟢
Training Comp:  █████████████████████████████  100% 🟢
```

---

## Department Comparison — Q1 vs Q4 Target

| Department | Q1 Click Rate | Q4 Target | Risk Level | Focus Area |
|------------|--------------|-----------|------------|------------|
| Finance & Accounting | 50.0% | 5% | Critical | BEC prevention, wire transfer verification |
| Customer Support | 44.0% | 5% | Critical | PII protection, social engineering |
| Sales & Marketing | 32.5% | 5% | High | Credential harvest awareness |
| Operations & Admin | 27.6% | 5% | Medium | General awareness |
| Engineering | 21.8% | 3% | Medium | Secure coding, credential protection |
| Executives & Board | 12.5% | 3% | Low | BEC awareness, reporting culture |
| Contractors & Interns | 20.0% | 5% | Medium | Onboarding training effectiveness |

---

## Training & Remediation Effectiveness

| Intervention | Q1 Users | Recidivism Rate | Notes |
|-------------|----------|----------------|-------|
| 15-min LMS training only | 54 | 68.9% | Training alone is insufficient |
| 1-on-1 coaching | 16 | 31.3% | Coaching significantly reduces recidivism |
| Manager notification | 42 | 45.2% | Manager involvement helps but is not sufficient alone |
| All interventions combined | — | 25.4% (projected) | Combined approach targets <25% recidivism |

---

## Key Insights

1. **Training alone is not enough**: 68.9% of users who completed training clicked again on the next wave. Training must be combined with coaching and technical controls.
2. **Finance will miss Q4 target without technical controls**: No amount of training will prevent all BEC attacks against AP staff. Hardware MFA tokens + out-of-band verification are required.
3. **Report rate improves with cultural reinforcement**: Wave 3 had the highest report rate (23.1%) due to the BEC topic being top-of-mind. Continuous reinforcement (not just training) drives reporting behavior.
4. **Executive engagement is a force multiplier**: When executives model good behavior (reporting, completing training), it drives organization-wide improvement.

---

## Budget & Resource Allocation

| Item | Q1 Spend | Annual Budget |
|------|----------|---------------|
| GoPhish (self-hosted) | $0 (open source) | $0 |
| LMS platform | $3,000 | $12,000 |
| Training content development | $5,000 | $15,000 |
| Hardware MFA tokens (Finance: 20 units) | $0 | $1,000 |
| Security Champions program | $0 | $5,000 (swag + rewards) |
| **Total** | **$8,000** | **$33,000** |

---

## Q2 Program Adjustments

Based on Q1 findings, the Q2 program will:
1. Deploy hardware MFA tokens for Finance team (FIDO2 — phishing-resistant)
2. Increase BEC simulation frequency for Finance from quarterly to monthly
3. Launch "Security Champions" program — 1 champion per department
4. Implement automated training enrollment tied to GoPhish click events
5. Deploy Phish Alert Button for Outlook (one-click reporting)
6. Begin measuring "report rate as a % of all simulated emails" (target: 50% in Q4)
