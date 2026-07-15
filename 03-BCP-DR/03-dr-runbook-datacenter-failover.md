# DR Runbook — Complete Data Center / AWS Region Failover

**Phase:** 3 — BCP/DR with Tested Runbooks
**Scenario:** us-east-1 region becomes unavailable (prolonged outage >30 minutes)
**Objective:** Fail over all Tier 1 and Tier 2 systems to us-west-2 DR region
**RTO Target:** ≤4 hours for T1 systems
**RPO Target:** ≤5 minutes data loss

---

## Pre-Requisites

- [ ] DR infrastructure provisioned in us-west-2 via Terraform
- [ ] RDS cross-region read replica configured for PII database
- [ ] Vault DR cluster configured with auto-unseal
- [ ] S3 cross-region replication enabled for ML models and configs
- [ ] Route53 health checks configured for automated DNS failover
- [ ] DR runbook accessible offline (printed + local copy)
- [ ] On-call engineer has access to AWS Organizations management account

---

## Step-by-Step Procedures

### Phase 1: Assessment (T+0 — T+15min)

| Step | Action | Owner | Duration | Verification |
|------|--------|-------|----------|-------------|
| 1.1 | Confirm region outage via AWS Health Dashboard + PagerDuty | On-call Engineer | 2 min | Multiple monitoring sources confirmed |
| 1.2 | Declare disaster event in incident tracking system | CISO | 2 min | Ticket SEV-1 created |
| 1.3 | Activate war room (Slack #dr-war-room + Zoom bridge) | CISO | 3 min | CTO, VP Eng, Security Team confirmed |
| 1.4 | Assess scope: which systems are affected, what is the estimated outage duration | CTO | 5 min | Documented in war room |
| 1.5 | Make go/no-go decision for DR failover | CISO + CTO | 3 min | Decision documented in ticket |

### Phase 2: DNS Failover (T+15min — T+30min)

| Step | Action | Owner | Duration | Verification |
|------|--------|-------|----------|-------------|
| 2.1 | Update Route53 DNS records: point api.nexpay.com to us-west-2 load balancer | On-call Engineer | 5 min | TTL set to 60 seconds |
| 2.2 | Update Route53 for app.nexpay.com → DR ALB | On-call Engineer | 5 min | TTL set to 60 seconds |
| 2.3 | Update Route53 for sso.nexpay.com (Okta) — no change needed (SaaS) | On-call Engineer | 2 min | Verified Okta status |
| 2.4 | Flush CloudFront cache for all distributions | On-call Engineer | 5 min | Cache invalidation completed |
| 2.5 | Verify DNS propagation: dig +trace for all public endpoints | On-call Engineer | 5 min | All records resolving to us-west-2 IPs |

### Phase 3: Database Failover (T+30min — T+60min)

| Step | Action | Owner | Duration | Verification |
|------|--------|-------|----------|-------------|
| 3.1 | Promote RDS read replica in us-west-2 to primary | DBA / DevOps | 10 min | RDS console shows "Available" as primary |
| 3.2 | Update application connection strings to new primary endpoint | DevOps | 5 min | Config updated in Parameter Store |
| 3.3 | Verify database integrity: row counts, latest transaction timestamp, replication lag | DBA | 15 min | All checks pass |
| 3.4 | Enable write operations on promoted database | DBA | 5 min | Write-ahead log verified |
| 3.5 | Verify application connectivity to new database | DevOps | 5 min | Health check endpoint returns 200 |

### Phase 4: Application Failover (T+60min — T+120min)

| Step | Action | Owner | Duration | Verification |
|------|--------|-------|----------|-------------|
| 4.1 | Deploy application containers to us-west-2 EKS cluster (if not already running) | DevOps | 20 min | `kubectl get pods -A` — all healthy |
| 4.2 | Scale up DR EKS cluster to production capacity | DevOps | 10 min | Auto-scaling group at desired count |
| 4.3 | Verify transaction engine health: test API endpoint, process test transaction | DevOps | 10 min | POST /v1/transactions returns 201 |
| 4.4 | Verify fraud detection service: submit test transaction, confirm model scores it | ML Eng | 10 min | Model endpoint responds |
| 4.5 | Verify Vault connectivity: applications can retrieve secrets from DR Vault | Security | 10 min | `vault status` — sealed status: false |
| 4.6 | Run automated integration test suite against DR endpoint | DevOps | 15 min | All tests pass (90%+ coverage) |

### Phase 5: Validation & Traffic Shift (T+120min — T+240min)

| Step | Action | Owner | Duration | Verification |
|------|--------|-------|----------|-------------|
| 5.1 | Shift 10% of traffic to DR — monitor for errors | CTO | 15 min | Error rate <0.1% |
| 5.2 | Shift 50% of traffic — monitor latency and error rates | CTO | 15 min | p99 latency <500ms |
| 5.3 | Shift 100% of traffic to DR | CTO | 5 min | Full production traffic on DR |
| 5.4 | Monitor DR systems for 30 minutes: errors, latency, transactions | DevOps | 30 min | All metrics within normal range |
| 5.5 | Declare DR active status | CISO | 2 min | Status update to exec team |

### Phase 6: Communication (Parallel)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 6.1 | Notify executive leadership (Slack + email) | CISO | T+15min |
| 6.2 | Update status page (status.nexpay.com) | DevOps | T+30min |
| 6.3 | Notify board (email summary) | CISO | T+1hr |
| 6.4 | Notify critical customers (pre-arranged list) | VP CS | T+2hr |
| 6.5 | Post incident update on social media (if needed) | PR | T+2hr |

---

## Rollback Procedure

If DR failover is unsuccessful or primary region recovers:

| Step | Action | Owner |
|------|--------|-------|
| RB-1 | Restore Route53 DNS to primary region endpoints | DevOps |
| RB-2 | Re-point application config to primary RDS instance | DevOps |
| RB-3 | Scale down DR EKS cluster to minimum | DevOps |
| RB-4 | Run integration tests against primary region | DevOps |
| RB-5 | Shift traffic back to primary (10% → 50% → 100%) | CTO |
| RB-6 | Demote promoted RDS replica back to read replica | DBA |

---

## Post-Recovery

- Conduct post-incident review within 5 business days
- Document runbook improvements based on lessons learned
- Update DR test schedule to quarterly for T1 systems
- Consider Chaos Engineering exercises to validate failover automation
