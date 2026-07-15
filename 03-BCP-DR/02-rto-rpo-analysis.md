# RTO/RPO Analysis

**Phase:** 3 — BCP/DR with Tested Runbooks
**Objective:** Define and document Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) for all critical systems

---

## RTO/RPO Definitions

| Metric | Definition | Determined By |
|--------|------------|---------------|
| RTO | Maximum time allowed to restore a system after disruption | Business Impact Analysis — how long can we afford to be down |
| RPO | Maximum acceptable data loss measured in time | Business Impact Analysis — how much data can we afford to lose |
| MAO | Maximum Acceptable Outage — the point at which disruption becomes intolerable | Board risk appetite |
| MTD | Maximum Tolerable Downtime — same as MAO | ISO 22301 terminology |

---

## System-Level RTO/RPO

### Tier 1 — Critical Systems

| System | RTO | RPO | MAO | Strategy | DR Region | Failover Type |
|--------|-----|-----|-----|----------|-----------|---------------|
| Transaction Engine API | 4 hours | 5 min | 1 hour | Active-active (multi-AZ) → cross-region failover | us-west-2 | Automated |
| Payment Key Vault (Vault) | 1 hour | Real-time | 30 min | Active-standby with auto-unseal | us-west-2 | Semi-automated |
| Customer PII Database (RDS) | 4 hours | 5 min | 1 hour | Cross-region read replica → promote | us-west-2 | Automated |
| Okta SSO | 1 hour | Real-time | 30 min | Okta cell-based architecture (multi-region) | SaaS-native | Automated |
| Fraud Detection ML (Sagemaker) | 4 hours | 1 hour | 4 hours | Model artifacts cross-region replicated + standby endpoint | us-west-2 | Manual promotion |
| AWS Production Environment | 4 hours | 5 min | 2 hours | Infrastructure-as-Code (Terraform) + cross-region deployment | us-west-2 | Semi-automated |

### Tier 2 — High Systems

| System | RTO | RPO | MAO | Strategy |
|--------|-----|-----|-----|----------|
| Customer Support Portal (Zendesk) | 8 hours | 1 hour | 8 hours | SaaS — Zendesk multi-region by default |
| Internal Financial Systems (QuickBooks) | 8 hours | 1 hour | 24 hours | Cloud backup + alternate access method |
| Microsoft 365 / Email | 8 hours | 1 hour | 8 hours | Microsoft-native redundancy (MS handles failover) |
| HR System (Rippling) | 24 hours | 4 hours | 24 hours | SaaS — Rippling multi-region by default |
| CI/CD Pipeline (GitHub Actions) | 24 hours | 4 hours | 12 hours | Self-hosted runner redundancy + backup |

### Tier 3 — Medium Systems

| System | RTO | RPO | MAO | Strategy |
|--------|-----|-----|-----|----------|
| Corporate Website | 24 hours | 24 hours | 72 hours | Static site — redeploy from repo |
| Internal Wiki (Confluence) | 24 hours | 24 hours | 72 hours | Cloud backup + restore |
| Project Management (Jira) | 24 hours | 24 hours | 72 hours | Atlassian-managed redundancy |

---

## Recovery Time Budget

The recovery time budget from declaration of disaster:

```
T=0       Disaster declared
T+15min   CISO/CTO war room established
T+30min   Incident assessment complete (scope, severity)
T+1hr     Failover initiation (automated scripts triggered)
T+2hr     Critical systems restored (authentication, database)
T+3hr     Transaction engine online — read-only validation
T+4hr     Full production traffic shifted to DR — T1 systems green
T+8hr     T2 systems restored
T+24hr    T3 systems restored
T+48hr    Full post-incident review complete
```

---

## RTO/RPO Validation Plan

| System | Validation Method | Frequency | Last Tested | Next Test |
|--------|------------------|-----------|-------------|-----------|
| Transaction Engine | Automated failover test + traffic shift | Quarterly | N/A (new) | Q2 2026 |
| RDS Database | Cross-region replica promotion test | Quarterly | N/A (new) | Q2 2026 |
| Okta SSO | Okta trust test (cell isolation) | Semi-annual | N/A (new) | Q2 2026 |
| Key Vault | DR site Vault unseal + key verification | Semi-annual | N/A (new) | Q2 2026 |
| ML Models | S3 cross-region copy verification + endpoint test | Semi-annual | N/A (new) | Q2 2026 |
| Email | MS-native redundancy (vendor-tested) | Annual | N/A (new) | Q2 2026 |
| CI/CD | Runner redeployment from backup | Semi-annual | N/A (new) | Q3 2026 |

---

## Gap Analysis

| Gap | Risk | Mitigation | Timeline |
|-----|------|------------|----------|
| No cross-region DR infrastructure exists | If us-east-1 goes down, all T1 systems fail for >4 hours | Provision DR infrastructure in us-west-2 via Terraform | Month 1–2 |
| Vault auto-unseal not configured for DR | Manual key management adds 2+ hours to recovery | Configure DR Vault with auto-unseal + KMS cross-region key replication | Month 2 |
| Fraud detection models not replicated cross-region | Fraud runs unchecked during DR failover | Set up S3 cross-region replication + SageMaker model registry in DR region | Month 2 |
| No DR runbook test performed | RTO/RPO targets are theoretical | Schedule first tabletop exercise (this phase) | Month 1 |
| RDS cross-region replica not configured | RPO of 5 minutes not achievable | Deploy cross-region read replica for PII database | Month 1 |
