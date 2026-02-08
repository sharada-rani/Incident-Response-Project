# Lessons Learned Report

**Incident ID:** INC-2026-0208-001  
**Incident Type:** Phishing / Credential Compromise  
**Date of Incident:** February 8, 2026  
**Report Date:** February 10, 2026  
**Report Author:** Incident Response Lead  
**Status:** Closed

---

## Executive Summary

On February 8, 2026, a targeted spearphishing attack resulted in the compromise of employee credentials and subsequent unauthorized access to an administrative account. The attack was detected through a combination of user reporting and automated security alerts. The incident was contained within 45 minutes and fully remediated within 2 hours. This report documents the root cause analysis, identifies control gaps, and recommends improvements.

### Key Metrics

| Metric | Value | Target | Status |
|--------|-------|--------|--------|
| Time to Detect | 15 minutes | < 30 min | ✅ Met |
| Time to Contain | 30 minutes | < 1 hour | ✅ Met |
| Time to Eradicate | 1.5 hours | < 4 hours | ✅ Met |
| Total Incident Duration | 2 hours | < 4 hours | ✅ Met |
| Data Exfiltration | None confirmed | None | ✅ Met |
| Regulatory Notification | Not required | N/A | ✅ Met |

---

## Incident Summary

### Timeline

| Time | Event | Phase |
|------|-------|-------|
| 09:10 AM | Phishing email delivered to employee | Attack |
| 09:12 AM | Employee opens attachment, enters credentials | Attack |
| 09:15 AM | Employee reports suspicious email to Help Desk | **Detection** |
| 09:15 AM | Attacker uses stolen credentials from Ukraine IP | Attack |
| 09:20 AM | SIEM generates impossible travel alert | **Detection** |
| 09:20 AM | SOC validates incident, notifies IR Lead | Identification |
| 09:25 AM | User account disabled, sessions revoked | **Containment** |
| 09:28 AM | Attacker accesses admin account via stored password | Attack |
| 09:30 AM | Admin account compromise detected | Detection |
| 09:35 AM | Admin account disabled, ERP isolated | **Containment** |
| 09:45 AM | Database query anomaly detected | Detection |
| 10:00 AM | Incident declared Severity 1, CISO notified | Escalation |
| 10:30 AM | Malicious IPs blocked, phishing domain blocked | Containment |
| 11:00 AM | All compromised credentials reset | **Eradication** |
| 11:15 AM | Systems validated, monitoring enhanced | **Recovery** |
| 11:30 AM | Incident contained, recovery phase begins | Recovery |

### Attack Chain (MITRE ATT&CK)

```
T1566.001           T1078              T1078              T1005
Spearphishing  →  Valid Accounts  →  Privilege        →  Data from
Attachment        (User Creds)       Escalation          Local System
                                     (Admin Creds)       (Attempted)
```

### Impact Assessment

| Category | Impact | Details |
|----------|--------|---------|
| Data Exposure | Low | Query access to 15,000 records; no exfiltration confirmed |
| Financial | Minimal | No fraud losses; IR costs estimated at $5,000 |
| Operational | Low | 30-minute ERP downtime during isolation |
| Reputational | None | No public disclosure required |
| Regulatory | None | No breach notification triggered |

---

## Root Cause Analysis

### Primary Root Cause

**Employee clicked on a phishing link and entered credentials into a fake login page.**

The phishing email was well-crafted, appearing to come from the CFO and containing an urgent request. The employee, under perceived time pressure, failed to verify the sender's email domain before acting.

### Contributing Factors

| Factor | Description | Category |
|--------|-------------|----------|
| **Lookalike Domain** | Attacker registered acme-financial.net (vs. legitimate .com) | External Threat |
| **MFA Gap** | Legacy ERP admin account did not have MFA enabled | Technical Control |
| **Credential Storage** | Admin password stored in plaintext SharePoint file | Process Failure |
| **Training Gap** | Last phishing simulation was 6+ months ago | Awareness |
| **Urgency Pressure** | Email leveraged authority and urgency to bypass critical thinking | Social Engineering |

### Root Cause Diagram (5 Whys)

```
WHY did the attacker access customer data?
    └─ Because they obtained admin credentials

WHY did they obtain admin credentials?
    └─ Because credentials were stored in a SharePoint file

WHY were credentials stored in SharePoint?
    └─ Because there was no password management policy for service accounts

WHY was there no password management policy?
    └─ Because legacy accounts were not included in IAM modernization

WHY were legacy accounts excluded?
    └─ Because MFA migration was deprioritized due to resource constraints
```

---

## What Went Well

### Effective Controls

| Area | Observation |
|------|-------------|
| **User Reporting** | Employee self-reported quickly (within 3 minutes of compromise) |
| **SIEM Detection** | Impossible travel rule triggered within 5 minutes |
| **Rapid Response** | SOC validated and escalated within 5 minutes |
| **Containment Speed** | User account disabled within 10 minutes of validation |
| **Team Coordination** | IRT worked effectively with clear communication |
| **Documentation** | Evidence was properly preserved from the start |

### Team Performance

- SOC Analyst correctly prioritized the alert and escalated immediately
- IT Admin executed containment actions within SLA
- IR Lead coordinated effectively across teams
- Legal provided timely guidance on regulatory requirements

---

## Control Gaps Identified

### Critical Gaps

| Gap ID | Description | Risk Level | MITRE Mitigation |
|--------|-------------|------------|------------------|
| **GAP-001** | MFA not enforced on legacy admin accounts | High | M1032 - Multi-factor Authentication |
| **GAP-002** | Credentials stored in plaintext in file shares | High | M1027 - Password Policies |
| **GAP-003** | Lookalike domain not detected by email security | Medium | M1049 - Antivirus/Antimalware |

