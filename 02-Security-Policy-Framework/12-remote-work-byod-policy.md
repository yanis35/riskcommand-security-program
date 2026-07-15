# Remote Work & BYOD Policy

**Document ID:** POL-11
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CTO
**Review Cycle:** Annual

---

## 1. Purpose

Define security requirements for employees working remotely and using personal devices (BYOD) for business purposes.

---

## 2. Scope

All employees who work remotely (home, co-working, travel) and all personal devices used to access NexPay corporate resources.

---

## 3. Policy Requirements

### 3.1 Remote Work Requirements
- All remote access to NexPay resources must be through the corporate VPN with MFA.
- Work must not be performed from public or untrusted networks (cafe Wi-Fi, hotel business centers) unless using corporate VPN.
- VPN must use split-tunneling disabled (all traffic routed through corporate network).
- Remote workers must maintain a physically secure workspace — screens not visible to others, devices locked when unattended.

### 3.2 BYOD Requirements
- BYOD devices must run a supported operating system (latest OS version + latest security patches).
- Minimum requirements: screen lock (PIN/biometric), full-disk encryption, remote wipe capability.
- Corporate MDM (Mobile Device Management) profile must be installed:
  - Enforces device PIN (6+ digits)
  - Enforces encryption
  - Enables remote wipe of corporate data
  - Disables jailbreak/root detection
- Company data must not be stored locally on personal devices — use approved cloud apps or virtual desktop.
- NexPay reserves the right to wipe corporate data from personal devices upon termination or security incident.

### 3.3 Corporate-Issued Devices
- Corporate laptops must be managed via MDM with full configuration enforcement.
- Full-disk encryption is mandatory on all corporate laptops.
- Endpoint protection (EDR) must be installed, active, and reporting to central console.
- Lost or stolen devices must be reported within 1 hour — remote wipe initiated immediately.

### 3.4 Prohibited in Remote/BYOD Context
- Use of personal cloud storage for company data (Google Drive, Dropbox, iCloud)
- Use of public file-sharing services for L3+ data
- Installation of unapproved software on corporate devices
- Connection to untrusted Wi-Fi without VPN
- Family member or third-party access to corporate devices

### 3.5 Termination
- Upon termination: VPN certificates revoked, MDM profiles removed, corporate data wiped from BYOD devices.
- Corporate devices must be returned within 5 business days and securely wiped before reassignment.

---

## 4. Related Documents

POL-01 (Information Security Policy), POL-02 (Acceptable Use Policy), POL-04 (Access Control Policy)
