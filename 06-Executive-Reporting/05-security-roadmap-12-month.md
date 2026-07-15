# Security Program Roadmap — 12-Month Plan

**Phase:** 6 — Executive Reporting & KRIs
**Objective:** Define the 12-month security program roadmap with milestones, owners, and success criteria
**Audience:** Board of Directors, CISO, Executive Leadership

---

## Roadmap Overview

```
Q1 2026          Q2 2026          Q3 2026          Q4 2026          Q1 2027
│                │                │                │                │
├─FOUNDATION─────┼─BUILD──────────┼─OPERATIONALIZE──┼─OPTIMIZE───────┼─SUSTAIN───►
│                │                │                │                │
│ Risk Assess    │ HSM Deploy     │ SIEM Tuning    │ DR Test Pass   │ SOC 2 Audit │
│ Policies       │ DR Infra       │ Auto Access    │ All KRIs at    │ Continuous  │
│ BCP/DR Plans   │ Vendor Assess  │ EDR Full       │ Target         │ Improv.     │
│ Awareness      │ MFA Hardware   │ Deployment     │ Vendor Program │            │
│ Vendor Tiering │ Pentest        │ 2nd TTX        │ Maturity 2.8   │            │
└────────────────┴────────────────┴────────────────┴────────────────┴────────────►
```

---

## Quarterly Milestones

### Q1 — Foundation (Complete)

| # | Milestone | Status | Owner |
|---|-----------|--------|-------|
| M-01 | Crown jewels analysis | Done | CISO |
| M-02 | Risk register with FAIR quantification | Done | CISO |
| M-03 | Board heatmap presentation | Done | CISO |
| M-04 | Security policy framework (12 policies) | Done | CISO |
| M-05 | NIST CSF control mapping | Done | CISO |
| M-06 | BIA and BCP/DR plans drafted | Done | CISO |
| M-07 | Tabletop exercise conducted | Done | CISO |
| M-08 | Security awareness program launched | Done | CISO |
| M-09 | Vendor tiering completed | Done | CISO |
| M-10 | KRI dashboard defined | Done | CISO |

### Q2 — Build (In Progress)

| # | Milestone | Due | Owner | Success Criteria |
|---|-----------|-----|-------|-----------------|
| M-11 | HSM deployment for payment keys | May | CTO | HSM operational, keys migrated, Vault HSM integration tested |
| M-12 | Cross-region DR infrastructure provisioned | May | CTO | Terraform deploys full T1 stack in us-west-2, smoke test passes |
| M-13 | Critical vendor assessments complete | May | Security | All 6 Critical vendors assessed, scores in register |
| M-14 | Hardware MFA tokens (FIDO2) for Finance | April | CTO | 20 tokens deployed, tested with Okta |
| M-15 | External penetration test | June | CISO | Full-scope pentest completed, findings remediated within SLA |
| M-16 | DR technical test — T1 systems | June | CTO | All T1 systems restored in DR region within RTO |
| M-17 | Vendor risk scoring operational | June | Security | Scoring algorithm implemented, all 31 vendors scored |

### Q3 — Operationalize

| # | Milestone | Due | Owner | Success Criteria |
|---|-----------|-----|-------|-----------------|
| M-18 | SIEM exfiltration detection rules | July | Security | 100% coverage of exfiltration scenarios, zero false positives |
| M-19 | Automated privileged access reviews | August | CTO | Quarterly reviews automated, 100% completion rate |
| M-20 | EDR full deployment (all endpoints) | August | CTO | 200 endpoints protected, 100% reporting to console |
| M-21 | Second tabletop exercise (cloud provider failure) | September | CISO | Tabletop completed, findings remediated |
| M-22 | Phishing click rate ≤10% | September | CISO | Q3 campaign results confirm |
| M-23 | Phishing report rate ≥40% | September | CISO | Q3 campaign results confirm |

### Q4 — Optimize

| # | Milestone | Due | Owner | Success Criteria |
|---|-----------|-----|-------|-----------------|
| M-24 | Full DR test — all systems | October | CTO | All T1–T3 systems restored within RTO |
| M-25 | Access review compliance 100% | October | CTO | All quarterly reviews completed on time |
| M-26 | Vendor risk program fully operational | November | CISO | All assessments current, monitoring active |
| M-27 | All KRIs at target | December | CISO | See KRI dashboard targets |
| M-28 | Phishing click rate ≤5% | December | CISO | Q4 campaign results confirm |
| M-29 | Security maturity Level 2.8 | December | CISO | CMMI assessment validates |
| M-30 | Training completion 100% | December | CISO | LMS completion records |
| M-31 | SOC 2 Type II readiness assessment | December | CISO | Pre-audit assessment clean |

### Q1 2027 — Sustain

| # | Milestone | Due | Owner |
|---|-----------|-----|-------|
| M-32 | SOC 2 Type II audit engagement | January | CISO |
| M-33 | Annual risk assessment refresh | January | CISO |
| M-34 | Annual policy review cycle | January | CISO |
| M-35 | Roadmap refresh for Year 2 | February | CISO |

---

## Resource Requirements

| Quarter | People | Tools | External Services | Total |
|---------|--------|-------|-------------------|-------|
| Q1 | $37,500 | $85,000 | $25,000 | $147,500 |
| Q2 | $37,500 | $60,000 | $30,000 | $127,500 |
| Q3 | $37,500 | $40,000 | $10,000 | $87,500 |
| Q4 | $37,500 | $20,000 | $10,000 | $67,500 |
| **Total** | **$150,000** | **$205,000** | **$75,000** | **$520,000** |

---

## Risk to Roadmap

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| CTO bandwidth — competing product priorities | DR and HSM delayed | Medium | Dedicated DevOps resource for infra projects |
| Budget overrun on tooling | Tool spend exceeds allocation | Low | Open-source alternatives evaluated (Wazuh, Grafana) |
| SOC 2 timeline slips | Certification delayed to Q3 2027 | Low | Pre-audit assessment in Q4 identifies gaps early |
| Key person departure | Program velocity drops | Medium | Cross-training in progress, documentation complete |
