# CMMI Maturity Scorecard — Security Program

**Phase:** 6 — Executive Reporting & KRIs
**Objective:** Assess security program maturity using CMMI levels mapped to NIST CSF 2.0 functions
**Framework:** CMMI (Capability Maturity Model Integration) v2.0
**Assessment Method:** Self-assessment (annual), Third-party validation (SOC 2)

---

## CMMI Maturity Levels

| Level | Label | Description |
|-------|-------|-------------|
| 0 | Incomplete | Process is not performed or does not achieve its purpose |
| 1 | Initial | Process is performed ad-hoc, often reactive, success depends on individual effort |
| 2 | Managed | Process is planned, monitored, and controlled; stakeholders are identified |
| 3 | Defined | Process is standardized across the organization; tailored from organizational standards |
| 4 | Quantitatively Managed | Process is measured and controlled using statistical and quantitative techniques |
| 5 | Optimizing | Process is continuously improved through quantitative feedback and innovation |

---

## Current Maturity Assessment (Month 2)

| NIST CSF Function | Category | CMMI Level | Target (Year 1) | Gap |
|-------------------|----------|-------------|-----------------|-----|
| **Govern (GV)** | | | | |
| | Organizational Context (GV.OC) | 2 | 3 | Policy approved, operating model defined |
| | Risk Management (GV.RM) | 2 | 3 | Risk register established, monthly review |
| | Policy (GV.PO) | 3 | 3 | Complete policy framework published |
| | Supply Chain (GV.SC) | 1 | 2 | Vendor tiering done, assessments in progress |
| **Identify (ID)** | | | | |
| | Asset Management (ID.AM) | 2 | 3 | Inventory exists, CMDB being deployed |
| | Risk Assessment (ID.RA) | 3 | 4 | FAIR quantification completed, quarterly updates |
| | Improvement (ID.IM) | 1 | 2 | No formal improvement process yet |
| **Protect (PR)** | | | | |
| | Access Control (PR.AC) | 2 | 3 | RBAC defined, JIT being rolled out |
| | Data Security (PR.DS) | 2 | 3 | Classification published, encryption standards defined |
| | Awareness & Training (PR.AT) | 2 | 3 | Program launched, first campaigns complete |
| | Platform Security (PR.PS) | 1 | 2 | Patch management defined, automated scanning in deployment |
| | Technology Resilience (PR.IR) | 1 | 2 | BCP/DR plans drafted, not yet tested |
| **Detect (DE)** | | | | |
| | Continuous Monitoring (DE.CM) | 2 | 3 | SIEM deployed, alerting configured |
| | Adverse Event Analysis (DE.AE) | 2 | 3 | Incident classification defined, triage in place |
| **Respond (RS)** | | | | |
| | Incident Management (RS.MA) | 2 | 3 | IR plan published, tabletop exercise done |
| | Improvements (RS.IM) | 1 | 2 | No post-incident improvement process |
| **Recover (RC)** | | | | |
| | Recovery Planning (RC.RP) | 1 | 2 | DR plans drafted, not tested |
| | Communications (RC.CO) | 1 | 2 | Crisis comms drafted, templates in progress |

---

## Maturity Scorecard (Visual)

```
Function:     CMMI Current  Target   ▲ Goal
────────────────────────────────────────────
Govern          ██░░ 2.1     3.0     ███████
Identify        ██░░ 2.1     3.3     ████████
Protect         █░░░ 1.7     2.8     ███████
Detect          ██░░ 2.0     3.0     ███████
Respond         ██░░ 1.5     2.5     ██████
Recover         █░░░ 1.0     2.0     █████

────────────────────────────────────────────
Overall         ██░░ 1.8     2.8     ██████
```

**Current overall maturity: Level 1.8 (between Initial and Managed)**
**Year 1 target: Level 2.8 (approaching Defined)**

---

## Maturity Improvement Roadmap

| Quarter | Target Level | Key Initiatives |
|---------|--------------|-----------------|
| Q1 — Baseline | 1.8 | Policy framework published, risk register created, awareness program launched |
| Q2 | 2.2 | DR tested, vendor assessments complete, SIEM tuning done, all KRIs measured |
| Q3 | 2.5 | JIT access enforced, hardware MFA deployed, access reviews automated |
| Q4 | 2.8 | DR test successful, vendor program operational, all KRIs at target |
| Year 2 | 3.5 | Quantitatively managed — measurements drive decisions |
| Year 3 | 4.0 | Optimizing — continuous improvement culture |

---

## Key Maturity Gaps

| Gap | Impact | Remediation | Timeline |
|-----|--------|-------------|----------|
| PR.IR — Technology Resilience at L1 | No tested DR capability → RTO at risk | Complete DR test (Phase 3) | Q2 |
| GV.SC — Supply Chain at L1 | Vendor risk is unmanaged | Complete all Critical vendor assessments | Q2 |
| ID.IM — Improvement at L1 | No process to learn from incidents | Post-incident review process | Q3 |
| RC.RP — Recovery at L1 | Recovery plans untested | DR tabletop + technical test | Q2 |
| RS.IM — Respond Improvements at L1 | Incident lessons not captured | IR after-action report process | Q3 |