### Process Gaps

| Gap ID | Description | Risk Level |
|--------|-------------|------------|
| **GAP-004** | Phishing simulations not conducted quarterly | Medium |
| **GAP-005** | No automated alerts for privileged account creation/access | Medium |
| **GAP-006** | Service account inventory incomplete | Low |

### Detection Gaps

| Gap ID | Description | Risk Level |
|--------|-------------|------------|
| **GAP-007** | Email security did not flag lookalike domain | Medium |
| **GAP-008** | No real-time alert for database bulk queries | Medium |

---

## Recommendations

### Immediate Actions (0-30 Days)

| ID | Recommendation | Owner | Priority | Target Date |
|----|----------------|-------|----------|-------------|
| REC-001 | Enable MFA on ALL admin/privileged accounts | IT Admin | Critical | Feb 15, 2026 |
| REC-002 | Audit and remove all stored plaintext credentials | IT Admin | Critical | Feb 20, 2026 |
| REC-003 | Implement privileged access management (PAM) solution | IT Director | High | Mar 1, 2026 |
| REC-004 | Deploy email lookalike domain detection | SOC Manager | High | Feb 28, 2026 |

### Short-Term Actions (30-90 Days)

| ID | Recommendation | Owner | Priority | Target Date |
|----|----------------|-------|----------|-------------|
| REC-005 | Conduct phishing simulation for all employees | Security Awareness | Medium | Mar 15, 2026 |
| REC-006 | Implement database activity monitoring alerts | DBA | Medium | Mar 30, 2026 |
| REC-007 | Complete service account inventory and risk assessment | IT Admin | Medium | Apr 1, 2026 |
| REC-008 | Update IR playbooks with lessons from this incident | IR Lead | Medium | Mar 15, 2026 |

### Long-Term Actions (90+ Days)

| ID | Recommendation | Owner | Priority | Target Date |
|----|----------------|-------|----------|-------------|
| REC-009 | Implement Zero Trust architecture for privileged access | CISO | High | Q3 2026 |
| REC-010 | Deploy UEBA for anomaly detection | SOC Manager | Medium | Q2 2026 |
| REC-011 | Establish quarterly phishing simulation program | Security Awareness | Medium | Ongoing |
| REC-012 | Implement SOAR for automated containment actions | SOC Manager | Low | Q4 2026 |

---

## Metrics & KPIs

### Response Time Analysis

```
Detection    ████████████████░░░░░░░░░░░░░░ 15 min (Target: 30 min) ✅
Containment  ████████████████████████████░░ 30 min (Target: 60 min) ✅
Eradication  ████████████████████████████░░ 90 min (Target: 240 min) ✅
Recovery     ████████████░░░░░░░░░░░░░░░░░░ 30 min (Target: 120 min) ✅
```

### Detection Source Distribution

| Source | Count | Percentage |
|--------|-------|------------|
| User Report | 1 | 33% |
| SIEM Alert | 2 | 67% |
| EDR Alert | 0 | 0% |

### Incident Severity Trend (Last 12 Months)

| Severity | Q1 | Q2 | Q3 | Q4 | YTD |
|----------|----|----|----|----|-----|
| Critical | 0 | 0 | 1 | 1 | 2 |
| High | 2 | 1 | 2 | 3 | 8 |
| Medium | 5 | 4 | 6 | 5 | 20 |
| Low | 12 | 15 | 11 | 14 | 52 |

---

## Post-Incident Review Meeting

**Date:** February 10, 2026  
**Attendees:** IR Lead, SOC Manager, IT Director, Legal Counsel, CISO

### Discussion Summary

1. **Detection Effectiveness:** The combination of user reporting and automated detection worked well. Training investment is paying off.

2. **MFA Gap:** The lack of MFA on the legacy admin account was the critical failure. This must be remediated immediately.

3. **Credential Storage:** The discovery of plaintext credentials in SharePoint highlights a broader governance issue. A comprehensive audit is required.

4. **Communication:** Internal communication was effective. Escalation thresholds were appropriate.

5. **Documentation:** Evidence collection and chain of custody were properly maintained.

### Action Item Tracking

| Action | Owner | Due Date | Status |
|--------|-------|----------|--------|
| Enable MFA on all privileged accounts | IT Admin | Feb 15, 2026 | In Progress |
| Remove plaintext credentials from SharePoint | IT Admin | Feb 20, 2026 | Not Started |
| Update IR playbook for phishing scenarios | IR Lead | Mar 15, 2026 | Not Started |
| Conduct full service account audit | IT Director | Apr 1, 2026 | Not Started |

---

## Appendix: Evidence Summary

### Evidence Collected

| Evidence ID | Type | Description | Hash (SHA-256) |
|-------------|------|-------------|----------------|
| EV-001 | Email | Original phishing email with headers | [Hash Value] |
| EV-002 | Logs | Authentication logs (09:00-12:00) | [Hash Value] |
| EV-003 | Logs | SIEM correlation events | [Hash Value] |
| EV-004 | Image | Memory dump - affected workstation | [Hash Value] |
| EV-005 | Logs | ERP database query logs | [Hash Value] |
| EV-006 | Screenshot | Fake login page screenshot | [Hash Value] |

### Chain of Custody

All evidence maintained per IR Evidence Handling Procedures. Full chain of custody documentation available in incident ticket INC-2026-0208-001.

---

## Document Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| IR Lead | [Name] | | Feb 10, 2026 |
| SOC Manager | [Name] | | Feb 10, 2026 |
| CISO | [Name] | | Feb 10, 2026 |

---

*This Lessons Learned Report is classified as Internal Use Only and should not be distributed outside the organization without CISO approval.*
