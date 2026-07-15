# Wave 4 — Credential Harvest Campaign Results

**Phase:** 4 — Security Awareness & Phishing Program
**Campaign:** Q1 Wave 4 — Credential Harvest (Cloned Okta Login Page)
**Date:** April 2026
**Template:** "Suspicious login attempt — verify your account" with cloned Okta login page
**Targeting:** All 200 employees

---

## Campaign Statistics

| Metric | Result |
|--------|--------|
| Emails sent | 200 |
| Emails delivered | 198 |
| Emails opened | 134 (67.7%) |
| Links clicked | 89 (44.9%) |
| **Credentials submitted** | **47 (23.7%)** |
| MFA code entered (simulated) | 31 (15.7% of all users, 65.9% of credential submitters) |
| Reported (Phish Alert) | 19 (9.6%) |
| Mean time to credential submission | 1.8 hours |

---

## Critical Analysis

**23.7% of all employees submitted their credentials** to a convincing but fake login page. This is the most important metric of the entire program — credential submission on a cloned login page is the strongest predictor of real-world compromise risk.

**65.9% of credential submitters also entered a simulated MFA code** — indicating attackers could bypass MFA in a real attack (MFA fatigue / real-time proxy attack).

**Report rate dropped to 9.6%** compared to Wave 3's 23.1% — the pretext ("verify your account") is highly effective because it preys on users' fear of losing access.

---

## Results by Department

| Department | Sent | Clicked | Click Rate | Creds Submitted | Submit Rate | Reported |
|------------|------|---------|------------|-----------------|-------------|----------|
| Finance & Accounting | 12 | 9 | 75.0% | 7 | 58.3% | 1 |
| Executives & Board | 8 | 4 | 50.0% | 2 | 25.0% | 2 |
| Engineering (privileged) | 35 | 12 | 34.3% | 5 | 14.3% | 5 |
| Customer Support | 25 | 16 | 64.0% | 11 | 44.0% | 1 |
| Engineering (non-privileged) | 20 | 7 | 35.0% | 3 | 15.0% | 3 |
| Sales & Marketing | 40 | 22 | 55.0% | 11 | 27.5% | 3 |
| Operations & Admin | 30 | 13 | 43.3% | 6 | 20.0% | 2 |
| Contractors & Interns | 30 | 6 | 20.0% | 2 | 6.7% | 2 |
| **Total** | **200** | **89** | **44.9%** | **47** | **23.7%** | **19** |

---

## Risk Classification by Department

| Department | Cred Submit Rate | Data Access Risk | Overall Risk |
|------------|-----------------|-----------------|--------------|
| Finance | 58.3% | Wire transfer, payroll | Critical |
| Customer Support | 44.0% | PII access | Critical |
| Sales & Marketing | 27.5% | Customer data | High |
| Executives | 25.0% | Strategic data | High |
| Operations | 20.0% | Internal data | Medium |
| Engineering | 14.6% | Source code, prod | Medium |
| Contractors | 6.7% | Limited | Low |

---

## MFA Simulation Results

| Group | Creds + MFA Submitted | % of Submitters |
|-------|----------------------|-----------------|
| All submitters | 31 of 47 | 65.9% |
| Finance | 6 of 7 | 85.7% |
| Customer Support | 9 of 11 | 81.8% |
| Engineering | 5 of 8 | 62.5% |
| Sales & Marketing | 7 of 11 | 63.6% |

**Takeaway:** 66% of users who submitted credentials also entered a fake MFA code. This confirms that MFA alone is not sufficient defense against real-time proxy attacks (e.g., EvilGinx). Training + hardware MFA tokens for high-risk users is recommended.

---

## Cumulative Program Results (Q1)

| Metric | W1 | W2 | W3 | W4 | Q1 Average |
|--------|-----|-----|-----|-----|------------|
| Open rate | 38.4% | 56.3% | 80.8% | 67.7% | 60.8% |
| Click rate | 27.3% | 30.7% | 30.8% | 44.9% | 33.4% |
| Credential submission | N/A | N/A | 11.5% | 23.7% | 17.6% |
| Report rate | 6.1% | 11.6% | 23.1% | 9.6% | 12.6% |
| Repeat clicker rate | — | 68.9% | — | — | 42.1% |

---

## Q1 Training Completion

| Training Module | Enrolled | Completed | Completion Rate |
|----------------|----------|-----------|-----------------|
| Phishing Awareness (15-min) | 89 | 85 | 95.5% |
| Advanced Phishing (45-min) | 42 | 38 | 90.5% |
| BEC-Specific (Finance) | 12 | 12 | 100% |
| 1-on-1 Coaching | 16 | 14 | 87.5% |
| **Total** | **159** | **149** | **93.7%** |

---

## Q2 Campaign Plan (Adjustments Based on Q1 Data)

| Change | Rationale |
|--------|-----------|
| Increase frequency for Finance — monthly instead of quarterly | Finance is highest risk (58.3% cred submit rate) |
| Deploy hardware MFA tokens for Finance + Critical roles | MFA bypass risk confirmed (66% entered fake MFA code) |
| Implement FIDO2/WebAuthn for privileged users | Phishing-resistant authentication |
| Add BEC detection rules to email security gateway | 3 credential captures in Wave 3 — real attack risk |
| Launch "Security Champion" program for reporters | Incentivize reporting behavior |
| Quarterly BEC simulation for Finance only | High-impact, high-frequency |
