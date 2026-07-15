# Tabletop Exercise — After-Action Report

**Phase:** 3 — BCP/DR with Tested Runbooks
**Exercise Date:** 2026-01-20
**Scenario:** Ransomware Attack + Key Person Loss
**Facilitator:** CISO
**Participants:** CISO, CTO, VP Eng, CFO, Legal Counsel, VP CS, PR Lead, Security Team Lead
**Observers:** Internal Audit Director

---

## Executive Summary

The tabletop exercise evaluated NexPay's preparedness for a combined ransomware + data exfiltration + key person loss scenario. The organization demonstrated strong detection capabilities but significant gaps in recovery procedures, runbook completeness, cross-training, and crisis communication.

**Overall Readiness Rating: 2.8 / 5** — "Needs Improvement"

---

## Exercise Results

### Detection: Rating 4 / 5

| Strengths | Weaknesses |
|-----------|------------|
| EDR detected ransomware within minutes | No automated alert to on-call escalation |
| Security team identified ransomware variant quickly | SIEM correlation rules did not trigger on exfiltration indicators |
| Network isolation procedures were effective | — |

### Containment: Rating 3 / 5

| Strengths | Weaknesses |
|-----------|------------|
| Quick network isolation of affected systems | Delayed decision on whether to power off or isolate |
| Effective credential rotation process | No playbook for Vault forensic preservation |
| — | MFA recovery process undocumented |

### Decision-Making: Rating 2 / 5

| Strengths | Weaknesses |
|-----------|------------|
| CISO made clear go/no-go decisions | Significant delay in data exfiltration discovery — SIEM gap |
| Team correctly chose not to pay ransom | No pre-defined decision tree for ransom vs. recovery |
| — | Backup admin unavailability caused 30+ minute debate on next steps |

### Communication: Rating 2 / 5

| Strengths | Weaknesses |
|-----------|------------|
| Legal counsel provided clear regulatory guidance | No pre-approved customer communication templates |
| — | No crisis communication plan for press inquiries |
| — | CEO was not briefed before reading about incident in news |
| — | Board notification timeline exceeded target (target: 4 hours, actual: 6+ hours) |

### Runbook Completeness: Rating 2 / 5

| Strengths | Weaknesses |
|-----------|------------|
| Ransomware runbook provided good high-level guidance | Backup restore procedure incomplete — assumes backup admin is available |
| — | No runbook for Vault access during an incident |
| — | No runbook for customer notification decision-making |
| — | DR failover runbook assumes primary infrastructure intact |

### Recovery Planning: Rating 3 / 5

| Strengths | Weaknesses |
|-----------|------------|
| Team confidently identified recovery path | RTO estimate (12–18 hours) exceeds 4-hour target |
| Immutable backups confirmed intact | Cross-region DR not yet configured — single region dependency |
| — | Backup restore MFA dependency on unreachable person |

---

## Key Findings

### Finding 1: Backup Admin Single Point of Failure

**Severity:** Critical
**Description:** The only person who has performed a full database restore is unreachable. The documented restore procedure is 8 months out of date. MFA for backup access is tied to the same person's device.
**Recommendation:** Cross-train 2 additional engineers on database restore procedures within 30 days. Implement backup access MFA with shared recovery codes stored in a secure, accessible location.

### Finding 2: Incomplete Crisis Communication Plan

**Severity:** High
**Description:** No pre-prepared customer notification templates, no press statement templates, no clear communication tree for notifying the board and CEO before they learn via external sources.
**Recommendation:** Develop crisis communication templates (customer notification, press statement, social media) within 30 days. Establish communication tree with backup contacts for all executive roles.

### Finding 3: SIEM Detection Gap

**Severity:** High
**Description:** The SIEM did not detect the data exfiltration phase of the attack. The attacker exfiltrated 200GB of data before triggering ransomware, and this was only discovered during forensic analysis.
**Recommendation:** Develop and deploy exfiltration detection rules in SIEM: large outbound data transfers, unusual S3 GetObject patterns, database export operations by non-DBA accounts.

### Finding 4: RTO Target Unrealistic

**Severity:** High
**Description:** Current RTO target of 4 hours for T1 systems is not achievable. The tabletop exercise demonstrated a realistic RTO of 12–18 hours given current runbook completeness, cross-training levels, and DR infrastructure gaps.
**Recommendation:** Update RTO targets to reflect current capabilities (propose 8 hours for T1). Develop a roadmap to achieve the original 4-hour target once DR infrastructure is deployed and runbooks are tested.

### Finding 5: No Cross-Region DR

**Severity:** Critical
**Description:** All production systems are in a single AWS region (us-east-1). A region-level outage would require a complete rebuild in a new region — well beyond the 4-hour RTO.
**Recommendation:** Deploy DR infrastructure in us-west-2 via Terraform within 60 days. Test cross-region failover within 90 days.

---

## Action Items

| ID | Action | Owner | Severity | Due Date |
|----|--------|-------|----------|----------|
| TTX-01 | Cross-train 2 engineers on database restore procedures | VP Eng | Critical | 30 days |
| TTX-02 | Create shared backup MFA recovery codes stored in safe location | CTO | Critical | 7 days |
| TTX-03 | Develop crisis communication templates (customer, press, board) | CISO + Legal | High | 30 days |
| TTX-04 | Deploy SIEM exfiltration detection rules | Security Team | High | 30 days |
| TTX-05 | Update RTO targets and develop remediation roadmap | CISO | High | 15 days |
| TTX-06 | Deploy DR infrastructure in us-west-2 (Terraform) | CTO | Critical | 60 days |
| TTX-07 | Update all DR runbooks with lessons learned | Security Team | High | 30 days |
| TTX-08 | Create backup admin restore runbook (step-by-step, current) | DevOps | Critical | 14 days |
| TTX-09 | Schedule next tabletop exercise (scenario: cloud provider failure) | CISO | Medium | 180 days |
| TTX-10 | Implement automated on-call escalation for SIEM alerts | DevOps | Medium | 45 days |

---

## Participant Feedback

| Aspect | Score (1–5) | Comments |
|--------|-------------|----------|
| Scenario realism | 5 | "This felt very real — the Friday 2AM timing was brutal but realistic" |
| Exercise organization | 4 | "Well-structured injects, good pacing" |
| Learning value | 5 | "We found gaps I didn't know existed" |
| Time pressure | 4 | "Good pressure but some sections felt rushed" |
| Psychological safety | 3 | "A few participants were visibly uncomfortable — need to emphasize it's a learning exercise" |
| Overall value | 5 | "Every security team should do this quarterly" |

---

## Next Steps

1. **Action item tracking:** All TTX items added to risk register with owners and deadlines
2. **Re-test:** Conduct focused restore procedure walkthrough within 30 days (after cross-training complete)
3. **Follow-up exercise:** Cloud provider failure scenario — scheduled for Q3 2026
4. **Board report:** This after-action report will be summarized in the next quarterly board security report
5. **Runbook update:** All runbooks updated within 30 days incorporating TTX findings
