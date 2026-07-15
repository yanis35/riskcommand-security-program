# Risk Register

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Objective:** Master register of all identified risks with ownership, treatment plans, and status tracking
**Format:** This document represents the canonical risk register. In production, this would be maintained in a GRC tool (Archer, ServiceNow, OneTrust) or structured spreadsheet.
**Review Cadence:** Monthly by CISO, Quarterly by Board

---

## Register Fields

| Field | Description |
|-------|-------------|
| Risk ID | Unique identifier |
| Category | NIST CSF function (Identify, Protect, Detect, Respond, Recover) |
| Risk Statement | If [threat actor] exploits [vulnerability], then [business impact] occurs |
| Asset | Crown jewel affected |
| Threat Source | Internal/external, accidental/malicious |
| Current Controls | What exists today |
| L | Qualitative Likelihood (1–5) |
| I | Qualitative Impact (1–5) |
| Risk Score | L × I |
| ALE | Annualized Loss Expectancy from FAIR |
| Treatment | Accept, Mitigate, Transfer, Avoid |
| Treatment Plan | Specific actions with timeline |
| Risk Owner | Who is accountable |
| Status | Open, In Progress, Accepted, Closed, Transferred |
| Residual Score | Score after controls implemented |

---

## Risk Register Entries

### RI-001 — PII Data Breach via SQL Injection

| Field | Value |
|-------|-------|
| Risk Statement | If an attacker exploits missing WAF SQLi rules, then customer PII (SSNs, bank accounts, KYC) will be exfiltrated, resulting in GDPR fines, breach notification costs, and customer churn. |
| Asset | CJ-001 — Customer PII Database |
| Threat Source | External — Automated scanners, opportunistic attackers |
| Current Controls | WAF deployed (no SQLi ruleset), RDS encryption at rest, network ACLs |
| L | 4 |
| I | 5 |
| Risk Score | **20 (Critical)** |
| ALE | $11,137,500 |
| Treatment | **Mitigate** |
| Treatment Plan | Deploy WAF OWASP SQLi ruleset → Run DAST scanner → Retest (2 weeks) |
| Risk Owner | CTO |
| Status | **Open** |
| Residual Score (projected) | 8 (Medium) |

### RI-002 — Payment Key Compromise via Vault Access

| Field | Value |
|-------|-------|
| Risk Statement | If an attacker authenticates to the key vault without MFA, then all payment signing keys and API credentials will be compromised, enabling fraudulent transactions and PCI DSS violation. |
| Asset | CJ-002 — Payment Processing Key Vault |
| Threat Source | Internal — Disgruntled employee, compromised engineer account |
| Current Controls | Token-based auth (24h expiry), network segmentation, Vault audit logging |
| L | 4 |
| I | 5 |
| Risk Score | **20 (Critical)** |
| ALE | $12,342,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Enable MFA on Vault → Restrict token paths → Deploy HSM → Vault proxy with access logging (2 weeks for MFA, 2 months for HSM) |
| Risk Owner | CTO |
| Status | **In Progress** |
| Residual Score (projected) | 6 (Medium) |

### RI-003 — DB Privilege Escalation

| Field | Value |
|-------|-------|
| Risk Statement | If an over-permissioned database role is exploited, then an attacker gains admin database access and can exfiltrate, modify, or destroy the full PII dataset. |
| Asset | CJ-001 — Customer PII Database |
| Threat Source | Internal — Over-permissioned engineers, attackers who compromise an engineer's session |
| Current Controls | IAM roles (some users have static credentials), audit logging enabled |
| L | 4 |
| I | 5 |
| Risk Score | **20 (Critical)** |
| ALE | $12,375,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Row-level security → revoke unnecessary privileges → deploy database firewall → implement just-in-time access (4 weeks) |
| Risk Owner | CTO |
| Status | **Open** |
| Residual Score (projected) | 8 (Medium) |

### RI-004 — Malicious PR in Production

| Field | Value |
|-------|-------|
| Risk Statement | If an attacker or compromised maintainer submits a malicious PR to a non-protected branch, then backdoored code reaches production, resulting in a supply chain attack. |
| Asset | CJ-004 — Source Code Repository |
| Threat Source | External — Supply chain attackers, compromised open-source dependencies |
| Current Controls | Branch protection on main branch, required PR reviews (honor system) |
| L | 4 |
| I | 5 |
| Risk Score | **20 (Critical)** |
| ALE | $6,321,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Enforce branch protection on ALL branches → require 2 approvals → enforce signed commits → deploy SCA tool (1 week) |
| Risk Owner | VP Engineering |
| Status | **Open** |
| Residual Score (projected) | 8 (Medium) |

### RI-005 — JWT Forgery with Escalated Privileges

| Field | Value |
|-------|-------|
| Risk Statement | If an attacker extracts the public signing key from client-side code, then forged JWTs can be crafted with admin claims, enabling unauthorized access to administrative API endpoints. |
| Asset | CJ-003 — Core Transaction Engine |
| Threat Source | External — API attackers, reverse engineers |
| Current Controls | RS256 signing, JWT expiration (1 hour), role-based authorization |
| L | 3 |
| I | 5 |
| Risk Score | **15 (Critical)** |
| ALE | $1,725,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Rotate JWT signing key → implement quarterly key rotation → move public key to server-side validation → migrate to RS384 (2 weeks) |
| Risk Owner | VP Engineering |
| Status | **Open** |
| Residual Score (projected) | 6 (Medium) |

### RI-006 — DDoS Against Transaction Engine

