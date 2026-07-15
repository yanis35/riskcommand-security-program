# GoPhish Campaign Design — Security Awareness Program

**Phase:** 4 — Security Awareness & Phishing Program
**Objective:** Deploy multi-wave phishing simulation campaigns to measure baseline risk, train users, and track improvement over 4 quarters
**Tool:** GoPhish (self-hosted)
**Scope:** All 200 employees
**Cadence:** Quarterly campaigns (4 waves per quarter → 16 total over 12 months)

---

## Campaign Framework

| Wave | Type | Difficulty | Schedule | Objective |
|------|------|------------|----------|-----------|
| 1 | Generic phishing | Low — obvious phish | Month 1 | Establish baseline click rate |
| 2 | Spear phishing (OSINT) | Medium — personalized | Month 2 | Test personalized targeting |
| 3 | CEO impersonation (BEC) | High — urgent, authoritative | Month 3 | Test authority-based attacks |
| 4 | Credential harvest (cloned login) | High — convincing pretext | Month 4 | Test credential theft resilience |

**Quarterly repeat:** Same 4 waves repeated each quarter with updated lures and pretexts

---

## Infrastructure Setup

| Component | Configuration |
|-----------|---------------|
| GoPhish server | AWS EC2 t3.small, Ubuntu 22.04, Elastic IP |
| Sending domain | security-notice.nexpay.com (registered, SPF/DKIM/DMARC configured) |
| Landing page | Internal phishing awareness page (notify users they "failed") |
| Sending profile | SMTP relay via AWS SES (authenticated, dedicated IP) |
| Target list | HR export via CSV (name, email, department, role) — updated monthly |

---

## Wave Templates

### Wave 1 — Generic Phishing

| Field | Value |
|-------|-------|
| Subject | "Your package is waiting — confirm delivery" |
| Sender | "FedEx Delivery" <delivery@fedex-notify.com> |
| Pretext | Fake FedEx tracking link — obvious red flags |
| Red Flags | Misspelled domain, generic greeting, urgency without context |
| Landing Page | "You clicked a simulated phishing email. This was a test. Here's what to look for..." |
| Expected Baseline Click Rate | Industry average: 25–30% |

### Wave 2 — Spear Phishing (OSINT)

| Field | Value |
|-------|-------|
| Subject | "Your [Department] team offsite — RSVP required" |
| Sender | "HR Team" <hr-events@nexpay-hr.com> |
| Pretext | Personalized email referencing the employee's actual department and manager name (gathered from LinkedIn, company website) |
| Personalization | First name, department name, manager name |
| Landing Page | Training page specific to spear phishing indicators |

### Wave 3 — CEO Impersonation (BEC)

| Field | Value |
|-------|-------|
| Subject | "URGENT: Wire transfer needed before EOD" |
| Sender | "John Chen — CEO" <john.chen@nexpay-exec.com> |
| Pretext | CEO is in meetings all day, needs an urgent wire transfer to a "new vendor" — wire $12,450 to account provided |
| Targeting | Finance team + executives + AP department |
| Landing Page | BEC-specific training (verify via phone, confirm with secondary contact) |

### Wave 4 — Credential Harvest (Cloned Login Page)

| Field | Value |
|-------|-------|
| Subject | "Suspicious login attempt — verify your account" |
| Sender | "Okta Security" <security@okta-verify.net> |
| Pretext | "We detected a login attempt from [City, Country]. Verify your account to prevent suspension." |
| Attack Type | Cloned Okta login page (hosted on GoPhish) — captures username + password + MFA code |
| Landing Page | "Your credentials were captured in a simulated phishing attack. This is what a real credential harvest looks like." |
| **This is the most important metric** | Credential submission rate is the strongest predictor of real-world compromise risk |

---

## User Segmentation

| Segment | Users | Risk Level | Notes |
|---------|-------|------------|-------|
| Finance & Accounting | 12 | High | Access to wire transfers, AP, payroll |
| Executives & Board | 8 | High | BEC targets, access to sensitive data |
| Engineering (privileged) | 35 | High | Source code, cloud access, prod data |
| Customer Support | 25 | Medium | PII access, customer data |
| Engineering (non-privileged) | 20 | Medium | Internal systems |
| Sales & Marketing | 40 | Low | Limited system access |
| Operations & Admin | 30 | Low | Limited system access |
| Contractors & Interns | 30 | Medium | Less security awareness experience |

---

## Training & Remediation

| Click Behavior | Consequence |
|----------------|-------------|
| First click (any wave) | Automatic enrollment in 15-minute interactive phishing training module |
| Second click (any wave) | 1-on-1 security coaching session with manager + Security team |
| Third click (any wave) | Escalated to HR — mandatory security training retake + written acknowledgment |
| Click + credential submission | Immediate password reset + MFA re-enrollment + security coaching |
| Report phishing (any user) | Positive reinforcement — "Thank you for reporting!" message + swag points |

---

## Reporting Metrics

| Metric | Target (Q4) | Measurement |
|--------|-------------|-------------|
| Baseline click rate | ≤30% (Q1) → ≤5% (Q4) | GoPhish campaign statistics |
| Credential submission rate | ≤2% (Q4) | GoPhish landing page submissions |
| Phishing report rate | ≥50% of all simulated emails reported (Q4) | Phish Alert Button + GoPhish "reported" tracking |
| Mean time to report | ≤15 minutes from email receipt (Q4) | GoPhish timestamp analysis |
| Repeat clicker rate | ≤5% of employees (Q4) | Users with 2+ clicks across campaigns |
| Training completion | 100% (all employees) | LMS completion records |
