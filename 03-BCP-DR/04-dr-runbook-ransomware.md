# DR Runbook — Ransomware Incident

**Phase:** 3 — BCP/DR with Tested Runbooks
**Scenario:** Ransomware detected on critical systems (encryption of production data, ransom demand received)
**Objective:** Isolate, contain, eradicate, and recover systems with minimal data loss and no ransom payment
**RTO Target:** ≤4 hours for T1 systems
**RPO Target:** ≤5 minutes data loss (immutable backups)

---

## Critical Rule

**DO NOT PAY THE RANSOM.** Paying funds criminal activity and does not guarantee data recovery. Contact law enforcement (FBI IC3, CISA) immediately.

**DO NOT POWER OFF AFFECTED SYSTEMS.** Power-off can destroy forensic evidence. Instead, network-isolate affected systems.

---

## Step-by-Step Procedures

### Phase 1: Detection & Isolation (T+0 — T+30min)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 1.1 | Acknowledge EDR alert / ransomware detection | Security Team | 2 min |
| 1.2 | Identify affected systems from EDR console | Security Team | 5 min |
| 1.3 | Network-isolate affected systems (block at firewall/NAC — do not power off) | Security Team | 5 min |
| 1.4 | Disable VPN access for affected user accounts | CTO | 3 min |
| 1.5 | Revoke all active session tokens for affected accounts | Security Team | 5 min |
| 1.6 | Disable S3 bucket public access + restrict IAM policy for compromised roles | DevOps | 5 min |
| 1.7 | Declare SEV-1 incident in tracking system | CISO | 2 min |
| 1.8 | Activate war room (Slack #security-incident + Zoom) | CISO | 3 min |

### Phase 2: Assessment (T+30min — T+90min)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 2.1 | Determine initial access vector (phishing? vulnerability? credential theft?) | Forensics Lead | 30 min |
| 2.2 | Identify ransomware variant and IOCs | Security Team | 15 min |
| 2.3 | Determine scope: which systems are encrypted, which are clean | CTO | 20 min |
| 2.4 | Check backup integrity: are immutable backups accessible? | DevOps | 10 min |
| 2.5 | Determine if data was exfiltrated (check S3 access logs, network flow logs) | Security Team | 15 min |
| 2.6 | Preserve forensic evidence: memory dump, disk image of affected systems | Forensics Lead | 30 min |

### Phase 3: Containment (T+90min — T+180min)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 3.1 | Rotate ALL secrets in Vault (API keys, DB passwords, TLS certs) | Security + DevOps | 30 min |
| 3.2 | Force password reset for all employees (via Okta) | CTO | 15 min |
| 3.3 | Enable MFA enforcement for all accounts (if not already enforced) | CTO | 10 min |
| 3.4 | Block ransomware C2 infrastructure at firewall/WAF | Security Team | 10 min |
| 3.5 | Deploy EDR scanning to all unaffected systems | DevOps | 20 min |
| 3.6 | Create new, uncompromised AWS accounts for critical services if needed | CTO | 30 min |

### Phase 4: Eradication & Recovery (T+180min — T+360min)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 4.1 | Validate immutable backup integrity (SHA-256 checksums) | DevOps | 15 min |
| 4.2 | Provision clean EC2 instances from golden AMI (not from compromised backups) | DevOps | 20 min |
| 4.3 | Restore application data from immutable backups | DevOps | 30 min |
| 4.4 | Restore database from pre-incident backup (verify RPO achieved) | DBA | 30 min |
| 4.5 | Deploy application containers from clean images | DevOps | 20 min |
| 4.6 | Apply all security patches before connecting to network | DevOps | 15 min |
| 4.7 | Connect restored systems to clean network segment | CTO | 10 min |
| 4.8 | Run security scan on all restored systems before production traffic | Security | 20 min |

### Phase 5: Validation (T+360min — T+480min)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 5.1 | Verify restored application functionality (integration tests) | DevOps | 30 min |
| 5.2 | Verify no indicators of compromise remain (full IOC scan) | Security Team | 30 min |
| 5.3 | Verify database integrity — transaction records complete and accurate | DBA | 30 min |
| 5.4 | Shift 10% → 50% → 100% traffic to restored systems | CTO | 30 min |
| 5.5 | Enable enhanced monitoring for 72 hours post-recovery | DevOps | — |

### Phase 6: Communication (Parallel)

| Step | Action | Owner | Duration |
|------|--------|-------|----------|
| 6.1 | Report to CISA / FBI IC3 (ransomware incident) | CISO + Legal | T+2hr |
| 6.2 | Notify affected customers per regulatory timeline | Legal + VP CS | Per GDPR: ≤72hr |
| 6.3 | Prepare press statement (if data was exfiltrated) | PR | T+4hr |
| 6.4 | Notify cyber insurance carrier | CFO | T+2hr |

---

## Recovery Without Paying Ransom

| Data Source | Recovery Method | Expected Success Rate | RTO |
|-------------|----------------|----------------------|-----|
| Immutable AWS Backups | Restore from S3 Object Lock backups | 99% | ≤4 hours |
| RDS automated backups | Point-in-time recovery to pre-incident | 99.9% | ≤2 hours |
| Terraform state | Restore from S3 versioned Terraform state | 100% | ≤1 hour |
| Git repositories | Restore from GitHub (no evidence of compromise) | 100% | ≤30 min |
| ML models | Redeploy from S3 cross-region copy | 99% | ≤4 hours |

---

## Post-Incident Activities

- Root cause analysis completed within 5 business days
- Determine if access was via phishing → update awareness program
- Determine if vulnerability was exploited → patch gap → update VM policy
- Review and improve detection rules based on ransomware IOCs
- Conduct full-scale tabletop exercise within 30 days
- Report findings to board at next quarterly meeting
