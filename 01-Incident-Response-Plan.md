# Incident Response Plan (IRP)

**Version:** 1.0  
**Effective Date:** February 2026  
**Framework Alignment:** NIST SP 800-61r2  
**Classification:** Internal Use Only

---

## Quick Reference Card

| Phase | Key Actions | Time Target |
|-------|-------------|-------------|
| **Detection** | Validate alert, gather IOCs | Immediate |
| **Containment** | Disable accounts, isolate systems | < 30 min |
| **Eradication** | Remove malware, reset credentials | < 4 hours |
| **Recovery** | Restore from backup, validate function | < 24 hours |
| **Lessons Learned** | Root cause analysis, update procedures | < 2 weeks |

**Emergency Contacts:** See Section 3.3

---

## Table of Contents

1. [Purpose & Scope](#1-purpose--scope)
2. [Incident Classification & Severity Levels](#2-incident-classification--severity-levels)
3. [Roles & Responsibilities](#3-roles--responsibilities)
4. [Incident Response Phases](#4-incident-response-phases)
5. [Communication Plan](#5-communication-plan)
6. [Escalation Criteria](#6-escalation-criteria)
7. [Documentation & Evidence Handling](#7-documentation--evidence-handling)

---

## 1. Purpose & Scope

### 1.1 Purpose

This Incident Response Plan (IRP) establishes a structured approach to detecting, responding to, and recovering from security incidents. The goal is to minimize business impact, protect organizational assets, ensure regulatory compliance, and improve security posture through lessons learned.

### 1.2 Scope

This plan applies to:
- All information systems and network infrastructure
- All employees, contractors, and third-party vendors
- All data classifications (public, internal, confidential, restricted)
- Physical and logical security incidents

### 1.3 Objectives

| Objective | Description |
|-----------|-------------|
| **Minimize Impact** | Reduce damage to systems, data, and business operations |
| **Rapid Response** | Ensure timely detection and containment of threats |
| **Preserve Evidence** | Maintain forensic integrity for potential legal proceedings |
| **Regulatory Compliance** | Meet notification requirements (GDPR, HIPAA, PCI-DSS) |
| **Continuous Improvement** | Learn from incidents to strengthen defenses |

---

## 2. Incident Classification & Severity Levels

### 2.1 Incident Types

| Category | Examples |
|----------|----------|
| **Malware** | Ransomware, trojans, viruses, worms |
| **Phishing** | Spearphishing, credential harvesting, BEC |
| **Unauthorized Access** | Compromised accounts, privilege escalation |
| **Data Breach** | Exfiltration, accidental exposure |
| **Denial of Service** | DDoS attacks, resource exhaustion |
| **Insider Threat** | Malicious or negligent employee actions |

### 2.2 Severity Levels

| Level | Classification | Description | Response Time | Examples |
|-------|---------------|-------------|---------------|----------|
| **1** | Critical | Immediate threat to business operations, widespread impact | 15 minutes | Active ransomware, large-scale data breach |
| **2** | High | Significant impact, contained to department/system | 1 hour | Compromised admin account, targeted phishing success |
| **3** | Medium | Moderate impact, limited scope | 4 hours | Single user credential compromise, malware on workstation |
| **4** | Low | Minimal impact, no data exposure | 24 hours | Failed login attempts, suspicious but blocked email |

### 2.3 Severity Determination Criteria

- **Data Sensitivity:** Type and volume of data potentially affected
- **System Criticality:** Business importance of affected systems
- **Spread Potential:** Likelihood of lateral movement or escalation
- **Regulatory Impact:** Notification requirements triggered
- **Reputational Risk:** Public visibility and customer impact

---

## 3. Roles & Responsibilities

### 3.1 Incident Response Team (IRT) Structure

```
┌─────────────────────────────────────────────────────────┐
│                  Executive Sponsor                       │
│              (CISO / Security Director)                  │
└─────────────────────────┬───────────────────────────────┘
                          │
┌─────────────────────────┴───────────────────────────────┐
│                Incident Response Lead                    │
│           (Incident Commander / IR Manager)              │
└────┬──────────────┬──────────────┬──────────────┬───────┘
     │              │              │              │
┌────┴────┐   ┌────┴────┐   ┌────┴────┐   ┌────┴────┐
│   SOC   │   │   IT    │   │  Legal  │   │  Comms  │
│ Analyst │   │  Admin  │   │Compliance│   │   PR    │
└─────────┘   └─────────┘   └─────────┘   └─────────┘
```

### 3.2 Role Definitions

| Role | Primary Responsibilities |
|------|-------------------------|
| **Executive Sponsor (CISO)** | Strategic decisions, resource allocation, external communications approval |
| **Incident Response Lead** | Coordinates response efforts, declares incident severity, manages timeline |
| **SOC Analyst** | Initial detection, triage, monitoring, log analysis, IOC identification |
| **IT Administrator** | System isolation, account resets, network changes, recovery operations |
| **Legal/Compliance** | Regulatory guidance, evidence preservation, notification requirements |
| **Communications/PR** | Internal messaging, external statements, customer notifications |
| **HR Representative** | Employee-related incidents, insider threat investigations |

### 3.3 Contact Information

| Role | Name | Phone | Email | Backup |
|------|------|-------|-------|--------|
| IR Lead | [Designated] | [Phone] | [Email] | [Backup Name] |
| SOC Manager | [Designated] | [Phone] | [Email] | [Backup Name] |
| IT Director | [Designated] | [Phone] | [Email] | [Backup Name] |
| Legal Counsel | [Designated] | [Phone] | [Email] | [Backup Name] |
| CISO | [Designated] | [Phone] | [Email] | [Backup Name] |

*Note: Maintain current contact list in secure, accessible location. Update quarterly.*

---

## 4. Incident Response Phases

*Aligned with NIST SP 800-61 Revision 2*

### Phase 1: Preparation

**Objective:** Establish capability to respond to incidents before they occur.

#### 1.1 Technical Readiness

| Component | Status | Owner |
|-----------|--------|-------|
| SIEM deployed and configured | ☐ | SOC |
| Endpoint Detection & Response (EDR) | ☐ | IT |
| Network monitoring (IDS/IPS) | ☐ | SOC |
| Log aggregation and retention | ☐ | IT |
| Forensic toolkit available | ☐ | IR Lead |
| Backup systems tested | ☐ | IT |

#### 1.2 Administrative Readiness

| Component | Status | Owner |
|-----------|--------|-------|
| IR Plan documented and approved | ☐ | IR Lead |
| IR Team identified and trained | ☐ | CISO |
| Contact lists current | ☐ | IR Lead |
| Communication templates ready | ☐ | Comms |
| Third-party contracts in place (forensics, legal) | ☐ | Legal |
| Tabletop exercises conducted | ☐ | IR Lead |

#### 1.3 Security Awareness

- Annual security awareness training for all employees
- Phishing simulation exercises (quarterly)
- Incident reporting procedures communicated
- Security champions program in departments

**Artifacts:**
- IR Policy Document
- Contact List (secure location)
- Escalation Threshold Matrix
- Vendor/Partner Contact List

---

### Phase 2: Identification

**Objective:** Detect potential incidents and determine if a security event is an actual incident.

#### 2.1 Detection Sources

| Source | Type | Examples |
|--------|------|----------|
| **Automated** | SIEM alerts | Correlation rules, anomaly detection |
| **Automated** | EDR alerts | Malware detection, suspicious behavior |
| **User-Reported** | Help desk tickets | Suspicious email, unusual system behavior |
| **External** | Third-party notification | Vendor alerts, threat intelligence, law enforcement |

#### 2.2 Initial Triage Process

```
┌─────────────────────────────────────────────────────────┐
│               Alert/Report Received                      │
└─────────────────────────┬───────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────┐
│  Initial Assessment (SOC Analyst - 15 min max)          │
│  • Validate alert is not false positive                 │
│  • Gather initial IOCs                                  │
│  • Check for related events                             │
└─────────────────────────┬───────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────┐
│  Incident Declaration Decision                           │
│  • Is this a confirmed security incident?               │
│  • Assign severity level                                │
│  • Create incident ticket                               │
└─────────────────────────┬───────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────┐
│  Escalate per Severity Level                             │
└─────────────────────────────────────────────────────────┘
```

#### 2.3 Indicators of Compromise (IOCs) to Document

- IP addresses (source and destination)
- Domain names and URLs
- File hashes (MD5, SHA-256)
- Email addresses and headers
- User accounts affected
- Timestamps of activity
- Affected systems/hostnames

#### 2.4 Example Triggers

| Trigger | Potential Incident Type |
|---------|------------------------|
| Employee reports suspicious email | Phishing attempt |
| Multiple failed login attempts from single IP | Brute force attack |
| Credential use from unusual geographic location | Account compromise |
| EDR detects malicious file execution | Malware infection |
| Unusual data transfer volumes | Data exfiltration |

---

### Phase 3: Containment

**Objective:** Limit the scope and impact of the incident.

#### 3.1 Short-Term Containment (Immediate)

| Action | Owner | Timeframe |
|--------|-------|-----------|
| Disable compromised user accounts | IT Admin | Immediate |
| Isolate affected endpoints from network | IT Admin | < 15 min |
| Block malicious IPs/domains at firewall | SOC | < 15 min |
| Preserve volatile evidence (memory dumps) | IR Lead | Before isolation |
| Implement temporary access restrictions | IT Admin | < 30 min |

#### 3.2 Long-Term Containment

| Action | Owner | Timeframe |
|--------|-------|-----------|
| Apply network segmentation | IT Admin | < 2 hours |
| Update firewall/proxy rules organization-wide | SOC | < 4 hours |
| Implement additional monitoring on similar systems | SOC | < 4 hours |
| Deploy temporary controls (additional authentication) | IT Admin | < 4 hours |
| Coordinate with ISP/hosting if external infrastructure | IR Lead | As needed |

#### 3.3 Containment Decision Matrix

| Scenario | Recommended Action |
|----------|-------------------|
| Single workstation malware | Isolate endpoint, image for forensics |
| Compromised user credentials | Reset password, revoke sessions, enable MFA |
| Phishing with lateral movement | Isolate affected systems, reset all exposed credentials |
| Ransomware detected | Network isolation, do NOT pay, engage forensics |
| Data exfiltration in progress | Block destination, capture traffic, preserve logs |

---

### Phase 4: Eradication

**Objective:** Remove the threat and all malicious artifacts from the environment.

#### 4.1 Eradication Activities

| Activity | Description | Owner |
|----------|-------------|-------|
| **Malware Removal** | Remove malicious files, clean registry entries | IT Admin |
| **Credential Reset** | Force password reset for all compromised accounts | IT Admin |
| **Patch Vulnerabilities** | Apply security patches that were exploited | IT Admin |
| **Remove Persistence** | Eliminate backdoors, scheduled tasks, services | SOC |
| **Clean Email System** | Purge malicious emails from all mailboxes | IT Admin |
| **Update Signatures** | Add new IOCs to security tools | SOC |

#### 4.2 Verification Checklist

- [ ] All known malicious files removed
- [ ] Compromised accounts reset with new credentials
- [ ] Exploited vulnerabilities patched
- [ ] Persistence mechanisms eliminated
- [ ] No active attacker presence in environment
- [ ] Updated detection rules deployed

---

### Phase 5: Recovery

**Objective:** Restore systems to normal operation while preventing re-infection.

#### 5.1 Recovery Steps

| Step | Action | Verification |
|------|--------|--------------|
| 1 | Restore from clean backups (if needed) | Backup integrity verified |
| 2 | Rebuild systems from known-good images | Checksums match |
| 3 | Re-enable user accounts with new credentials | MFA verified working |
| 4 | Gradually restore network connectivity | Monitor for anomalies |
| 5 | Resume business operations | Application testing complete |

#### 5.2 Post-Recovery Monitoring

| Monitoring Activity | Duration | Owner |
|---------------------|----------|-------|
| Enhanced logging on affected systems | 30 days | SOC |
| Close monitoring for IOC recurrence | 30 days | SOC |
| User behavior analytics review | 14 days | SOC |
| Network traffic baseline comparison | 14 days | SOC |

#### 5.3 Business Validation

- [ ] Critical business applications functional
- [ ] User access restored appropriately
- [ ] Data integrity verified
- [ ] Customer-facing services operational
- [ ] No performance degradation

---

### Phase 6: Lessons Learned

**Objective:** Improve incident response capability and prevent recurrence.

#### 6.1 Post-Incident Review Meeting

**Timing:** Within 1-2 weeks of incident closure

**Attendees:**
- All IRT members involved
- System owners
- Executive sponsor (for significant incidents)

**Agenda:**
1. Incident timeline reconstruction
2. What went well
3. What could be improved
4. Root cause analysis
5. Action items and owners

#### 6.2 Documentation Requirements

| Document | Contents | Owner |
|----------|----------|-------|
| Incident Report | Full timeline, actions taken, impact assessment | IR Lead |
| Root Cause Analysis | Technical and process failures identified | IR Lead |
| Improvement Plan | Specific remediation actions with deadlines | CISO |
| Metrics Report | Response time, containment time, recovery time | SOC |

#### 6.3 Improvement Categories

- **Technical Controls:** New security tools, configuration changes
- **Process Updates:** Procedure modifications, playbook updates
- **Training Needs:** Identified gaps in team skills or user awareness
- **Policy Changes:** Updates to security policies or standards

---

## 5. Communication Plan

### 5.1 Internal Communications

| Audience | Communication Method | Timing | Owner |
|----------|---------------------|--------|-------|
| IRT Members | Secure channel (Teams/Slack) | Immediate | IR Lead |
| IT Leadership | Direct call + email | < 30 min | IR Lead |
| Executive Team | Briefing call | Within 2 hours | CISO |
| All Employees | Email notification | After containment | Comms |
| Board of Directors | Executive summary | Within 24-48 hours | CISO |

### 5.2 External Communications

| Audience | Trigger | Timing | Owner |
|----------|---------|--------|-------|
| Customers | Data breach affecting their data | Per regulatory requirements | Legal/Comms |
| Regulators | Reportable incident | Per regulation (24-72 hours) | Legal |
| Law Enforcement | Criminal activity, significant breach | As appropriate | Legal |
| Media | Public-facing incident | After legal approval | Comms |
| Partners/Vendors | Their systems/data affected | As needed | IR Lead |

### 5.3 Communication Templates

Maintain pre-approved templates for:
- Internal incident notification
- Customer breach notification
- Regulatory notification
- Press statement
- Employee FAQ

---

## 6. Escalation Criteria

### 6.1 Escalation Matrix

| Severity | Initial Response | Escalate To | Executive Notification |
|----------|-----------------|-------------|----------------------|
| **Critical** | SOC Analyst | IR Lead immediately | CISO within 15 min |
| **High** | SOC Analyst | IR Lead within 30 min | CISO within 1 hour |
| **Medium** | SOC Analyst | IR Lead within 4 hours | Daily summary |
| **Low** | SOC Analyst | Document only | Weekly summary |

### 6.2 Automatic Escalation Triggers

The following conditions trigger immediate executive escalation:

- Ransomware or destructive malware detected
- Confirmed data breach of sensitive data
- Compromise of privileged accounts (administrator, executive)
- Evidence of advanced persistent threat (APT)
- Attack on critical infrastructure
- Potential regulatory notification required
- Media coverage or public exposure likely

---

## 7. Documentation & Evidence Handling

### 7.1 Incident Ticket Requirements

Every incident must have a ticket containing:

| Field | Description |
|-------|-------------|
| Incident ID | Unique identifier |
| Date/Time Detected | When first identified |
| Date/Time Reported | When formally reported |
| Reporter | Who identified the incident |
| Severity Level | Initial and final classification |
| Affected Systems | List of impacted assets |
| Affected Users | List of impacted accounts |
| IOCs | All indicators collected |
| Actions Taken | Chronological action log |
| Status | Open, Contained, Eradicated, Recovered, Closed |

### 7.2 Evidence Preservation

#### Chain of Custody

| Requirement | Description |
|-------------|-------------|
| **Documentation** | Who collected, when, where, how |
| **Integrity** | Hash values recorded before/after handling |
| **Storage** | Secure, access-controlled location |
| **Access Log** | Record everyone who accessed evidence |

#### Evidence Types

| Evidence Type | Collection Method | Retention |
|---------------|-------------------|-----------|
| System logs | SIEM export | 1 year minimum |
| Memory dumps | Forensic tools | Duration of investigation |
| Disk images | Bit-for-bit copy | Duration of investigation |
| Network captures | PCAP files | 90 days minimum |
| Email evidence | Original + headers | Duration of investigation |
| Screenshots | Timestamped images | Duration of investigation |

### 7.3 Retention Requirements

| Document Type | Retention Period |
|---------------|------------------|
| Incident tickets | 7 years |
| Evidence (legal hold) | Until legal releases |
| Lessons learned | Permanent |
| Communication records | 3 years |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | February 2026 | [Author] | Initial release |

**Review Schedule:** Annual or after significant incidents

**Approval:**

| Role | Name | Signature | Date |
|------|------|-----------|------|
| CISO | | | |
| Legal | | | |
| IT Director | | | |

---

*This document is aligned with NIST SP 800-61r2 (Computer Security Incident Handling Guide) and incorporates industry best practices for incident response.*
