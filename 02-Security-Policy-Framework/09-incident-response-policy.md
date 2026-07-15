# Incident Response Policy

**Document ID:** POL-08
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** CISO
**Review Cycle:** Annual

---

## 1. Purpose

Establish a structured approach to detecting, reporting, responding to, and recovering from security incidents to minimize impact to the organization.

---

## 2. Scope

All security incidents affecting NexPay's information assets, systems, networks, facilities, or personnel.

---

## 3. Incident Classification

| Level | Definition | Examples | Response Time |
|-------|------------|----------|---------------|
| SEV-1 | Critical — active data breach, service outage, extortion | Ransomware, PII exfiltration, payment system down, APT detection | Immediate (≤15 min) |
| SEV-2 | High — confirmed malicious activity, data at risk | Malware outbreak, unauthorized access, DoS attack, credential theft | ≤1 hour |
| SEV-3 | Medium — potential incident, suspicious activity | Phishing click with credential entry, IDS alert, policy violation | ≤4 hours |
| SEV-4 | Low — informational, false positive | Phishing report (no interaction), vulnerability scan finding | ≤24 hours |

---

## 4. Incident Response Phases

### 4.1 Preparation
- Incident Response Plan documented and tested annually.
- IR team identified with on-call rotation (24/7 for SEV-1/SEV-2).
- Tools and access provisioned for IR team.
- Forensic readiness: logging enabled, evidence collection procedures documented.

### 4.2 Detection & Reporting
- All employees must report suspected security incidents immediately to security@nexpay.com or via the Phish Alert button.
- Automated detection: SIEM alerts, EDR alerts, CSPM alerts, IDS/IPS alerts.
- Third-party notifications: threat intel feeds, CVE notifications, partner breach disclosures.

### 4.3 Triage & Analysis
- Initial assessment: determine scope, severity, and impact.
- Containment strategy determined based on incident type:
  - Active breach → isolate affected systems (disconnect from network)
  - Ransomware → power off affected systems (do not reboot)
  - Malicious insiders → suspend accounts immediately
- Evidence preserved for forensic analysis.

### 4.4 Containment & Eradication
- Short-term containment: block IPs, disable accounts, isolate systems.
- Long-term containment: apply patches, change credentials, rebuild systems.
- Eradication: remove malware, close vulnerabilities, revoke compromised credentials.

### 4.5 Recovery
- Restore systems from clean backups.
- Verify integrity before returning to production.
- Monitor restored systems for recurrence (72-hour enhanced monitoring window).

### 4.6 Post-Incident Review
- Conduct within 5 business days of SEV-1/SEV-2 closure, within 10 days for SEV-3.
- Document: root cause, timeline, effectiveness of response, lessons learned, remediation actions.
- Remediation items tracked in risk register with owners and deadlines.

---

## 5. Communication

| Audience | Notification | Responsible |
|----------|-------------|-------------|
| Internal Security Team | Immediate (Slack, PagerDuty) | On-call IR lead |
| Executive Leadership | SEV-1/SEV-2 within 1 hour | CISO |
| Board of Directors | SEV-1 within 4 hours | CISO |
| Legal Counsel | SEV-1/SEV-2 immediately | CISO |
| Customers (if PII affected) | Per regulatory timeline (GDPR: 72 hours) | CISO + Legal |
| Regulators | Per applicable regulation | Legal |
| Law Enforcement | SEV-1 with criminal element | CISO + Legal |

---

## 6. Related Documents

POL-09 (Business Continuity Policy), POL-03 (Data Classification & Handling Policy), POL-01 (Information Security Policy)
