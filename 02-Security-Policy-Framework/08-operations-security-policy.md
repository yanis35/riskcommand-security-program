# Operations Security Policy

**Document ID:** POL-07
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CTO
**Review Cycle:** Annual

---

## 1. Purpose

Define operational security requirements for managing IT infrastructure, systems, and services securely.

---

## 2. Policy Requirements

### 2.1 Change Management
- All changes to production systems and configurations must follow the Change Management Process.
- Changes classified as: Standard (pre-approved), Normal (requires CAB review), Emergency (requires CTO/VP Eng approval).
- All changes must be documented: what, why, when, risk assessment, rollback plan, testing results.
- CAB meets weekly to review and approve Normal changes.

### 2.2 Configuration Management
- All systems must be configured following the Security Baseline Standards.
- Configuration drift must be detected via automated tooling (CSPM, configuration assessment).
- Gold images maintained for all server types, reviewed and updated at least quarterly.

### 2.3 Patch Management
- Critical security patches: applied within 7 days
- High security patches: applied within 30 days
- Medium/Low security patches: applied within 90 days
- Patch status must be monitored and reported monthly to CTO/CISO.

### 2.4 Backup & Recovery
- Backups must be performed for all L2+ data and critical systems.
- Backup frequency: L4 data — continuous/ hourly; L3 data — daily; L2 data — weekly.
- Backups must be encrypted and stored in a separate geographic region from primary data.
- Backup restoration tested quarterly, documented with results.

### 2.5 Logging & Monitoring
- All production systems must generate security-relevant logs.
- Logs must be forwarded to the SIEM and retained: 90 days hot, 1 year warm, 3 years cold for compliance data.
- Log integrity must be protected (write-once, append-only for critical systems).
- Monitoring alerts must be reviewed and triaged within defined SLAs.

### 2.6 Anti-Malware
- All endpoints must have EDR/anti-malware installed, active, and reporting to central console.
- Signature updates must occur at least daily.
- Scan schedules: full scan weekly, real-time scanning always enabled.

### 2.7 Cloud Security Operations
- Cloud security posture management (CSPM) must be deployed for all cloud environments.
- Public-facing cloud resources must be reviewed for misconfigurations daily.
- IAM policy review: monthly with automated least-privilege analysis.

### 2.8 Capacity Management
- System capacity must be monitored and reviewed monthly.
- Capacity alerts must trigger before thresholds are reached (70% CPU/memory → alert, 85% → auto-scale).

---

## 3. Related Documents

POL-01 (Information Security Policy), POL-04 (Access Control Policy), POL-12 (Vulnerability Management Policy)
