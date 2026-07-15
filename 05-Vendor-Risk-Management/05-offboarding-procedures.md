# Vendor Off-Boarding Procedures

**Phase:** 5 — Vendor Risk Management Program
**Objective:** Define secure off-boarding procedures for vendor contract termination

---

## Off-Boarding Process Timeline

```
T-90 days: Contract end notification
T-60 days: Data return/destruction planning
T-30 days: Data export initiation
T-0: Contract termination + access revocation
T+30 days: Destruction confirmation
T+45 days: Final security assessment
```

---

## Step-by-Step Procedure

### Phase 1: Planning (T-90 to T-60 days)

| Step | Action | Owner |
|------|--------|-------|
| 1 | Notify vendor of non-renewal / termination per contract terms | Procurement |
| 2 | Identify all NexPay data stored with or accessible by the vendor | Security Team + Vendor Owner |
| 3 | Determine data disposition: return, transfer, or destroy | Legal + CISO |
| 4 | Document data inventory: databases, backups, logs, analytics | Security Team |
| 5 | Identify all integrations, API keys, SSO connections | DevOps + Vendor Owner |

### Phase 2: Data Extraction (T-60 to T-30 days)

| Step | Action | Owner |
|------|--------|-------|
| 6 | Export all NexPay data in portable format (CSV, JSON, encrypted archive) | Vendor Owner |
| 7 | Verify data completeness — compare export counts to known totals | Security Team |
| 8 | Download and store exported data in encrypted, access-controlled S3 bucket | DevOps |
| 9 | Transfer data to replacement vendor (if applicable) | Vendor Owner |

### Phase 3: Termination (T-0)

| Step | Action | Owner |
|------|--------|-------|
| 10 | Send formal termination notice per contract terms | Procurement |
| 11 | Revoke all API keys, service accounts, and SSO integrations | DevOps |
| 12 | Remove vendor from SSO identity provider | DevOps |
| 13 | Remove vendor from internal documentation (runbooks, architecture diagrams) | Security Team |
| 14 | Update firewall rules to block vendor network access (if applicable) | DevOps |
| 15 | Update DNS records if vendor-controlled domains used | DevOps |

### Phase 4: Data Destruction Confirmation (T+30 days)

| Step | Action | Owner |
|------|--------|-------|
| 16 | Request written certification of data destruction from vendor | Security Team |
| 17 | Certification must include: date of destruction, method used, scope of data destroyed | Legal |
| 18 | Verify certification against data inventory | Security Team |
| 19 | Store destruction certification in vendor risk register | Security Team |

### Phase 5: Final Assessment (T+45 days)

| Step | Action | Owner |
|------|--------|-------|
| 20 | Confirm no residual data access remains | Security Team |
| 21 | Update vendor risk register: status = "Decommissioned" | Security Team |
| 22 | Archive vendor assessment documentation per data retention policy | Security Team |
| 23 | Conduct post-off-boarding review — document lessons learned | CISO |
| 24 | Update vendor management processes based on lessons learned | CISO |

---

## Off-Boarding Checklist

| # | Item | Completed? | Date | Notes |
|---|------|------------|------|-------|
| 1 | Contract termination notice sent | | | |
| 2 | Data inventory complete | | | |
| 3 | Data exported and verified | | | |
| 4 | All API tokens revoked | | | |
| 5 | SSO integrations removed | | | |
| 6 | Firewall rules updated | | | |
| 7 | DNS records updated | | | |
| 8 | Team notified of vendor change | | | |
| 9 | Replacement vendor onboarded (if applicable) | | | |
| 10 | Destruction certification received | | | |
| 11 | Risk register updated | | | |
| 12 | Documentation archived | | | |

---

## Off-Boarding SLA

| Tier | Access Revocation | Data Destruction Certificate |
|------|-------------------|------------------------------|
| Critical | ≤4 hours | ≤14 days |
| High | ≤24 hours | ≤30 days |
| Medium | ≤48 hours | ≤30 days |
| Low | ≤7 days | ≤45 days |
