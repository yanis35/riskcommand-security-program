# Threat Modeling — STRIDE Analysis

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Objective:** Systematically identify threats against critical systems using the STRIDE methodology
**Framework:** Microsoft STRIDE
**Scope:** 4 Tier-1 crown jewel systems

---

## Methodology

STRIDE categorizes threats into six dimensions. Each system is analyzed across all six, with identified threats mapped to potential attacks, existing controls, and residual risk.

| Category | Definition | Violates |
|----------|------------|----------|
| Spoofing | Pretending to be someone/something else | Authentication |
| Tampering | Modifying data or code without authorization | Integrity |
| Repudiation | Denying an action without proof | Non-repudiation |
| Information Disclosure | Exposing data to unauthorized parties | Confidentiality |
| Denial of Service | Disrupting service availability | Availability |
| Elevation of Privilege | Gaining unauthorized access rights | Authorization |

---

## System 1: Customer PII Database (CJ-001)

**Asset:** PostgreSQL RDS instance containing 1.2M user records (SSNs, bank accounts, KYC docs)

| Threat ID | STRIDE Category | Threat Description | Impact | Existing Control | Severity |
|-----------|----------------|-------------------|--------|-----------------|----------|
| T-001 | Spoofing | Attacker uses stolen DB credentials from engineer's laptop | Full PII exfiltration | IAM roles (partial — some users use static creds) | High |
| T-002 | Tampering | Attacker modifies transaction history or user balances | Financial fraud, regulatory fines | Audit logging enabled, no integrity verification | Critical |
| T-003 | Repudiation | Insider performs unauthorized query and denies it | Legal liability, regulatory findings | CloudTrail enabled, no user-level audit | High |
| T-004 | Information Disclosure | SQL injection via API endpoint exposes PII | GDPR violation, breach notification | WAF in place (rate limiting only, no SQLi ruleset) | Critical |
| T-005 | Denial of Service | RDS instance overwhelmed by query volume | Customer-facing app outage | RDS auto-scaling (not tested) | High |
| T-006 | Elevation of Privilege | Read-only user exploits DB vulnerability to gain admin | Full database compromise | Least privilege (not enforced — many users have write access) | Critical |

---

## System 2: Payment Processing Key Vault (CJ-002)

**Asset:** Software-based key vault (Vault by HashiCorp) storing HSMs, API signing keys, TLS private keys

| Threat ID | STRIDE Category | Threat Description | Impact | Existing Control | Severity |
|-----------|----------------|-------------------|--------|-----------------|----------|
| T-007 | Spoofing | Attacker authenticates to Vault using stolen token | All keys compromised | Vault tokens expire after 24h — no MFA on Vault | Critical |
| T-008 | Tampering | Attacker replaces a payment API key with their own | Payment diversion to attacker | No integrity checking on key retrieval | Critical |
| T-009 | Repudiation | Engineer exports production keys and claims they didn't | IP theft, key compromise | No audit on `vault read` operations | High |
| T-010 | Information Disclosure | Vault logs exposed to SIEM without redaction | Keys exposed in plaintext in logs | Vault audit logs sent to SIEM — not filtered | High |
| T-011 | Denial of Service | Vault sealed by repeated bad auth attempts | All services that need keys go down | Auto-unseal configured (single point of failure) | Critical |
| T-012 | Elevation of Privilege | CI/CD pipeline token scoped too broadly | Pipeline can access production keys | Token scoped to KV mount — not path-limited | High |

---

## System 3: Core Transaction Engine (CJ-003)

**Asset:** Java/Spring Boot application processing $8M/month in transactions

