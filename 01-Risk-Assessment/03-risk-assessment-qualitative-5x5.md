# Risk Assessment — Qualitative (5x5 Matrix)

**Phase:** 1 — Risk Assessment & Crown Jewels Analysis
**Objective:** Evaluate top risks using a qualitative 5x5 likelihood × impact matrix
**Framework:** ISO 31000, NIST SP 800-30
**Scope:** Top 25 identified risks from STRIDE analysis + business context

---

## Risk Scoring Methodology

Risk is calculated as: **Risk Score = Likelihood × Impact**

| Score | Likelihood | Impact |
|-------|------------|--------|
| 5 | Almost Certain (≥90%) | Catastrophic (>$10M loss, regulatory action, company survival) |
| 4 | Likely (50–89%) | Major ($1M–$10M loss, reputational damage, client loss) |
| 3 | Possible (20–49%) | Moderate ($100K–$1M loss, operational disruption) |
| 2 | Unlikely (5–19%) | Minor ($10K–$100K loss, temporary inconvenience) |
| 1 | Rare (<5%) | Insignificant (<$10K loss, no external impact) |

**Risk Rating:** Critical (15–25), High (10–14), Medium (5–9), Low (1–4)

---

## Risk Register — Qualitative Assessment

### Critical Risks (Score 15–25)

| # | Risk | Threat | L | I | Score | Current Controls | Residual |
|---|------|--------|---|----|----|-----------------|----------|
| R-01 | Customer PII exfiltrated via SQL injection | T-004 | 4 | 5 | **20** | WAF (no SQLi rules), RDS encryption at rest | Critical |
| R-02 | Payment keys stolen via Vault compromise | T-007 | 4 | 5 | **20** | Token-based auth (no MFA), 24h token expiry | Critical |
| R-03 | DB privilege escalation leads to full data compromise | T-006 | 4 | 5 | **20** | IAM roles (over-permissioned), no row-level security | Critical |
| R-04 | Malicious PR merges backdoor into production | T-020 | 4 | 5 | **20** | Branch protection on main only, no code review enforcement | Critical |
| R-05 | JWT token forged with elevated privileges | T-018 | 3 | 5 | **15** | RS256 signing, public key exposed, no key rotation | Critical |
| R-06 | DDoS takes down transaction engine | T-017 | 4 | 4 | **16** | CloudFront + basic rate limiting, no WAF DDoS protection | Critical |
| R-07 | Over-scoped CI/CD token reads all Vault secrets | T-012 | 4 | 4 | **16** | Token scoped to KV mount, not path-limited | Critical |
| R-08 | Payment key replaced by attacker | T-008 | 3 | 5 | **15** | Static keys, no integrity verification on retrieval | Critical |

### High Risks (Score 10–14)

| # | Risk | Threat | L | I | Score | Current Controls | Residual |
|---|------|--------|---|----|----|-----------------|----------|
| R-09 | Stolen engineer credentials used to access PII DB | T-001 | 4 | 3 | **12** | IAM roles + static creds for some services | High |
| R-10 | Secrets committed to public repo | T-022 | 4 | 3 | **12** | pre-commit hooks (not enforced) | High |
| R-11 | ML model exfiltrated from S3 | T-019 | 3 | 4 | **12** | S3 server-side encryption, no access logging | High |
| R-12 | Supply chain via third-party GitHub App | T-024 | 3 | 4 | **12** | No OAuth scope review process | High |
| R-13 | Insider denies unauthorized DB query | T-003 | 3 | 3 | **9** | CloudTrail enabled, no user-level audit | High |
| R-14 | RDS instance overwhelmed — app outage | T-005 | 3 | 3 | **9** | RDS auto-scaling (not tested) | High |

### Medium Risks (Score 5–9)

| # | Risk | Threat | L | I | Score | Current Controls | Residual |
|---|------|--------|---|----|----|-----------------|----------|
| R-15 | Vault audit logs leak keys in SIEM | T-010 | 3 | 2 | **6** | Audit logging enabled, no redaction | Medium |
| R-16 | mTLS bypass allows service impersonation | T-013 | 2 | 4 | **8** | mTLS partially deployed | Medium |
| R-17 | Internal traffic not encrypted | T-014 | 3 | 2 | **6** | TLS for external, no internal encryption | Medium |
| R-18 | Duplicate transaction processed | T-015 | 2 | 3 | **6** | Idempotency keys, no dead-letter monitoring | Medium |
| R-19 | Error message leaks stack trace | T-016 | 2 | 2 | **4** | Generic error responses configured | Low |
| R-20 | GH Actions crypto miner uses all CI minutes | T-023 | 2 | 2 | **4** | Self-hosted runners, no resource limits | Low |

---

## Risk Heatmap

```
Impact →
    1     2     3     4     5
L  ┌──────────────────────────┐
i  5 │      │      │      │      │ R-01 │
k  │      │      │      │      │ R-02 │
e  │      │      │      │      │ R-03 │
l  ├──────┼──────┼──────┼──────┼──────┤
i  4 │      │      │ R-09 │ R-06 │ R-01 │
h  │      │      │ R-10 │ R-07 │ R-02 │
o  │      │      │      │      │ R-03 │
o  ├──────┼──────┼──────┼──────┼──────┤
d  3 │      │ R-15 │ R-05 │ R-08 │      │
↓  │      │ R-14 │ R-13 │ R-04 │      │
   │      │ R-17 │ R-12 │      │      │
   ├──────┼──────┼──────┼──────┼──────┤
   2 │      │ R-19 │ R-16 │      │      │
   │      │ R-20 │      │      │      │
   │      │ R-18 │      │      │      │
   ├──────┼──────┼──────┼──────┼──────┤
   1 │      │      │      │      │      │
   └──────────────────────────┘
```

| Color | Zone | Action |
|-------|------|--------|
| Red | Critical (15–25) | Immediate remediation — within 30 days |
| Orange | High (10–14) | Remediate within 90 days |
| Yellow | Medium (5–9) | Include in backlog, remediate within 6 months |
| Green | Low (1–4) | Accept or monitor |

---

## Risk Treatment Decisions

| Risk ID | Treatment | Rationale | Timeline | Cost Est. |
|---------|-----------|-----------|----------|-----------|
| R-01 | Mitigate | Deploy WAF with OWASP SQLi ruleset | 2 weeks | $5K |
| R-02 | Mitigate | Enable MFA on Vault + rotate tokens | 1 week | $2K |
| R-03 | Mitigate | Implement row-level security + least privilege DB roles | 4 weeks | $10K |
| R-04 | Mitigate | Enforce branch protection + required reviews on all branches | 1 week | $0 |
| R-05 | Mitigate | Replace JWT key, implement key rotation policy | 2 weeks | $3K |
| R-06 | Mitigate | Deploy AWS WAF with DDoS protection + Shield Advanced | 3 weeks | $8K/mo |
| R-11 | Mitigate | S3 bucket policy + access logging + encryption with KMS | 1 week | $1K |
| R-12 | Mitigate | Implement OAuth app review process + scope auditing | 2 weeks | $0 |

**Risk Transfer:** Cyber insurance policy ($15K/year — covers breach response, ransomware, business interruption)

**Risk Acceptance (with monitoring):** R-15 (Vault log exposure — low likelihood, will be addressed in SIEM v2)

---

## Next Steps

1. Present critical risks to board with recommended remediation budget ($30K one-time, $8K/month ongoing)
2. Begin remediation of top 5 critical risks (R-01 through R-05) immediately
3. Update risk register monthly with control effectiveness data
4. Prepare FAIR quantitative analysis for top 10 risks (see companion document)
