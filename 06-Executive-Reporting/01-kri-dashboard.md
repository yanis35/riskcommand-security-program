# KRI Dashboard — Key Risk Indicators

**Phase:** 6 — Executive Reporting & KRIs
**Objective:** Define and track Key Risk Indicators (KRIs) for the security program
**Tool:** Datadog / Grafana dashboard (board-ready)
**Review Cadence:** Monthly (Security Team), Quarterly (Board)

---

## KRI Definitions

| KRI ID | KRI Name | Formula | Target | Warning | Critical | Frequency |
|--------|----------|---------|--------|---------|----------|-----------|
| KRI-01 | Patch Compliance | % of critical patches applied within SLA (7 days) | ≥95% | <90% | <80% | Weekly |
| KRI-02 | Phishing Click Rate | % of users who clicked simulated phish in most recent wave | ≤5% | >10% | >20% | Quarterly |
| KRI-03 | Open Critical Vulnerabilities | Count of CVSS 9+ vulnerabilities past SLA | 0 | 1–3 | >3 | Weekly |
| KRI-04 | Mean Time to Detect (MTTD) | Average hours to detect a confirmed security incident | ≤1 hr | >4 hrs | >24 hrs | Per incident |
| KRI-05 | Mean Time to Respond (MTTR) | Average hours to contain a confirmed incident | ≤4 hrs | >8 hrs | >24 hrs | Per incident |
| KRI-06 | Vendor Risk Score (Avg) | Average risk score across all Critical-tier vendors | <40 | 40–60 | >60 | Quarterly |
| KRI-07 | Access Review Compliance | % of scheduled access reviews completed on time | 100% | <95% | <90% | Monthly |
| KRI-08 | Security Training Completion | % of employees who completed annual training | 100% | <95% | <90% | Monthly |
| KRI-09 | Phishing Report Rate | % of simulated emails reported by users | ≥50% | <30% | <15% | Quarterly |
| KRI-10 | DR Test Success Rate | % of DR tests meeting RTO/RPO targets | 100% | <90% | <80% | Per test |

---

## KRI Dashboard — Monthly View (Month 2 Example)

```
KRI Dashboard ─ Month 2 2026                      Status
──────────────────────────────────────────────────────────
KRI-01 Patch Compliance            ████████████░░   92%  🟡
KRI-02 Phishing Click Rate         █████████████    27%  🔴
KRI-03 Open Critical Vulns         ██░░░░░░░░░░░    2    🟡
KRI-04 MTTD                        █████████░░░░   2.5h  🟡
KRI-05 MTTR                        ████████░░░░░░   6h   🟡
KRI-06 Vendor Risk Score (Avg)     █████████████   48    🟡
KRI-07 Access Review Compliance    ██████████░░░░   83%  🔴
KRI-08 Training Completion         ██████████████   94%  🟡
KRI-09 Phishing Report Rate        █████░░░░░░░░░   12%  🔴
KRI-10 DR Test Success Rate        N/A (first test in Q2)

Legend: 🟢 On Target  🟡 Warning  🔴 Critical
```

---

## KRI Trend — Quarterly Comparison

| KRI | Q1 | Q2 (Proj) | Q3 (Proj) | Q4 (Target) |
|-----|-----|-----------|-----------|-------------|
| Patch Compliance | 92% | 93% | 95% | **95%** |
| Phishing Click Rate | 27.3% | 18% | 10% | **5%** |
| Open Critical Vulns | 2 | 0 | 0 | **0** |
| MTTD | 2.5 hrs | 1.5 hrs | 1 hr | **≤1 hr** |
| MTTR | 6 hrs | 4 hrs | 3 hrs | **≤4 hrs** |
| Vendor Risk Score | 48 | 42 | 38 | **<40** |
| Access Review Compliance | 83% | 90% | 95% | **100%** |
| Training Completion | 94% | 96% | 98% | **100%** |
| Report Rate | 12% | 25% | 40% | **50%** |

---

## KRI Status Summary

| Status | Count | KRIs |
|--------|-------|------|
| 🟢 On Target | 0 | — |
| 🟡 Warning | 6 | KRI-01, KRI-03, KRI-04, KRI-05, KRI-06, KRI-08 |
| 🔴 Critical | 3 | KRI-02, KRI-07, KRI-09 |
| N/A | 1 | KRI-10 |

---

## KRI Escalation Thresholds

When a KRI enters Critical status:

| KRI | Escalation Path | Remediation Expectation |
|-----|----------------|------------------------|
| KRI-02 (Click Rate) | CISO → VP Eng/Finance | Enhanced training, targeted coaching |
| KRI-07 (Access Review) | CISO → CTO → HR | Complete all overdue reviews within 7 days |
| KRI-09 (Report Rate) | CISO → All managers | Phish Alert Button campaign + incentives |
