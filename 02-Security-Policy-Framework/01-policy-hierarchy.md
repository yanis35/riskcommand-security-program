# Security Policy Framework — Policy Hierarchy

**Phase:** 2 — Security Policy Framework
**Objective:** Define the policy hierarchy, document taxonomy, and governance structure
**Framework:** NIST CSF 2.0, ISO 27001:2022 Annex A
**Total documents:** 1 master policy + 11 domain policies + 2 supporting documents = 14 documents

---

## Policy Hierarchy

```
                    ┌─────────────────────────────────────┐
                    │     Information Security Policy      │
                    │         (Master Policy)              │
                    │    Board-approved, annual review      │
                    └────────────────┬────────────────────┘
                                     │
                    ┌────────────────┼────────────────────┐
                    │                │                     │
         ┌──────────┴──────────┐    │    ┌─────────────────┴──────────────┐
         │  Domain Policies     │    │    │   Supporting Documents         │
         │  (Mandatory)         │    │    │   (Standards, Procedures,     │
         │                     │    │    │    Guidelines)                  │
         ├─────────────────────┤    │    ├──────────────────────────────┤
         │ AU — Acceptable Use │    │    │ Password Standard              │
         │ DC — Data Class.    │    │    │ Encryption Standard            │
         │ AC — Access Control │    │    │ Incident Response Procedure    │
         │ CR — Cryptography   │    │    │ Backup Procedure               │
         │ PS — Physical Sec.  │    │    │ Vendor Assessment Standard     │
         │ OS — Operations Sec.│    │    │ Secure Coding Guidelines       │
         │ IR — Incident Resp. │    │    │ Cloud Security Standard        │
         │ BC — Business Cont. │    │    │ Compliance Checklist           │
         │ VM — Vendor Mgmt    │    │    │ ───                           │
         │ RW — Remote Work    │    │    │ RACI Matrix                   │
         │ VL — Vulnerability  │    │    │ NIST CSF Control Mapping      │
         └─────────────────────┘    │    └──────────────────────────────┘
                                     │
                    ┌────────────────┴────────────────┐
                    │         Procedures              │
                    │  (Step-by-step how-to guides)   │
                    │  Maintained by Security Team    │
                    │  Reviewed quarterly             │
                    └─────────────────────────────────┘
```

---

## Document Taxonomy

| Level | Document Type | Description | Approval Authority | Review Cycle |
|-------|---------------|-------------|-------------------|--------------|
| **Level 1** | Policy | High-level statement of management intent, mandatory requirements | Board of Directors | Annual |
| **Level 2** | Standard | Specific mandatory requirements, technical configurations | CISO | Annual |
| **Level 3** | Procedure | Step-by-step instructions for accomplishing a task | Security Team Lead | Semi-annual |
| **Level 4** | Guideline | Recommended best practices, not mandatory | Security Team | As needed |

---

## Policy Documents — Complete List

| ID | Policy Name | Version | Effective Date | Owner |
|----|-------------|---------|----------------|-------|
| POL-01 | Information Security Policy (Master) | 1.0 | 2026-01-15 | CISO |
| POL-02 | Acceptable Use Policy | 1.0 | 2026-01-15 | CISO |
| POL-03 | Data Classification & Handling Policy | 1.0 | 2026-01-15 | CISO |
| POL-04 | Access Control Policy | 1.0 | 2026-01-15 | CTO |
| POL-05 | Cryptography Policy | 1.0 | 2026-01-15 | CTO |
| POL-06 | Physical Security Policy | 1.0 | 2026-01-15 | Facilities |
| POL-07 | Operations Security Policy | 1.0 | 2026-01-15 | CTO |
| POL-08 | Incident Response Policy | 1.0 | 2026-01-15 | CISO |
| POL-09 | Business Continuity Policy | 1.0 | 2026-01-15 | CISO |
| POL-10 | Vendor Management Policy | 1.0 | 2026-01-15 | CISO |
| POL-11 | Remote Work & BYOD Policy | 1.0 | 2026-01-15 | CTO |
| POL-12 | Vulnerability Management Policy | 1.0 | 2026-01-15 | CTO |

---

## Policy Lifecycle

```
Draft → Review → Approval → Publication → Awareness → Enforcement → Review (Annual) → Update
  │         │          │          │            │            │              │            │
  └─CISO    └─Legal    └─Board    └─Wiki      └─Training   └─Audit       └─CISO       └─Rev V+I
     Lead      + Exec             + Email      + Acknowledgment             Review
```

---

## Exceptions Process

Any deviation from policy must follow the exceptions process:

1. **Request:** Risk owner submits Policy Exception Request form (documented in GRC tool)
2. **Review:** CISO reviews business justification and compensating controls
3. **Risk Acceptance:** If approved, risk is added to risk register as "Accepted" with expiry date
4. **Approval:** Exceptions require CISO approval (or Board if >30 days or Critical risk)
5. **Expiration:** All exceptions have a maximum term of 12 months
6. **Renewal:** Exceptions may be renewed once with CISO + Board approval

---

## Policy Distribution & Acknowledgment

- All policies published on internal wiki (Confluence)
- All employees must acknowledge receipt and understanding within 30 days of hire
- Annual re-acknowledgment required for all active employees
- Acknowledgment tracked in HRIS (Rippling)
- Non-acknowledgment escalated to manager → HR → termination if unresolved >90 days
