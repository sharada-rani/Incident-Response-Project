# Tabletop Exercise: Phishing Incident Scenario

**Exercise Type:** Discussion-Based Tabletop  
**Duration:** 90 minutes  
**Framework Alignment:** NIST SP 800-61, MITRE ATT&CK  
**Classification:** Training Exercise

---

## Table of Contents

1. [Exercise Overview](#1-exercise-overview)
2. [MITRE ATT&CK Mapping](#2-mitre-attck-mapping)
3. [Scenario Background](#3-scenario-background)
4. [Timeline with Injects](#4-timeline-with-injects)
5. [Discussion Questions & Answers](#5-discussion-questions--answers)
6. [Evidence Artifacts](#6-evidence-artifacts)
7. [Exercise Evaluation](#7-exercise-evaluation)

---

## Pre-Exercise Facilitator Checklist

- [ ] Distribute scenario overview to participants 24 hours in advance
- [ ] Reserve conference room with whiteboard/screen sharing
- [ ] Prepare timer for tracking response times
- [ ] Print copies of IR Plan for reference
- [ ] Set up shared document for capturing action items
- [ ] Invite all required stakeholders
- [ ] Prepare coffee/refreshments (optional but recommended!)

---

## 1. Exercise Overview

### 1.1 Purpose

This tabletop exercise simulates a phishing attack that results in credential compromise and unauthorized access. Participants will walk through the incident response process to validate procedures, identify gaps, and improve readiness.

### 1.2 Objectives

| Objective | Description |
|-----------|-------------|
| **Validate IRP** | Test incident response procedures against realistic scenario |
| **Clarify Roles** | Ensure team members understand their responsibilities |
| **Identify Gaps** | Discover weaknesses in current processes |
| **Practice Communication** | Exercise escalation and notification procedures |
| **Build Muscle Memory** | Familiarize team with response workflows |

### 1.3 Participants

| Role | Responsibility in Exercise |
|------|---------------------------|
| Exercise Facilitator | Presents injects, guides discussion |
| SOC Analyst | Responds to detection scenarios |
| Incident Response Lead | Coordinates simulated response |
| IT Administrator | Addresses technical containment questions |
| Legal/Compliance | Provides regulatory perspective |
| Management Representative | Makes simulated business decisions |

### 1.4 Ground Rules

- This is a **no-fault** learning exercise
- All responses are hypothetical—no actual systems will be affected
- Focus on **what we would do**, not assigning blame
- Document action items for post-exercise improvement
- Classified information should not be discussed

---

## 2. MITRE ATT&CK Mapping

This scenario involves the following MITRE ATT&CK techniques:

### Primary Techniques

| Technique ID | Technique Name | Tactic | Description |
|--------------|----------------|--------|-------------|
| **T1566.001** | Phishing: Spearphishing Attachment | Initial Access | Adversary sends targeted email with malicious attachment |
| **T1078** | Valid Accounts | Defense Evasion, Persistence, Initial Access | Adversary uses compromised legitimate credentials |

### Potential Escalation Techniques

| Technique ID | Technique Name | Tactic | Description |
|--------------|----------------|--------|-------------|
| **T1110** | Brute Force | Credential Access | Adversary attempts to access other accounts using known passwords |
| **T1071.001** | Application Layer Protocol: Web | Command and Control | Adversary uses HTTPS for C2 communication |
| **T1005** | Data from Local System | Collection | Adversary collects data from compromised systems |

### Attack Chain Visualization

```
┌──────────────────────────────────────────────────────────────────────┐
│                        ATTACK CHAIN                                   │
├──────────────────────────────────────────────────────────────────────┤
│                                                                       │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐              │
│  │  T1566.001  │───▶│   T1078     │───▶│   T1110     │              │
│  │ Spearphish  │    │   Valid     │    │   Brute     │              │
│  │ Attachment  │    │  Accounts   │    │   Force     │              │
│  └─────────────┘    └─────────────┘    └─────────────┘              │
│        │                  │                  │                       │
│        ▼                  ▼                  ▼                       │
│   Initial Access    Lateral Movement    Privilege Escalation        │
│                                                                       │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 3. Scenario Background

### 3.1 Organization Context

**Company:** Acme Financial Services (fictional)  
**Industry:** Financial Services  
**Employees:** 500  
**Regulatory Requirements:** SOX, GLBA, state data breach notification laws

**Current Security Posture:**
- SIEM deployed with 24/7 SOC monitoring
- Endpoint Detection & Response (EDR) on all workstations
- Email security gateway with attachment sandboxing
- MFA enabled for VPN and cloud applications
- MFA **NOT** enabled for some legacy administrative accounts
- Annual security awareness training completed (last: 6 months ago)

### 3.2 Threat Actor Profile

| Attribute | Description |
|-----------|-------------|
| **Actor Type** | Financially motivated cybercriminal group |
| **Sophistication** | Moderate |
| **Objective** | Financial data theft, potential ransomware deployment |
| **Known TTPs** | Spearphishing, credential harvesting, lateral movement |

### 3.3 Pre-Incident Conditions

- Today is a normal Tuesday business day
- Q4 financial reports are being finalized
- The CFO is traveling and accessing systems remotely
- IT is in the middle of a scheduled system upgrade (reduced capacity)

---

## 4. Timeline with Injects

### Inject 1: 09:15 AM — Initial Report

**SITUATION:**

> Sarah Chen, an Accounts Payable Specialist, calls the IT Help Desk. She reports receiving an email that seemed unusual. The email appeared to be from the CFO requesting an urgent review of an attached invoice. Sarah clicked on the attachment, and a login page appeared asking for her credentials. She entered her username and password before realizing something was wrong.

**INJECT DETAILS:**

| Attribute | Value |
|-----------|-------|
| Reported By | Sarah Chen, Accounts Payable |
| Email Subject | "URGENT: Q4 Invoice Review Required" |
| Sender Display | "David Morrison, CFO" |
| Sender Email | david.morrison@acme-financial.net (note: actual domain is acme-financial.com) |
| Attachment | Q4_Invoice_Review.pdf (actually an HTML file) |
| User Action | Opened attachment, entered credentials in fake login page |

**FACILITATOR NOTE:** *Pause for team discussion before proceeding.*

---

### Inject 2: 09:20 AM — SOC Alert

**SITUATION:**

> Five minutes after Sarah's help desk call, the SOC receives an automated alert from the SIEM. The alert shows a successful authentication for Sarah Chen's account from an IP address geolocated to Eastern Europe, occurring 3 minutes after a successful login from her normal workstation.

**ALERT DETAILS:**

| Field | Value |
|-------|-------|
| Alert Type | Impossible Travel Detection |
| User Account | schen@acme-financial.com |
| Source IP #1 | 10.50.25.112 (Corporate Network, Sarah's workstation) |
| Source IP #2 | 185.174.xxx.xxx (Ukraine) |
| Time Difference | 3 minutes |
| Systems Accessed | Email (O365), SharePoint |

**NEW INFORMATION:**

The SOC Analyst queries authentication logs and finds:
- 4 failed login attempts for Sarah's account in the past 12 hours (before the successful compromise)
- Successful password reset 2 months ago (legitimate)
- No previous foreign IP logins for this account

**FACILITATOR NOTE:** *What actions should be taken immediately?*

---

### Inject 3: 09:30 AM — Privilege Escalation Detected

**SITUATION:**

> The attacker, using Sarah's credentials, has accessed the Finance SharePoint site. They discover a file named "IT_Admin_Accounts.xlsx" containing a list of service accounts and, alarmingly, one entry with a plaintext password for a legacy IT admin account used for the ERP system.

**ALERT DETAILS:**

| Field | Value |
|-------|-------|
| Alert Type | Privileged Account Login from Unusual Source |
| Account | erp_admin (Local IT Admin Account) |
| Source IP | 185.174.xxx.xxx (Same Ukraine IP) |
| System Accessed | ERP System (On-premises) |
| MFA Status | Not enabled on this legacy account |

**NEW INFORMATION:**

- The erp_admin account has access to customer financial records
- This account was scheduled for MFA migration next quarter
- The account has not been used legitimately in 30 days

**FACILITATOR NOTE:** *This is now a more serious incident. Reassess severity.*

---

### Inject 4: 09:45 AM — Potential Data Access

**SITUATION:**

> The SOC detects unusual database queries running against the customer database from the ERP system. Query patterns suggest systematic extraction of customer records including names, addresses, and account numbers.

**ALERT DETAILS:**

| Field | Value |
|-------|-------|
| Alert Type | Anomalous Database Query Pattern |
| Source | ERP Application Server |
| Query Type | SELECT * FROM customers WHERE... (iterating through records) |
| Records Touched | ~15,000 customer records queried in 10 minutes |
| Data Fields | Name, Address, SSN (encrypted), Account Number |

**NEW INFORMATION:**

- No data exfiltration detected YET (queries are internal)
- Attacker may be staging data for extraction
- Outbound connection attempts observed to unknown external IP

**FACILITATOR NOTE:** *Containment is now critical. What's the priority order?*

---

### Inject 5: 10:00 AM — Incident Escalation

**SITUATION:**

> The Incident Response Lead declares this a Severity 1 (Critical) incident and initiates full incident response procedures. The following stakeholders need to be notified immediately.

**ESCALATION REQUIRED TO:**

- CISO (mandatory for Severity 1)
- Legal Counsel (potential data breach)
- CFO (executive notification + his identity was spoofed)
- HR (employee credential compromise)
- External IR Retainer (forensic support)

**ADDITIONAL PRESSURE:**

- A board meeting is scheduled for 2:00 PM today
- The CFO's executive assistant is asking why his calendar is showing meetings he didn't schedule
- A wire transfer request has been submitted (requires verification)

**FACILITATOR NOTE:** *Exercise enters full response mode. Focus on coordination and decision-making.*

---

## 5. Discussion Questions & Answers

### Q1: How is the incident identified?

**Answer:**

The incident is identified through **two channels**:

1. **User Report (Primary):** Sarah Chen self-reported to the Help Desk after realizing she may have entered credentials into a suspicious page. This represents effective security awareness.

2. **Automated Detection (Secondary):** The SIEM generated an impossible travel alert when Sarah's credentials were used from Ukraine within minutes of her legitimate login.

**Key Point:** Both detection methods worked in this scenario. User reporting provided context (the phishing email), while automated detection provided confirmation and timeline.

---

### Q2: Who declares this a security incident?

**Answer:**

**The Incident Response Lead** formally declares this a security incident.

**Declaration Timeline:**
| Time | Event | Declared By |
|------|-------|-------------|
| 09:15 | Help desk receives report | Potential incident (Help Desk) |
| 09:20 | SIEM alert correlates with report | Confirmed incident (SOC Analyst) |
| 09:20 | IR Lead notified, validates | Severity 2 initially (IR Lead) |
| 09:30 | Privilege escalation detected | Elevated to Severity 1 (IR Lead) |

**Authority Chain:**
- SOC Analyst can identify and classify initial incidents
- IR Lead has authority to declare and escalate severity
- CISO must be notified for Severity 1/2 incidents

---

### Q3: What is the severity level?

**Answer:**

**Final Severity: Level 1 (Critical)**

**Severity Evolution:**
| Time | Severity | Justification |
|------|----------|---------------|
| 09:15 | Level 3 (Medium) | Single user credential potentially compromised |
| 09:20 | Level 2 (High) | Confirmed credential use from malicious IP |
| 09:30 | Level 1 (Critical) | Privileged account compromised, data access |

**Critical Severity Triggers Met:**
- ✅ Privileged account compromise
- ✅ Potential access to regulated customer data
- ✅ Active threat actor in environment
- ✅ Regulatory notification likely required

---

### Q4: What systems/accounts are contained?

**Answer:**

**Immediate Containment Actions:**

| Asset | Action | Priority | Owner |
|-------|--------|----------|-------|
| schen@acme-financial.com | Disable account, revoke all sessions | Immediate | IT Admin |
| erp_admin account | Disable account, change password | Immediate | IT Admin |
| ERP Application Server | Network isolation | Immediate | IT Admin |
| Sarah's workstation | Disconnect from network | Immediate | IT Admin |
| Malicious IP (185.174.xxx.xxx) | Block at firewall | Immediate | SOC |
| Phishing domain (acme-financial.net) | Block at proxy/DNS | Immediate | SOC |

**Broader Containment:**
- All Finance department accounts: Force password reset
- VPN access: Temporarily require re-authentication
- ERP access: Suspend all remote access pending investigation

---

### Q5: Who must be notified (legal, management)?

**Answer:**

**Internal Notifications:**

| Stakeholder | Why | When | How |
|-------------|-----|------|-----|
| CISO | Severity 1 requirement | Within 15 min | Phone call |
| Legal Counsel | Potential data breach, regulatory | Within 30 min | Phone + email |
| CFO | Identity spoofed, exec awareness | Within 1 hour | Phone call |
| CEO | Severity 1 business impact | Within 2 hours | CISO briefing |
| HR | Employee involvement | Within 4 hours | Email |
| Board | Potential material impact | Before 2 PM meeting | CISO briefing |

**External Notifications (if breach confirmed):**

| Stakeholder | Requirement | Timeline |
|-------------|-------------|----------|
| State Regulators | State breach notification laws | Varies (24-72 hours) |
| Affected Customers | Breach notification | Per regulatory requirement |
| Law Enforcement | If criminal investigation warranted | As determined by Legal |
| Cyber Insurance | Claim notification | Within 24 hours |

---

### Q6: Is regulatory notification required?

**Answer:**

**Potentially yes — depends on investigation findings.**

**Analysis:**

| Factor | Status | Implication |
|--------|--------|-------------|
| Data Type | Customer PII (names, SSN, accounts) | High sensitivity |
| Data Access | Confirmed queries on 15,000 records | Breach likely |
| Data Exfiltration | Not confirmed yet | Under investigation |
| Encryption Status | SSN encrypted at rest | May reduce scope |

**Applicable Regulations:**

| Regulation | Trigger | Timeline |
|------------|---------|----------|
| State Laws (varies) | Unauthorized access to PII | 24-72 hours |
| GLBA Safeguards | Financial data breach | "As soon as possible" |
| SOX | Material impact on financials | Disclosure consideration |

**Recommendation:** Engage Legal immediately. Assume notification will be required and begin preparing documentation while investigation continues.

---

### Q7: How is evidence preserved?

**Answer:**

**Evidence Preservation Protocol:**

| Evidence Type | Collection Method | Owner | Storage |
|---------------|-------------------|-------|---------|
| Email (phishing) | Export original with full headers | SOC | Evidence locker |
| Sarah's workstation | Forensic disk image | IR Team | Offline storage |
| SIEM logs | Export with hash verification | SOC | Evidence locker |
| Authentication logs | Export from Azure AD / IdP | IT Admin | Evidence locker |
| ERP database logs | Query logs, access logs | DBA | Evidence locker |
| Network captures | PCAP from time of incident | SOC | Evidence locker |
| Memory dump | Volatile capture from workstation | IR Team | Evidence locker |

**Chain of Custody Requirements:**
- Document who collected each item, when, and how
- Calculate and record hash values (SHA-256)
- Store in secure, access-controlled location
- Maintain access log for all evidence interactions
- Preserve original; work from copies

**Legal Hold:**
- Issue legal hold notice to IT
- Suspend normal log rotation for affected systems
- Preserve all backups from incident timeframe

---

## 6. Evidence Artifacts

### 6.1 Phishing Email Headers (Simulated)

```
Return-Path: <bounce@mail.acme-financial.net>
Received: from mail.acme-financial.net (185.174.xxx.xxx)
        by mx.acme-financial.com with SMTP
        id abc123def456; Tue, 08 Feb 2026 09:10:15 -0500
From: "David Morrison, CFO" <david.morrison@acme-financial.net>
To: schen@acme-financial.com
Subject: URGENT: Q4 Invoice Review Required
Date: Tue, 08 Feb 2026 09:10:00 -0500
X-Mailer: Microsoft Outlook 16.0
Content-Type: multipart/mixed; boundary="----=_NextPart_001"

------=_NextPart_001
Content-Type: text/html; charset="UTF-8"

<html>
<body>
<p>Sarah,</p>
<p>Please review the attached Q4 invoice immediately. 
   I need your approval before the board meeting today.</p>
<p>Thanks,<br>David Morrison<br>Chief Financial Officer</p>
</body>
</html>
------=_NextPart_001
Content-Type: application/octet-stream; name="Q4_Invoice_Review.pdf"
Content-Disposition: attachment; filename="Q4_Invoice_Review.pdf"

[Malicious HTML file masquerading as PDF]
```

### 6.2 Authentication Log Entries (Simulated)

```
2026-02-08T09:12:33.000Z INFO  AUTH schen@acme-financial.com SUCCESS 
    IP=10.50.25.112 UA="Mozilla/5.0 Windows" Location=HQ-Floor3

2026-02-08T09:15:18.000Z INFO  AUTH schen@acme-financial.com SUCCESS 
    IP=185.174.xxx.xxx UA="Mozilla/5.0 Windows" Location=Ukraine

2026-02-08T09:28:44.000Z INFO  AUTH erp_admin SUCCESS 
    IP=185.174.xxx.xxx UA="curl/7.64.1" Location=Ukraine

2026-02-08T09:30:02.000Z WARN  DB_QUERY erp_admin BULK_SELECT 
    Table=customers Rows=15342 Duration=847ms
```

### 6.3 IOC Summary

| Type | Value | Context |
|------|-------|---------|
| IP Address | 185.174.xxx.xxx | Attacker source |
| Domain | acme-financial.net | Phishing domain |
| Email | david.morrison@acme-financial.net | Spoofed sender |
| File Hash | [SHA256 of attachment] | Malicious file |
| User Agent | curl/7.64.1 | Automated access |

---

## 7. Exercise Evaluation

### 7.1 Performance Metrics

| Metric | Target | Actual (Fill post-exercise) |
|--------|--------|----------------------------|
| Time to initial response | < 15 min | |
| Time to containment decision | < 30 min | |
| Time to executive notification | < 1 hour | |
| All stakeholders notified | 100% | |
| Evidence preservation initiated | < 1 hour | |

### 7.2 Debrief Questions

**What went well?**
- [ ] Document positive observations

**What needs improvement?**
- [ ] Document gaps and challenges

**Action Items:**

| Item | Owner | Due Date | Status |
|------|-------|----------|--------|
| | | | |
| | | | |
| | | | |

### 7.3 Key Takeaways

1. **User reporting is critical** — Sarah's quick report enabled faster response
2. **MFA gaps are exploitable** — Legacy admin account lacked protection
3. **Privileged access must be monitored** — Unusual admin account usage was detected
4. **Credential hygiene matters** — Password stored in SharePoint enabled escalation
5. **Communication is essential** — Clear escalation paths prevent confusion

---

## Appendix: Exercise Facilitator Notes

**Before Exercise:**
- Distribute scenario overview (Section 3 only) 24 hours in advance
- Ensure all participants have access to IRP for reference
- Prepare whiteboard/shared doc for capturing discussion points

**During Exercise:**
- Allow 10-15 minutes per inject for discussion
- Encourage participation from all roles
- Challenge assumptions and probe for detail
- Keep time to ensure all injects are covered

**After Exercise:**
- Collect evaluation forms
- Schedule follow-up meeting within 1 week
- Assign action items with owners and due dates
- Update IRP based on identified gaps

---

*Exercise Developed: February 2026*  
*Framework Alignment: NIST SP 800-61r2, MITRE ATT&CK v12*
