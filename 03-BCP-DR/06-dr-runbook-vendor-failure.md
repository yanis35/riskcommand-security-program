# DR Runbook — Critical Vendor Failure

**Phase:** 3 — BCP/DR with Tested Runbooks
**Scenario:** A Critical-tier vendor suffers a prolonged outage or security incident affecting NexPay operations
**Objective:** Maintain business operations through vendor outage or transition to alternative provider
**RTO Target:** Varies by vendor (see below)

---

## Critical Vendor Inventory

| Vendor | Service | Tier | RTO | Fallback Strategy |
|--------|---------|------|-----|-------------------|
| AWS | Cloud infrastructure | Critical | Rapid → DR region | Cross-region failover (see DR Runbook 01) |
| Okta | Identity & SSO | Critical | 1 hour | Backup IdP (Google Workspace) + offline access |
| Twilio/SendGrid | Transactional email | High | 4 hours | SES fallback (pre-configured) |
| Stripe | Payment processing | Critical | Immediate | Adyen (pre-integrated but dormant) |
| Datadog | Monitoring & SIEM | High | 8 hours | CloudWatch + manual monitoring |
| Zendesk | Customer support | High | 8 hours | Email-only support (manual process) |
| GitHub | Source code & CI/CD | High | 4 hours | GitLab self-hosted (backup instance) |

---

## AWS Outage (see separate DR Runbook 01 — Datacenter Failover)

Refer to the complete AWS Region Failover runbook for AWS outage procedures.

---

## Okta SSO Outage

### Impact
- ALL users cannot authenticate to ANY service
- Complete business shutdown within 30 minutes

### Recovery Steps

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 1 | Verify Okta status page (status.okta.com) | Security | 2 min |
| 2 | If Okta outage confirmed, activate backup IdP | CTO | 5 min |
| 3 | Enable backup IdP (Google Workspace) for authentication | DevOps | 15 min |
| 4 | Deploy emergency break-glass accounts for critical personnel (pre-created & stored in Vault) | Security | 10 min |
| 5 | Communication: notify employees of backup authentication method | CTO | 5 min |
| 6 | Monitor Okta status — fail back when operational | DevOps | Until resolved |

---

## Stripe Payment Processing Outage

### Impact
- All payment transactions fail
- Revenue loss: $267,000/hour

### Recovery Steps

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 1 | Confirm Stripe outage (status.stripe.com) | DevOps | 2 min |
| 2 | If outage >15 minutes, activate Adyen fallback | CTO | 10 min |
| 3 | Switch API endpoint from Stripe to Adyen in configuration | DevOps | 10 min |
| 4 | Verify test transaction processes through Adyen | DevOps | 5 min |
| 5 | Resume production traffic through Adyen | CTO | 5 min |
| 6 | Monitor transaction success rate | DevOps | Until resolved |
| 7 | When Stripe recovers, validate before switching back | DevOps | — |

---

## Vendor Failure Prevention

- All Critical-tier vendors must have a documented fallback option
- Fallback integrations tested annually (at minimum)
- Vendor risk score reviewed quarterly (see Vendor Risk Management program)
- SLA credits tracked and claimed for any outage exceeding contractual SLA
- Business continuity plans updated when critical vendor changes occur
