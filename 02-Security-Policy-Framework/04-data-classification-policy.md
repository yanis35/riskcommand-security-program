# Data Classification & Handling Policy

**Document ID:** POL-03
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CISO
**Review Cycle:** Annual

---

## 1. Purpose

Establish a data classification framework to ensure information is protected commensurate with its sensitivity, value, and regulatory requirements throughout its lifecycle.

---

## 2. Classification Levels

| Level | Label | Definition | Examples | Regulatory |
|-------|-------|------------|----------|------------|
| L4 | Restricted | Unauthorized disclosure causes severe harm to organization or individuals | PII (SSN, bank accounts, KYC), payment card data, cryptographic keys | GDPR, CCPA, PCI DSS |
| L3 | Confidential | Unauthorized disclosure causes material harm to business | Source code, ML models, financial reports, customer contracts, board materials | SOC 2, IP law |
| L2 | Internal | Unauthorized disclosure causes minor operational impact | Internal policies, org charts, project plans, internal wikis | — |
| L1 | Public | Authorized for public release | Marketing materials, job postings, press releases | — |

---

## 3. Handling Requirements by Level

| Requirement | L1 Public | L2 Internal | L3 Confidential | L4 Restricted |
|-------------|-----------|-------------|-----------------|---------------|
| Encryption at rest | Not required | Recommended | Required (AES-256) | Required (AES-256 + KMS) |
| Encryption in transit | Not required | Recommended | Required (TLS 1.3) | Required (TLS 1.3 + mTLS) |
| Access control | None | User authentication | Role-based + least privilege | Role-based + JIT + MFA + audit |
| Retention period | As needed | Per business need | Per legal/compliance schedule | Defined per regulation |
| Disposal method | None | Overwrite | Cryptographic erase | Physical destruction + certificate |
| Sharing with third parties | Unlimited | Contract required | NDA + contract + assessment | NDA + contract + SIG + SOC 2 review |
| Incident notification | Not required | Internal only | CISO + Legal | CISO + Legal + Board + Regulator |
| Labeling | Optional | Recommended | Required (header/footer/metadata) | Required (header/footer/metadata + system tags) |

---

## 4. Data Lifecycle

### 4.1 Creation
- Data creators must classify data at the time of creation.
- Automated classification tools may be used to assist, but the creator retains accountability.

### 4.2 Storage
- L3/L4 data must be stored only in approved, encrypted repositories (AWS environments with KMS, approved SaaS with SOC 2 reports).
- L3/L4 data is prohibited from personal devices, USB drives, and unsanctioned cloud services.

### 4.3 Transmission
- L3/L4 data transmitted externally must use encrypted channels (SFTP, HTTPS, encrypted email).
- Internal transmission of L4 data must use approved secure file transfer mechanisms with audit logging.

### 4.4 Retention
- Data retention periods are defined in the Data Retention Schedule maintained by Legal.
- Data must be securely disposed upon expiration of the retention period.

### 4.5 Disposal
- L1: Standard deletion
- L2: Overwrite or degauss
- L3: Cryptographic erase or certified shredding
- L4: Cryptographic erase + physical destruction of media + certificate of destruction

---

## 5. Data Owner Responsibilities

- Classify data under their purview
- Review classification annually
- Approve access requests
- Ensure handling requirements are met
- Report data incidents immediately

---

## 6. Related Documents

POL-01 (Information Security Policy), POL-05 (Cryptography Policy), POL-04 (Access Control Policy)
