# Wave 3 — CEO Impersonation (BEC) Campaign Results

**Phase:** 4 — Security Awareness & Phishing Program
**Campaign:** Q1 Wave 3 — Business Email Compromise (BEC)
**Date:** March 2026
**Template:** "URGENT: Wire transfer needed before EOD" — CEO impersonation targeting finance team
**Targeting:** Finance + Accounting (12), Executives (8), High-risk Engineering (6) = 26 targeted users

---

## Campaign Statistics (Targeted Users Only)

| Metric | Result |
|--------|--------|
| Emails sent (targeted) | 26 |
| Emails delivered | 26 |
| Emails opened | 21 (80.8%) |
| Links clicked | 8 (30.8%) |
| Credentials submitted | 3 (11.5%) — credential harvest page used |
| Reported (Phish Alert) | 6 (23.1%) |
| Emails forwarded to colleagues | 4 (15.4%) — indicates high believability |

---

## Results by Role

| Role | Sent | Clicked | Click Rate | Submitted Creds | Reported |
|------|------|---------|------------|-----------------|----------|
| CFO | 1 | 0 | 0% | 0 | 1 |
| VP Finance | 1 | 0 | 0% | 0 | 1 |
| Finance Director | 1 | 1 | 100% | 0 | 0 |
| AP Staff (3) | 3 | 3 | 100% | 2 | 0 |
| Accounting (5) | 5 | 2 | 40% | 1 | 1 |
| CEO | 1 | 0 | 0% | 0 | 0 |
| CTO | 1 | 0 | 0% | 0 | 1 |
| Other Execs (6) | 6 | 1 | 16.7% | 0 | 2 |
| High-Risk Engineers (6) | 6 | 1 | 16.7% | 0 | 1 |
| **Total** | **26** | **8** | **30.8%** | **3** | **6** |

---

## Critical Findings

1. **100% of AP staff clicked and 67% submitted credentials** — this is the most dangerous finding of the entire program. AP staff are the direct target of real BEC attacks.
2. **3 credentials captured** — these were immediately reset (by design). In a real attack, these credentials would enable wire fraud.
3. **80.8% open rate** — the BEC pretext was highly convincing. The CEO name + urgency + authority created strong emotional pressure.
4. **15.4% forwarded to colleagues** — users who didn't click still forwarded the email, amplifying the attack. In a real scenario, forwarding spreads the phish.
5. **Senior finance leadership (CFO, VP Finance) detected and reported** — training effectiveness at senior levels is strong.

---

## Real-World Impact Simulation

If this had been a real BEC attack:
- **3 compromised credentials** → attacker accesses email → identifies active deals/clients → intercepts invoices
- **Potential wire fraud loss:** AP staff authorized to process wires up to $50K → 3 staff × $50K = $150K potential loss
- **Time to detection:** If unreported for >24 hours (as is typical for BEC), funds are likely unrecoverable
- **Estimated real-world ALE from BEC:** $450K/year (based on 3 successful BEC scenarios/year)

---

## Immediate Actions

| Action | Owner | Due |
|--------|-------|-----|
| Reset passwords for 3 users who submitted credentials | CTO | Immediate |
| Re-enroll MFA for 3 affected users | CTO | Immediate |
| Require BEC-specific training for ALL finance personnel | Security Team | 7 days |
| Implement mandatory out-of-band verification for wire transfers >$5K | CFO | 14 days |
| Add "Finance" tag to SIEM for enhanced email monitoring | Security Team | 7 days |
| Deploy BEC detection rules in email security gateway | DevOps | 30 days |
| Escalate AP staff performance to Finance Director for performance plan | HR | 14 days |

---

## Quarterly Trend

| Wave | Click Rate | Report Rate | Credential Submission |
|------|------------|-------------|----------------------|
| W1 — Generic | 27.3% | 6.1% | N/A |
| W2 — Spear | 30.7% | 11.6% | N/A |
| W3 — BEC | 30.8% | 23.1% | 11.5% |

**Trend:** Click rate is leveling (good — indicates training is preventing increase). Report rate is improving (excellent). BEC credential submission is a concern that requires technical controls (not just training).
