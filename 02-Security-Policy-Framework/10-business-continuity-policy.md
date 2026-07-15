# Business Continuity Policy

**Document ID:** POL-09
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CISO
**Review Cycle:** Annual

---

## 1. Purpose

Establish the framework for business continuity and disaster recovery to ensure critical business functions can continue during and after a disruption.

---

## 2. Policy Requirements

### 2.1 Business Impact Analysis
- BIA shall be conducted annually for all business processes.
- BIA identifies: critical processes, dependencies, resource requirements, RTO, RPO, and MAO (Maximum Acceptable Outage).
- Critical processes defined as those whose disruption would cause >$100K/hour loss or regulatory violation.

### 2.2 Recovery Objectives

| Tier | Description | RTO (Recovery Time Objective) | RPO (Recovery Point Objective) | Examples |
|------|-------------|-------------------------------|-------------------------------|----------|
| T1 | Critical | ≤4 hours | ≤5 minutes | Transaction engine, PII database, payment processing |
| T2 | High | ≤8 hours | ≤1 hour | Customer portal, internal financial systems |
| T3 | Medium | ≤24 hours | ≤4 hours | Corporate email, HR systems, CRM |
| T4 | Low | ≤72 hours | ≤24 hours | Internal wiki, project management, collaboration tools |

### 2.3 Business Continuity Plans
- BCPs must be documented for each critical business process.
- BCPs include: activation criteria, alternate procedures, communications plan, resource requirements, and recovery steps.

### 2.4 Disaster Recovery Plans
- DR plans must be documented for all T1 and T2 systems.
- DR plans include: failover procedures, validation steps, rollback procedures, and contact information.

### 2.5 Testing
- Tabletop exercises: semi-annual for critical scenarios (ransomware, data center failure, key person loss).
- Technical DR tests: quarterly for T1 systems, annual for T2 systems.
- Full-scale exercise: annual including failover to DR site and live transaction processing validation.

### 2.6 Plan Maintenance
- BCP/DR plans reviewed and updated after each test, after significant infrastructure changes, and annually.
- All plans stored in a centrally accessible location available offline.

---

## 3. Related Documents

POL-01 (Information Security Policy), POL-08 (Incident Response Policy), POL-07 (Operations Security Policy)
