# Information Security Policy (Master)

**Document ID:** POL-01
**Version:** 1.0
**Effective Date:** 2026-01-15
**Approved By:** Board of Directors
**Owner:** CISO
**Review Cycle:** Annual

---

## 1. Purpose

This policy establishes NexPay Financial's commitment to information security and defines the principles, objectives, and responsibilities for protecting the confidentiality, integrity, and availability of all information assets. It serves as the foundation for all domain-specific security policies, standards, procedures, and guidelines.

---

## 2. Scope

This policy applies to:
- All employees, contractors, consultants, and temporary staff of NexPay Financial
- All third parties with access to NexPay information systems or data
- All information assets owned, leased, or managed by NexPay
- All systems, networks, applications, and data, regardless of location (on-premises, cloud, remote work)
- All devices used to access NexPay systems (corporate-managed and BYOD)

---

## 3. Policy Statements

### 3.1 Security Governance

3.1.1 The CISO is responsible for establishing, implementing, maintaining, and continuously improving the information security program.
3.1.2 The security program shall align with NIST Cybersecurity Framework (CSF) 2.0 and ISO/IEC 27001:2022.
3.1.3 The Board of Directors shall receive a quarterly security report detailing program status, KRIs, and risk posture.
3.1.4 The security program budget shall be approved annually as part of the corporate budgeting process.

### 3.2 Risk Management

3.2.1 Risk assessments shall be conducted at least annually and whenever significant changes occur to the business or technology environment.
3.2.2 All risks shall be documented in the corporate risk register with identified owners, treatment plans, and residual risk ratings.
3.2.3 Risk acceptance decisions must be documented and approved by the CISO (for Medium risks) or Board (for High/Critical risks).

### 3.3 Access Control

3.3.1 Access to information systems shall be granted based on the principle of least privilege.
3.3.2 All access shall be authorized by the data owner or system owner before provisioning.
3.3.3 Multi-factor authentication shall be required for all remote access, privileged accounts, and access to sensitive systems.
3.3.4 Access reviews shall be conducted quarterly for privileged accounts and annually for all other accounts.

### 3.4 Data Protection

3.4.1 Data shall be classified according to the Data Classification & Handling Policy and protected accordingly.
3.4.2 All sensitive data shall be encrypted at rest and in transit.
3.4.3 Data retention and disposal shall comply with legal, regulatory, and business requirements.

### 3.5 Incident Management

3.5.1 All security incidents shall be reported immediately to the Security team.
3.5.2 Incident response shall follow the documented Incident Response Policy and procedures.
3.5.3 Post-incident reviews shall be conducted for all confirmed incidents to identify root causes and preventive measures.

### 3.6 Business Continuity

3.6.1 Business continuity and disaster recovery plans shall be documented, tested annually, and updated based on test results.
3.6.2 Critical business processes shall have documented RTOs and RPOs.

### 3.7 Third-Party Security

3.7.1 All third parties with access to NexPay data or systems shall undergo security assessment commensurate with the risk tier of the engagement.
3.7.2 Contracts with third parties shall include security requirements, data protection obligations, and right-to-audit clauses.

### 3.8 Security Awareness

3.8.1 All employees shall complete security awareness training upon hire and annually thereafter.
3.8.2 Phishing simulation exercises shall be conducted at least quarterly.
3.8.3 Role-specific security training shall be provided for developers, IT operations, and privileged users.

### 3.9 Compliance

3.9.1 The organization shall maintain compliance with all applicable legal, regulatory, and contractual obligations.
3.9.2 SOC 2 Type II certification shall be achieved within 12 months of this policy's effective date.
3.9.3 Internal audits shall be conducted annually to assess compliance with this policy and supporting standards.

### 3.10 Continuous Improvement

3.10.1 Security metrics and KRIs shall be reviewed monthly by the Security team.
3.10.2 The security program maturity shall be assessed annually using the CMMI framework mapped to NIST CSF functions.
3.10.3 Lessons learned from incidents, audits, and exercises shall drive program improvements.

---

## 4. Roles & Responsibilities

| Role | Responsibility |
|------|---------------|
| Board of Directors | Approve security policy, oversee security program, review risk posture quarterly |
| CISO | Develop, implement, and maintain security program; report to Board |
| CTO | Implement technical security controls; ensure secure system architecture |
| VP Engineering | Ensure secure development practices; maintain code and infrastructure security |
| CFO | Ensure security budget; oversee cyber insurance program |
| All Employees | Comply with security policies; report incidents; complete training |
| HR | Ensure security awareness onboarding; track policy acknowledgment |
| Legal | Review security contracts; advise on regulatory compliance |
| Internal Audit | Assess policy compliance; report findings to Board |

---

## 5. Policy Compliance

5.1 Compliance with this policy is mandatory for all users within scope.
5.2 Violations may result in disciplinary action, up to and including termination of employment and legal action.
5.3 Managers are responsible for ensuring their teams understand and comply with this policy.
5.4 The Security team shall monitor compliance through automated tooling, audits, and manual reviews.

---

## 6. Exceptions Process

Any exception to this policy must follow the documented exceptions process:
1. Submit Policy Exception Request to CISO
2. Include business justification, compensating controls, and proposed duration
3. CISO review and approval (or Board for exceptions >30 days)
4. Exception tracked in risk register with expiry date
5. Maximum exception term: 12 months

---

## 7. Related Documents

| ID | Document |
|----|----------|
| POL-02 | Acceptable Use Policy |
| POL-03 | Data Classification & Handling Policy |
| POL-04 | Access Control Policy |
| POL-05 | Cryptography Policy |
| POL-06 | Physical Security Policy |
| POL-07 | Operations Security Policy |
| POL-08 | Incident Response Policy |
| POL-09 | Business Continuity Policy |
| POL-10 | Vendor Management Policy |
| POL-11 | Remote Work & BYOD Policy |
| POL-12 | Vulnerability Management Policy |

---

## 8. Review & Maintenance

This policy shall be reviewed annually by the CISO and updated as necessary. Changes to the business, regulatory environment, or threat landscape may trigger an unscheduled review. All policy changes require Board approval.

---

## 9. NIST CSF Mapping

| NIST CSF Function | Category | Policy Section |
|-------------------|----------|----------------|
| Govern (GV) | GV.OC, GV.RM, GV.SC | Sections 3.1, 3.2, 3.7 |
| Identify (ID) | ID.AM, ID.RA, ID.RM | Section 3.2 |
| Protect (PR) | PR.AC, PR.DS, PR.AT, PR.PS | Sections 3.3, 3.4, 3.8 |
| Detect (DE) | DE.CM, DE.AE | Section 3.5 |
| Respond (RS) | RS.MA, RS.CO, RS.AN | Section 3.5 |
| Recover (RC) | RC.RP, RC.IM | Section 3.6 |
