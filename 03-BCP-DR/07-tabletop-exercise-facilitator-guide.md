# Tabletop Exercise — Facilitator Guide

**Phase:** 3 — BCP/DR with Tested Runbooks
**Scenario:** Ransomware Attack + Key Person Loss (combined inject)
**Duration:** 3 hours (including debrief)
**Participants:** CISO, CTO, VP Eng, CFO, Legal, VP CS, PR Lead, Security Team Lead
**Facilitator:** CISO (or external IR consultant)
**Observers:** Internal Audit, Board Representative

---

## Exercise Objectives

1. Test the organization's ability to detect, contain, and respond to a ransomware incident
2. Test the BCP/DR plan activation and decision-making process
3. Test communication protocols (internal, customer, regulatory, press)
4. Identify gaps in runbooks, tooling, cross-training, and decision authority
5. Validate RTO/RPO assumptions under realistic pressure

---

## Exercise Structure

| Phase | Duration | Activity |
|-------|----------|----------|
| Briefing | 15 min | Rules of engagement, scenario overview, participant introductions |
| Inject 1 | 30 min | Initial ransomware detection |
| Inject 2 | 20 min | Ransom demand + data exfiltration evidence |
| Inject 3 | 15 min | Key person unavailable (backup admin on vacation) |
| Inject 4 | 20 min | Customer notification decision |
| Inject 5 | 15 min | Press inquiry |
| Inject 6 | 20 min | Recovery decision |
| Facilitator Pivot | 10 min | Curveball: backups are also encrypted |
| Debrief | 45 min | After-action review, lessons learned, action items |

---

## Scenario Background

**Setting:** Friday, 2:00 AM. The on-call engineer receives an EDR alert: "Ransomware detected — file encryption in progress." The alert covers 15 endpoints and 3 production servers in the us-east-1 region. The on-call engineer escalates to the Security team.

The company has been operating for 18 months with a partially implemented security program. Some controls are in place (EDR, SIEM, MFA for privileged users), but others are not (no HSM, partial backups, no cross-region DR).

---

## Inject 1 — Initial Detection (T+0)

**Time:** Friday, 2:00 AM

**Situation:** The on-call Security Engineer reports:
- Ransomware detected on: 2 developer laptops, 1 CI/CD build server, 1 production web server, 1 database read replica
- Ransomware variant identified: looks like LockBit 3.0
- Ransom note demands 50 BTC (~$3.5M)
- Affected servers are in us-east-1

**Questions for participants:**
1. What is your immediate response (first 15 minutes)?
2. Who needs to be notified and when?
3. Do you isolate affected systems? How?
4. Do you power off affected systems? Why or why not?
5. What is your initial containment strategy?

---

## Inject 2 — Escalation (T+45min)

**Time:** Friday, 2:45 AM

**Situation:** During investigation, the Security team discovers evidence of data exfiltration. The attacker exfiltrated approximately 200GB of data from the PII database before triggering the ransomware. The stolen data appears to include customer names, SSNs, and bank account numbers.

The ransom note has been updated: now demands 75 BTC ($5.25M) and threatens to release the stolen data on a dark web leak site within 48 hours if not paid.

**Questions for participants:**
1. Does this change your response strategy? How?
2. Who needs to be notified now that data has been exfiltrated?
3. Do you pay the ransom? Why or why not?
4. What is the GDPR 72-hour notification timeline? Do you have enough information yet?
5. Who makes the decision to involve law enforcement?

---

## Inject 3 — Compounding Issue (T+1hr 15min)

**Time:** Friday, 3:15 AM

**Situation:** The Security team lead attempts to reach the backup administrator — the only person who has performed a full database restore in the past 6 months. The backup admin is on vacation in a remote area with no cell service and is unreachable.

The backup restore procedure is documented, but it hasn't been followed in over 8 months and significant infrastructure changes have occurred since.

**Questions for participants:**
1. The backup admin is unavailable. What do you do?
2. Is anyone else cross-trained on database restore? Who?
3. What is your confidence level in the documented restore procedure?
4. Does this change your RTO estimate? By how much?
5. What's your backup restore plan at this point?

---

## Inject 4 — Customer Notification (T+1hr 45min)

**Time:** Friday, 3:45 AM

**Situation:** Legal counsel advises that based on the data exfiltration evidence, this incident likely meets the threshold for GDPR breach notification. However, the full scope of affected customers is not yet known.

One of NexPay's enterprise customers (a publicly traded company, 15% of revenue) has already detected unusual activity and is asking questions. Their CISO is emailing your CTO.

**Questions for participants:**
1. Do you notify affected customers now or wait for more information?
2. What do you tell the enterprise customer who is asking questions?
3. What is the GDPR 72-hour notification trigger? Have you met it?
4. Who drafts the customer communication? Who approves it?
5. Do you issue a press release or wait?

---

## Inject 5 — Press Inquiry (T+2hr 15min)

**Time:** Friday, 4:15 AM

**Situation:** A cybersecurity news outlet (e.g., BleepingComputer, KrebsOnSecurity) has published a brief article: "Fintech Startup NexPay Hit by Ransomware — LockBit Claims Responsibility." The article includes screenshots of the ransom note and mentions "customer data allegedly stolen."

Your CEO has just woken up to find 15 text messages and is calling the CISO.

**Questions for participants:**
1. How do you respond to the press inquiry?
2. What do you tell the CEO?
3. Do you issue a statement or say "no comment"?
4. Who is authorized to speak to the press?
5. What information do you share publicly vs. keep confidential?

---

## Inject 6 — Recovery Decision (T+2hr 45min)

**Time:** Friday, 5:00 AM

**Situation:** The Security team has confirmed:
- 35 systems affected total (spread across dev, staging, and production)
- Immutable backups are confirmed intact for the primary RDS database
- 6 application servers need to be rebuilt from golden images
- Estimated recovery time using current runbooks: 12-18 hours
- Customer PII was exfiltrated — estimated 200K records affected
- Ransom demand: 75 BTC ($5.25M) — deadline now 43 hours away

The CEO on the phone: "Can we be back online by 8 AM Monday? We have a board meeting at 10 AM."

**Questions for participants:**
1. What is your revised RTO estimate?
2. Do you activate the DR site? Or restore in place?
3. What do you tell the CEO?
4. What is your message to the board?
5. What resources do you need right now that you don't have?

---

## Facilitator Pivot — Curveball (T+3hr 15min)

**Time:** Friday, 5:15 AM

**Surprise inject (revealed by facilitator after recovery discussion):** Upon attempting to restore from immutable backups, DevOps discovers that the backup vault's access keys were also compromised. The backups are intact but the restore process requires MFA which uses an authenticator app on the backup admin's phone — who is still unreachable on vacation.

**Questions for participants:**
1. Your backup restore path is blocked. What now?
2. Does anyone have access to the backup vault? How do you recover?
3. Do you have a secondary backup method? Is it tested?

---

## Exercise Conclusion

**Time:** Friday, 6:00 AM (exercise ends)

Participants step out of scenario. Debrief begins.

---

## Evaluation Criteria

| Capability | Rating (1–5) | Observations |
|------------|--------------|-------------|
| Detection speed | | |
| Containment effectiveness | | |
| Decision-making under pressure | | |
| Communication clarity | | |
| Runbook completeness | | |
| Cross-team coordination | | |
| Leadership escalation | | |
| Stakeholder management | | |
| Recovery planning | | |
| Overall readiness | | |

**Rating Scale:** 1 = Not demonstrated, 2 = Needs improvement, 3 = Adequate, 4 = Effective, 5 = Highly effective
