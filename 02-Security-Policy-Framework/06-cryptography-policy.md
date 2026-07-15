# Cryptography Policy

**Document ID:** POL-05
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CTO
**Review Cycle:** Annual

---

## 1. Purpose

Define cryptographic control requirements to protect the confidentiality, integrity, and authenticity of NexPay data in transit, at rest, and during processing.

---

## 2. Policy Requirements

### 2.1 Encryption at Rest
- All L3 and L4 data must be encrypted at rest using AES-256 or equivalent.
- Cloud storage (S3, EBS, RDS) must use KMS-managed keys with automatic key rotation (annual minimum).
- Database encryption: TDE or column-level encryption for L4 fields.
- Backup encryption: All backups containing L3/L4 data must be encrypted.

### 2.2 Encryption in Transit
- All external-facing services must use TLS 1.3 with strong cipher suites.
- Internal service-to-service communication must use TLS 1.2 minimum (mTLS preferred for critical paths).
- HTTPS is required for all web applications. HSTS must be enabled.
- Email in transit: TLS required for mail server-to-server communication.

### 2.3 Key Management
- All cryptographic keys must be managed through a centralized key management system (AWS KMS or equivalent HSM).
- Key rotation requirements:
  - Customer master keys: annually
  - Data encryption keys: per AWS automatic rotation
  - TLS certificates: every 13 months (automated via ACM)
  - SSH keys: quarterly
  - PGP keys: annually
- Keys must be stored separately from the data they protect.
- HSM (Hardware Security Module) required for payment signing keys.

### 2.4 Approved Algorithms

| Use Case | Approved Algorithm | Key Length | Notes |
|----------|-------------------|------------|-------|
| Symmetric encryption | AES-256-GCM | 256-bit | Preferred for data at rest |
| Asymmetric encryption | RSA-OAEP | 4096-bit | Key exchange, PGP |
| Digital signatures | ECDSA (P-384) | 384-bit | Code signing, JWT |
| Hashing | SHA-256, SHA-384 | — | Integrity verification |
| Key agreement | ECDH (P-384) | 384-bit | TLS key exchange |
| JWT signing | RS384 or ES384 | 384-bit | API authentication |

### 2.5 Prohibited Algorithms
- DES, 3DES, RC4, MD5, SHA-1 (for signatures), SSL 3.0, TLS 1.0/1.1
- Custom cryptography — only NIST-approved, publicly reviewed algorithms may be used.

### 2.6 Certificate Management
- All internal CAs must be managed through a Public Key Infrastructure (PKI).
- Certificate expiry must be monitored with automated alerts at 30, 14, and 7 days.
- Certificate transparency logging required for all public-facing certificates.

---

## 3. Related Documents

POL-01 (Information Security Policy), POL-03 (Data Classification & Handling Policy), POL-04 (Access Control Policy)