| Field | Value |
|-------|-------|
| Risk Statement | If a DDoS attack saturates the public API endpoint, then customer transactions fail for hours, resulting in $267K/hour revenue loss and SLA penalty payouts. |
| Asset | CJ-003 — Core Transaction Engine |
| Threat Source | External — Hacktivists, competitors, extortion groups |
| Current Controls | CloudFront CDN, basic rate limiting, auto-scaling |
| L | 4 |
| I | 4 |
| Risk Score | **16 (Critical)** |
| ALE | $3,105,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Deploy AWS Shield Advanced → configure WAF rate limiting + geo-blocking → run DDoS tabletop exercise (3 weeks) |
| Risk Owner | CTO |
| Status | **In Progress** |
| Residual Score (projected) | 8 (Medium) |

### RI-007 — CI/CD Vault Token Over-Scoping

| Field | Value |
|-------|-------|
| Risk Statement | If the CI/CD pipeline Vault token is scoped too broadly (entire KV mount), then a pipeline compromise leads to all secrets in Vault being readable by the attacker. |
| Asset | CJ-002 — Payment Processing Key Vault |
| Threat Source | External — Supply chain attack on CI/CD pipeline |
| Current Controls | Vault token with KV mount scope, CI/CD runs in ephemeral containers |
| L | 4 |
| I | 4 |
| Risk Score | **16 (Critical)** |
| ALE | $3,630,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Create path-restricted tokens per pipeline → rotate all tokens → implement Vault agent sidecar for short-lived tokens (1 week) |
| Risk Owner | VP Engineering |
| Status | **Open** |
| Residual Score (projected) | 6 (Medium) |

### RI-008 — Internal MITM on Payment Infrastructure

| Field | Value |
|-------|-------|
| Risk Statement | If an attacker gains internal network access (compromised VPN, rogue device), then they can perform man-in-the-middle attacks on payment traffic between the transaction engine and downstream processors, capturing card data and authentication tokens. |
| Asset | CJ-003 — Core Transaction Engine |
| Threat Source | Internal — Compromised VPN credentials, rogue device on internal network |
| Current Controls | Network segmentation (VLANs), HTTPS/TLS encryption, no internal PKI |
| L | 3 |
| I | 4 |
| Risk Score | **12 (High)** |
| ALE | $903,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Deploy internal PKI with mutual TLS → implement network access controls (NAC) → configure TLS with certificate pinning on payment endpoints (4 weeks) |
| Risk Owner | CTO |
| Status | **Open** |
| Residual Score (projected) | 6 (Medium) |

### RI-009 — ML Model Exfiltration

| Field | Value |
|-------|-------|
| Risk Statement | If an engineer with broad S3 access exfiltrates the fraud detection model, then a competitor can replicate the company's core IP, eliminating competitive advantage. |
| Asset | CJ-006 — ML Fraud Detection Model |
| Threat Source | Internal — Over-permissioned engineers, accidental exposure |
| Current Controls | S3 server-side encryption (AES-256), bucket policies (no logging) |
| L | 3 |
| I | 4 |
| Risk Score | **12 (High)** |
| ALE | $18,360,000 |
| Treatment | **Mitigate** |
| Treatment Plan | S3 bucket access logging → KMS encryption → file-level ACLs → data loss prevention monitoring (2 weeks) |
| Risk Owner | VP Engineering |
| Status | **Open** |
| Residual Score (projected) | 6 (Medium) |

### RI-010 — Secrets Committed to Public Repo

| Field | Value |
|-------|-------|
| Risk Statement | If a developer commits cloud credentials or API keys to a public repository, then the entire AWS production environment is exposed, enabling data theft and resource abuse. |
| Asset | CJ-004 — Source Code Repository / CJ-005 — AWS Production Environment |
| Threat Source | Internal — Developer error, rushed deployments |
| Current Controls | pre-commit hooks (not enforced), git-secrets (not installed for all) |
| L | 4 |
| I | 3 |
| Risk Score | **12 (High)** |
| ALE | $6,020,000 |
| Treatment | **Mitigate** |
| Treatment Plan | Enforce pre-commit hooks → deploy secret scanning in CI/CD → rotate all credentials → implement GitHub push protection (1 week) |
| Risk Owner | VP Engineering |
| Status | **In Progress** |
| Residual Score (projected) | 4 (Low) |

---

## Risk Register Summary

| Status | Count | Total ALE |
|--------|-------|-----------|
| Open | 7 | $54,451,500 |
| In Progress | 3 | $21,467,000 |
| Accepted | 0 | $0 |
| Transferred | 0 | $0 |
| Closed | 0 | $0 |
| **Total** | **10** | **$75,918,500** |

---

## Risk Treatment Summary

| Treatment | Count | Risks |
|-----------|-------|-------|
| Mitigate | 10 | All top 10 risks |
| Accept | 0 | — |
| Transfer | 0 | — |
| Avoid | 0 | — |

**Note:** Risk transfer (cyber insurance) is a separate program covering secondary losses. It does not replace mitigation for any of these risks.

---

## Risk Owner Accountability

| Owner | Count | Risks | Total ALE |
|-------|-------|-------|-----------|
| CTO | 5 | RI-001, RI-002, RI-003, RI-006, RI-008 | $39,862,500 |
| VP Engineering | 5 | RI-004, RI-005, RI-007, RI-009, RI-010 | $36,056,000 |

---

## Next Review

**Next Risk Register Review:** 30 days from report date
**Next Board Risk Update:** Next quarterly board meeting
**Risk Register Owner:** CISO
