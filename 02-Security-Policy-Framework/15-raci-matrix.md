# RACI Matrix — Security Policy Framework

**Phase:** 2 — Security Policy Framework
**Objective:** Define roles and responsibilities for policy development, approval, implementation, and enforcement

---

## Legend

- **R** — Responsible (does the work)
- **A** — Accountable (owns the outcome)
- **C** — Consulted (provides input)
- **I** — Informed (receives updates)

---

## Policy Lifecycle RACI

| Activity | CISO | CTO | VP Eng | CFO | Legal | HR | Board | Security Team | Internal Audit |
|----------|------|-----|--------|-----|-------|-----|-------|---------------|----------------|
| Policy Development | R | C | C | C | C | — | — | R | — |
| Policy Review | A | C | C | C | R | C | — | C | C |
| Policy Approval (Master) | A | I | I | I | I | I | R | I | I |
| Policy Approval (Domain) | A | R | I | I | C | C | I | I | I |
| Policy Publication | R | I | I | I | I | I | — | R | I |
| Policy Awareness Training | A | I | I | I | — | R | — | R | I |
| Policy Enforcement | A | R | R | — | — | R | — | R | I |
| Compliance Monitoring | A | R | R | — | — | — | I | R | R |
| Policy Exception Approval | R | C | C | — | C | — | I | A | I |
| Annual Policy Review | R | C | C | — | C | — | I | A | I |
| Policy Acknowledgment Tracking | C | — | — | — | — | R | — | I | C |

---

## Incident Response RACI

| Activity | CISO | CTO | VP Eng | Legal | Security Team | Engineering | PR | HR |
|----------|------|-----|--------|-------|---------------|-------------|-----|-----|
| Incident Detection | — | — | — | — | R | C | — | — |
| Triage & Classification | A | I | I | I | R | — | — | — |
| Containment Decision | A | R | R | — | C | C | — | — |
| Forensic Investigation | A | — | — | — | R | — | — | — |
| Legal Notification | C | — | — | A/R | — | — | — | — |
| Customer Communication | A | — | — | R | — | — | R | — |
| Regulatory Reporting | C | — | — | A/R | — | — | — | — |
| Post-Incident Review | A | C | C | C | R | C | — | — |
| Remediation Tracking | A | R | R | — | R | R | — | — |

---

## Vendor Risk Management RACI

| Activity | CISO | CTO | VP Eng | CFO | Legal | Procurement | Security Team | Vendor Owner |
|----------|------|-----|--------|-----|-------|-------------|---------------|--------------|
| Vendor Classification | A | C | C | — | — | R | R | C |
| Security Assessment | A | — | — | — | — | — | R | C |
| Contract Security Review | C | — | — | C | A/R | R | — | C |
| Risk Scoring | A | — | — | — | — | — | R | — |
| Ongoing Monitoring | A | C | — | — | — | — | R | — |
| Off-Boarding | C | C | C | — | C | A | R | R |

---

## Business Continuity RACI

| Activity | CISO | CTO | VP Eng | CFO | Department Heads | Security Team | Facilities |
|----------|------|-----|--------|-----|------------------|---------------|------------|
| BIA Development | A | C | C | C | R | R | C |
| BCP Development | A | R | R | — | R | R | — |
| DR Plan Development | A | R | R | — | — | R | — |
| Tabletop Exercise Design | A | C | C | — | — | R | — |
| Tabletop Exercise Execution | A | R | R | I | R | R | R |
| After-Action Report | A | C | C | — | — | R | R |
| Remediation Tracking | A | R | R | — | R | R | — |
| Annual Test Coordination | A | C | C | — | — | R | R |

---

## Key Accountability Notes

1. **CISO** holds primary accountability for the security program — all security policies ultimately roll up to the CISO.
2. **CTO** is accountable for technical implementation of security controls in infrastructure and platform.
3. **VP Engineering** is accountable for application security and secure software development lifecycle.
4. **Legal** holds accountability for regulatory compliance, contract security terms, and privacy obligations.
5. **Security Team** performs the operational work — assessments, monitoring, incident response, awareness.
6. **Board** approves the master security policy and is informed of significant security events and risk posture changes.
