# NIST CSF 2.0 Control Mapping

**Phase:** 2 — Security Policy Framework
**Objective:** Map all 12 security policies to NIST Cybersecurity Framework 2.0 functions, categories, and subcategories

---

## Mapping Legend

- **P** — Primary coverage (policy directly addresses this subcategory)
- **S** — Secondary coverage (policy partially or indirectly addresses this subcategory)
- **—** — Not covered by policy framework (covered by other programs)

---

## Govern (GV) — New CSF 2.0 Function

| Subcategory | Description | Primary Policy | Coverage |
|-------------|-------------|----------------|----------|
| GV.OC | Organizational Context | POL-01 — Information Security | P |
| GV.RM | Risk Management Strategy | POL-01 — Information Security | P |
| GV.RA | Roles, Responsibilities | All policies (Each defines roles) | P |
| GV.SC | Supply Chain Risk Management | POL-10 — Vendor Management | P |
| GV.PO | Policy & Oversight | POL-01 — Information Security | P |
| GV.OV | Oversight | POL-01 — Information Security | S |

---

## Identify (ID)

| Category | Subcategory | Primary Policy | Coverage |
|----------|-------------|----------------|----------|
| ID.AM | Asset Management | POL-07 — Operations Security | P |
| ID.AM-01 | Asset inventory | POL-07 (Section 2.2) | P |
| ID.AM-02 | Ownership | POL-01 (Section 4) | P |
| ID.AM-03 | Data classification | POL-03 — Data Classification | P |
| ID.AM-04 | Systems & services | POL-07 (Section 2.2) | P |
| ID.RA | Risk Assessment | POL-01 (Section 3.2) | P |
| ID.RA-01 | Risk identification | POL-01 (Section 3.2) | P |
| ID.RA-02 | Threat intelligence | POL-08 (Section 4.2) | S |
| ID.RA-03 | Risk analysis | POL-01 (Section 3.2) | P |
| ID.RA-04 | Risk prioritization | POL-01 (Section 3.2) | P |
| ID.RA-05 | Risk register | POL-01 (Section 3.2) | P |
| ID.RM | Risk Management Strategy | POL-01 (Section 3.2) | P |
| ID.IM | Improvement | POL-08 (Section 4.6) | S |
| ID.SC | Supply Chain Risk Management | POL-10 — Vendor Management | P |

---

## Protect (PR)

| Category | Subcategory | Primary Policy | Coverage |
|----------|-------------|----------------|----------|
| PR.AC | Access Control | POL-04 — Access Control | P |
| PR.AC-01 | Identity management | POL-04 (Section 3.1) | P |
| PR.AC-02 | Authentication | POL-04 (Section 3.2) | P |
| PR.AC-03 | Authorization | POL-04 (Section 3.3) | P |
| PR.AC-04 | Privileged access | POL-04 (Section 3.4) | P |
| PR.AC-05 | Remote access | POL-04 (Section 3.7), POL-11 | P |
| PR.AC-06 | Access reviews | POL-04 (Section 3.5) | P |
| PR.DS | Data Security | POL-03 — Data Classification | P |
| PR.DS-01 | Data at rest | POL-05 — Cryptography | P |
| PR.DS-02 | Data in transit | POL-05 — Cryptography | P |
| PR.DS-03 | Data classification | POL-03 | P |
| PR.DS-04 | Data handling | POL-03 | P |
| PR.DS-05 | Data disposal | POL-03 (Section 4.5) | P |
| PR.AT | Awareness & Training | POL-01 (Section 3.8) | P |
| PR.AT-01 | Security awareness | POL-01 (Section 3.8) | P |
| PR.AT-02 | Role-based training | POL-01 (Section 3.8) | S |
| PR.PS | Platform Security | POL-07 — Operations Security | P |
| PR.PS-01 | Configuration management | POL-07 (Section 2.2) | P |
| PR.PS-02 | Patch management | POL-07 (Section 2.3), POL-12 | P |
| PR.PS-03 | Malware protection | POL-07 (Section 2.6) | P |
| PR.PS-04 | Backups | POL-07 (Section 2.4) | P |
| PR.PS-05 | Physical security | POL-06 — Physical Security | P |
| PR.IR | Technology Infrastructure Resilience | POL-09 — Business Continuity | P |

---

## Detect (DE)

| Category | Subcategory | Primary Policy | Coverage |
|----------|-------------|----------------|----------|
| DE.CM | Continuous Monitoring | POL-07 (Section 2.5) | P |
| DE.CM-01 | Network monitoring | POL-07 (Section 2.5) | P |
| DE.CM-02 | Physical monitoring | POL-06 (Section 3.2) | P |
| DE.CM-03 | Personnel activity | POL-04 (Section 3.5), POL-07 (2.5) | S |
| DE.CM-04 | Malware detection | POL-07 (Section 2.6) | P |
| DE.CM-05 | Vulnerability scanning | POL-12 | P |
| DE.CM-06 | Service monitoring | POL-07 (Section 2.8) | S |
| DE.AE | Adverse Event Analysis | POL-08 (Section 4.3) | P |
| DE.AE-01 | Alert triage | POL-08 (Section 4.3) | P |

---

## Respond (RS)

| Category | Subcategory | Primary Policy | Coverage |
|----------|-------------|----------------|----------|
| RS.MA | Incident Management | POL-08 — Incident Response | P |
| RS.MA-01 | Incident response plan | POL-08 (Section 4) | P |
| RS.MA-02 | IR plan execution | POL-08 (Section 4) | P |
| RS.MA-03 | Communication | POL-08 (Section 5) | P |
| RS.MA-04 | Analysis | POL-08 (Section 4.3) | P |
| RS.MA-05 | Mitigation | POL-08 (Section 4.4) | P |
| RS.MA-06 | Recovery | POL-08 (Section 4.5) | P |
| RS.IM | Improvements | POL-08 (Section 4.6) | P |

---

## Recover (RC)

| Category | Subcategory | Primary Policy | Coverage |
|----------|-------------|----------------|----------|
| RC.RP | Recovery Planning | POL-09 — Business Continuity | P |
| RC.RP-01 | Recovery plan | POL-09 (Section 2.4) | P |
| RC.IM | Improvements | POL-09 (Section 2.5) | P |
| RC.CO | Communications | POL-08 (Section 5) | S |

---

## Coverage Summary

| Function | Subcategories | Covered (P) | Partial (S) | Not Covered |
|----------|---------------|-------------|--------------|-------------|
| Govern (GV) | 6 | 5 | 1 | 0 |
| Identify (ID) | 10 | 8 | 2 | 0 |
| Protect (PR) | 17 | 16 | 1 | 0 |
| Detect (DE) | 7 | 5 | 2 | 0 |
| Respond (RS) | 7 | 7 | 0 | 0 |
| Recover (RC) | 3 | 2 | 1 | 0 |
| **Total** | **50** | **43 (86%)** | **7 (14%)** | **0** |