| Threat ID | STRIDE Category | Threat Description | Impact | Existing Control | Severity |
|-----------|----------------|-------------------|--------|-----------------|----------|
| T-013 | Spoofing | Attacker impersonates a trusted internal service via mTLS bypass | Fraudulent transactions | mTLS between services — not enforced for all | High |
| T-014 | Tampering | Man-in-the-middle modifies transaction amount during processing | Financial loss, reconciliation nightmare | TLS 1.3 in transit — internal traffic not encrypted | High |
| T-015 | Repudiation | Duplicate transaction processed and blamed on "system error" | Financial loss, audit findings | Idempotency keys on API — no dead-letter queue monitoring | Medium |
| T-016 | Information Disclosure | Error message leaks SQL query or stack trace | Reconnaissance data to attacker | Generic error responses — dev mode not disabled in prod | Medium |
| T-017 | Denial of Service | DDoS on public-facing API endpoint | Revenue loss ($267K/day) | CloudFront + WAF (basic rate limiting only) | Critical |
| T-018 | Elevation of Privilege | JWT token forged with escalated role permissions | Unauthorized admin actions | JWT signed with RS256 — public key exposed in client code | Critical |

---

## System 4: Source Code Repository (CJ-004)

**Asset:** GitHub Enterprise containing proprietary ML models and payment integration code

| Threat ID | STRIDE Category | Threat Description | Impact | Existing Control | Severity |
|-----------|----------------|-------------------|--------|-----------------|----------|
| T-019 | Spoofing | Attacker uses leaked GitHub PAT to clone private repos | Full source code + ML model theft | PATs scoped (some tokens have full repo scope) | Critical |
| T-020 | Tampering | Malicious PR merges backdoored code into production | Supply chain attack | Branch protection on main (not on release branches) | Critical |
| T-021 | Repudiation | Developer introduces vulnerability and denies it | No attribution for security incident | Commits are signed — signing not enforced | Medium |
| T-022 | Information Disclosure | Hardcoded secrets in code committed to repo | Cloud credentials, API keys exposed | pre-commit hooks (not used by all developers) | High |
| T-023 | Denial of Service | GitHub Actions crypto miner consumes all CI minutes | CI/CD pipeline unavailable | Self-hosted runners (no resource limits configured) | Medium |
| T-024 | Elevation of Privilege | Third-party GitHub App OAuth scope creep | External tool can read all repos | OAuth review process (not documented, not enforced) | High |

---

## Risk Scoring Legend

| Severity | Score | Definition |
|----------|-------|------------|
| Critical | 4 | Control gap — threat is realizable with no meaningful prevention |
| High | 3 | Partial control exists but could be bypassed |
| Medium | 2 | Control exists but is not enforced or monitored |
| Low | 1 | Control is effective and monitored |

---

## Top Threats by Residual Risk

| Rank | ID | Threat | System | Score |
|------|-----|--------|--------|-------|
| 1 | T-006 | DB privilege escalation | PII Database | Critical |
| 2 | T-012 | Over-scoped CI/CD Vault token | Key Vault | Critical |
| 3 | T-007 | Vault access without MFA | Key Vault | Critical |
| 4 | T-018 | JWT forged escalation | Transaction Engine | Critical |
| 5 | T-004 | SQL injection via API | PII Database | Critical |
| 6 | T-020 | Malicious PR in production | Source Code | Critical |
| 7 | T-008 | Payment key tampering | Key Vault | Critical |
| 8 | T-001 | Stolen DB credentials | PII Database | High |

---

## Recommended Controls

| Mitigation | Addressed Threats | Effort | Priority |
|------------|------------------|--------|----------|
| Deploy WAF with OWASP ruleset (SQLi, XSS) | T-004, T-017 | Medium | P0 |
| Enforce MFA on Vault authentication | T-007, T-009 | Low | P0 |
| Implement path-restricted Vault tokens for CI/CD | T-012, T-019 | Low | P0 |
| Enforce commit signing + branch protection on all branches | T-020, T-021 | Low | P1 |
| Rotate JWT signing keys + implement key rotation policy | T-018, T-006 | Medium | P1 |
| Deploy secret scanning in CI/CD pipeline | T-022, T-019 | Low | P1 |
| Encrypt internal service traffic (mTLS mesh) | T-013, T-014 | High | P2 |
| Implement user-level DB audit logging | T-003, T-006 | Medium | P2 |
