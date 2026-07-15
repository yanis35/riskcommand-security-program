# Access Control Policy

**Document ID:** POL-04
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CTO
**Review Cycle:** Annual

---

## 1. Purpose

Define access control requirements to ensure that access to information systems and data is authorized, granted on a least-privilege basis, and reviewed regularly.

---

## 2. Scope

All users, systems, applications, networks, and data repositories within NexPay's environment.

---

## 3. Policy Requirements

### 3.1 Identity Management
- All users must have a unique digital identity (user account) before accessing any system.
- Shared accounts are prohibited except for emergency break-glass accounts which must be logged and audited.
- Identity lifecycle: provision → enable → review → disable → archive → delete.

### 3.2 Authentication
- All accounts must be protected by passwords meeting the Password Standard (minimum 14 characters, complexity required).
- MFA is mandatory for: privileged accounts, remote access, access to L4 data, vendor portals, and email.
- Biometric or hardware-token-based MFA is preferred over SMS-based MFA.

### 3.3 Authorization
- Access is granted based on the principle of least privilege: users receive only the permissions required for their role.
- Role-Based Access Control (RBAC) shall be implemented for all systems where feasible.
- Privileged access (admin, root, domain admin) requires separate privileged accounts and approval from the system owner.

### 3.4 Just-in-Time Access
- Privileged access to production systems and L4 data shall use just-in-time (JIT) elevation.
- JIT requests require: business justification, approval, and automatic revocation after the approved window.

### 3.5 Access Reviews
- Privileged account reviews: quarterly
- All other account reviews: annually
- Reviews must verify: access is still needed, level is appropriate, no segregation-of-duty conflicts
- Review results documented with remediation tracking for any findings

### 3.6 Termination & Transfers
- Upon employee termination: all access revoked within 4 hours of HR notification.
- Upon role change: access reviewed and adjusted within 5 business days.
- Service accounts: reviewed quarterly, passwords rotated on review cycle.

### 3.7 Remote Access
- Remote access to internal systems requires VPN + MFA.
- Third-party remote access requires approval, limited duration, and session recording.

### 3.8 API & Programmatic Access
- API tokens must be scoped to the minimum required permissions.
- Tokens must expire and be rotated (service accounts: 90 days, machine-to-machine: 1 year).
- Static credentials in code are prohibited (use secrets management).

---

## 4. Access Control Model

```
User → Authentication (MFA) → Authorization (RBAC) → Resource
                               ↓
                        Just-in-Time Elevation
                        (for privileged actions)
```

---

## 5. Related Documents

POL-01 (Information Security Policy), POL-11 (Remote Work & BYOD Policy), POL-12 (Vulnerability Management Policy)
