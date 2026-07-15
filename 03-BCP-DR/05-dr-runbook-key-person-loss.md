# DR Runbook — Key Person Loss

**Phase:** 3 — BCP/DR with Tested Runbooks
**Scenario:** Unexpected loss of a critical team member (resignation, medical, or other absence)
**Objective:** Ensure business continuity by transferring knowledge, access, and responsibilities to backup personnel
**RTO Target:** ≤24 hours for critical knowledge transfer

---

## Key Person Inventory

| Role | Person | Critical Knowledge | Backup(s) | Cross-Trained? |
|------|--------|-------------------|-----------|----------------|
| CTO | Confidential | AWS architecture, payment infrastructure, Vault management, vendor relationships | VP Eng, Sr. DevOps | Partial |
| Database Administrator | Confidential | RDS configuration, cross-region replication, backup/restore procedures | DevOps (2) | Partial |
| Lead ML Engineer | Confidential | Fraud detection models, training pipeline, model deployment | ML Eng (1) | No |
| Security Engineer | Confidential | SIEM configuration, EDR management, incident response procedures | CISO | Partial |

---

## Immediate Actions (First 24 Hours)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 1 | Confirm the person's absence and expected duration | HR / Manager | 1 hour |
| 2 | Identify the most critical pending items that require the absent person's knowledge | Manager | 2 hours |
| 3 | Access the person's documentation: runbooks, architecture docs, passwords (if approved) | Manager + Security | 2 hours |
| 4 | Reset all shared passwords/keys known to the absent person (if unplanned absence) | DevOps | 4 hours |
| 5 | Revoke the person's access: disable accounts, rotate personal API keys, revoke VPN certs | DevOps + Security | 2 hours |
| 6 | Review the person's calendar for pending deadlines, meetings, commitments | Manager | 1 hour |
| 7 | Assign a backup person to cover critical responsibilities | CTO / VP | 2 hours |

---

## Knowledge Transfer Plan

| Knowledge Area | Documentation Location | Transfer Method | Backup Person | Target Date |
|---------------|-----------------------|-----------------|---------------|-------------|
| AWS Architecture | Confluence: AWS Architecture Overview | Pairing sessions + recorded walkthrough | VP Eng | 1 week |
| RDS Management | Runbook: Database Operations | Hands-on restore test + recorded session | DevOps Lead | 1 week |
| Vault Administration | Runbook: Vault Operations | Pairing + failover test | DevOps Lead | 2 weeks |
| ML Model Pipeline | Confluence: ML Ops | Code review + deploy test | ML Eng 2 | 2 weeks |
| Incident Response | IR Playbook (documented) | Tabletop exercise | Security Eng 2 | 1 month |
| Vendor Relationships | Vendor Register + Contract Database | Account handoff calls | CTO | 2 weeks |

---

## Long-Term Actions (30–90 Days)

| Action | Owner | Timeline |
|--------|-------|----------|
| Begin recruitment for the role (if permanent loss) | HR | Within 1 week |
| Complete full knowledge transfer and cross-training | Backup person | 30 days |
| Update all runbooks with any undocumented knowledge discovered during transition | Manager | 30 days |
| Review and update key person risk in risk register | CISO | 15 days |
| Schedule quarterly "bus factor" review for all critical roles | CISO | Ongoing |

---

## Preventive Measures

- All critical procedures documented in runbooks (Confluence)
- All infrastructure defined as code (Terraform) — no manual configuration
- Privileged access requires MFA + JIT elevation (no standing admin access)
- Critical roles have at least one cross-trained backup
- Quarterly knowledge sharing sessions for each critical function
- Annual key-person risk assessment as part of BIA review
