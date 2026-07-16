# Business Impact Analysis

**Phase:** 3 — BCP/DR with Tested Runbooks
**Objective:** Identify critical business processes, quantify impact of disruption, determine RTO/RPO/MAO
**Methodology:** NIST SP 800-34, ISO 22301
**Review Cycle:** Annual

---

## Methodology

Each business process is evaluated across five impact dimensions:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| Revenue Impact | 30% | Direct revenue loss per hour of downtime |
| Regulatory Impact | 25% | Fines, penalties, compliance violations |
| Customer Impact | 20% | SLA penalties, churn, reputational damage |
| Operational Impact | 15% | Downstream process disruption, productivity loss |
| Recovery Cost | 10% | Cost to restore operations (labor, tools, vendors) |

---

## Process Inventory & Criticality

### Tier 1 — Critical (MAO < 4 hours)

| ID | Process | Owner | Revenue/Hour | MAO | RTO | RPO |
|----|---------|-------|-------------|-----|-----|------|
| BP-01 | Payment Transaction Processing | CTO | $267,000 | 4 hours | ≤1 hour | ≤5 min |
| BP-02 | Customer API Gateway | VP Eng | $133,500 | 2 hours | ≤4 hours | ≤5 min |
| BP-03 | User Authentication & SSO | CTO | $267,000 | 1 hour | ≤30 min | Real-time sync |
| BP-04 | Payment Key Management | CTO | $267,000 | 1 hour | ≤4 hours | ≤5 min |
| BP-05 | Transaction Fraud Detection | VP Eng | $100,000 | 4 hours | ≤4 hours | ≤1 hour |

### Tier 2 — High (MAO 4–24 hours)

| ID | Process | Owner | Revenue/Hour | MAO | RTO | RPO |
|----|---------|-------|-------------|-----|-----|------|
| BP-06 | Customer Support Portal | VP CS | $25,000 | 8 hours | ≤8 hours | ≤1 hour |
| BP-07 | Internal Financial Operations | CFO | $10,000 | 24 hours | ≤8 hours | ≤1 hour |
| BP-08 | Employee Email & Comms | CTO | $5,000 | 8 hours | ≤8 hours | ≤1 hour |
| BP-09 | HR & Payroll | CFO | $2,500 | 24 hours | ≤24 hours | ≤4 hours |
| BP-10 | Engineering CI/CD Pipeline | VP Eng | $15,000 | 12 hours | ≤24 hours | ≤4 hours |

### Tier 3 — Medium (MAO 24–72 hours)

| ID | Process | Owner | Revenue/Hour | MAO | RTO | RPO |
|----|---------|-------|-------------|-----|-----|------|
| BP-11 | Corporate Website | Marketing | $1,000 | 72 hours | ≤24 hours | ≤24 hours |
| BP-12 | Internal Wiki & Documentation | CTO | $500 | 72 hours | ≤24 hours | ≤24 hours |
| BP-13 | Project Management Tools | VP Eng | $500 | 72 hours | ≤24 hours | ≤24 hours |

---

## Dependency Analysis

### BP-01: Payment Transaction Processing

```
Payment Processing
├── Depends on:
│   ├── User Authentication (BP-03) — Critical dependency
│   ├── Payment Key Management (BP-04) — Critical dependency
│   ├── Transaction Fraud Detection (BP-05) — High dependency
│   ├── Customer PII Database (CJ-001) — Critical dependency
│   ├── Payment Key Vault (CJ-002) — Critical dependency
│   ├── AWS Production Environment (CJ-005) — Critical dependency
│   └── Employee Email (BP-08) — Medium dependency (comms)
├── Supports:
│   ├── Customer API Gateway (BP-02)
│   ├── Customer Support (BP-06)
│   └── Internal Financial Ops (BP-07)
└── Regulatory: PCI DSS, SOC 2, GDPR
```

### BP-03: User Authentication & SSO

```
User Authentication
├── Depends on:
│   ├── Okta tenant (SaaS)
│   ├── Corporate Email (BP-08) — password resets
│   └── AWS Route53 — DNS
├── Supports:
│   ├── ALL other business processes
│   └── ALL crown jewel assets
└── Critical risk: Single point of failure — if Okta goes down, ALL systems are inaccessible
```

---

## Financial Impact Summary

| Tier | Count | Revenue/Hour (Total) | Daily Revenue Loss | 7-Day Revenue Loss |
|------|-------|---------------------|--------------------|--------------------|
| T1 — Critical | 5 | $772,500 | $18,540,000 | $129,780,000 |
| T2 — High | 5 | $57,500 | $1,380,000 | $9,660,000 |
| T3 — Medium | 3 | $2,000 | $48,000 | $336,000 |
| **Total** | **13** | **$832,000** | **$19,968,000** | **$139,776,000** |

---

## Regulatory Impact of Downtime

| Regulation | Trigger | Maximum Fine | Notes |
|------------|---------|-------------|-------|
| PCI DSS | Payment processing stopped >24 hours | $500,000/month + reputational | Transaction engine is in scope |
| SOC 2 | Any control failure during operations | Loss of certification → lost enterprise deals | All T1 processes in scope |
| GDPR | PII unavailability during breach response | €20M or 4% global revenue | PII DB is a dependency |
| CCPA | Customer data access not restored | $2,500 per violation per consumer | Cumulative exposure >$3M |

---

## Business Continuity Strategy

| Disruption Scenario | T1 Strategy | T2 Strategy | T3 Strategy |
|--------------------|-------------|-------------|-------------|
| Single system failure | Active-active failover (AWS multi-AZ) | Auto-recovery + manual failback | Restore from backup |
| Data center/AZ failure | Cross-region failover to DR region | Warm standby in DR region | Cold standby |
| Ransomware | Immutable backups + bare-metal restore | File restore from cloud backup | Rebuild from gold image |
| SaaS provider outage | Vendor SLA enforcement + fallback process | Manual workaround | Accept downtime |
| Key person loss | Documented procedures + cross-training | Documented procedures | Delayed response |
| Prolonged cloud outage | Declare disaster → activate DR site | Activate DR for critical systems | Accept downtime for non-critical |

---

## Key Findings

1. **Revenue concentration risk:** BP-01 (Payment Processing) accounts for 64% of hourly revenue impact
2. **Authentication single point of failure:** BP-03 (Okta) supports ALL processes — 30-minute MAO is aggressive and requires redundant IdP
3. **Fraud detection gap:** If BP-05 goes down, BP-01 continues processing without fraud checks → increased fraud loss risk
4. **Regulatory amplification:** A 24-hour outage of T1 systems triggers PCI, SOC 2, and potential GDPR reporting obligations simultaneously
