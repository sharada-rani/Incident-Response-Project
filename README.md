# 🛡️ Incident Response + Tabletop Exercise Project

[![NIST SP 800-61](https://img.shields.io/badge/Framework-NIST%20SP%20800--61-0066CC?style=for-the-badge&logo=nist&logoColor=white)](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE%20ATT%26CK-Mapped-E62129?style=for-the-badge&logo=hackaday&logoColor=white)](https://attack.mitre.org/)
[![MIT License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](./LICENSE)

---

## 📋 Overview

This project demonstrates a comprehensive **Incident Response (IR) capability** for handling cybersecurity incidents. It simulates a **phishing attack** that results in credential compromise and unauthorized access, providing complete documentation from detection through post-incident analysis.

### 🎯 Project Purpose

- **Portfolio Demonstration:** Showcase GRC and incident response skills
- **Interview Preparation:** Practice explaining IR concepts and NIST framework
- **Learning Resource:** Understand the complete incident lifecycle
- **Template:** Adapt for real organizational use

---

## 📁 Project Structure

```
📦 Incident-Response-Project
├── 📄 01-Incident-Response-Plan.md      # Comprehensive IRP (NIST SP 800-61)
├── 📊 02-RACI-Matrix.csv                # Responsibility assignment matrix
├── 📋 03-Tabletop-Exercise-Scenario.md  # Phishing simulation with injects
├── 🎨 04-IR-Workflow-Diagram.html       # Interactive swimlane flowchart
├── 📈 05-Lessons-Learned-Report.md      # Post-incident analysis & metrics
├── 📜 CHANGELOG.md                      # Version history
├── 🤝 CONTRIBUTING.md                   # Contribution guidelines
├── ⚖️ LICENSE                           # MIT License
└── 📖 README.md                         # This file
```

---

## 🔐 Scenario Overview

### Attack Simulation

| Attribute | Details |
|-----------|---------|
| **Attack Type** | Spearphishing with credential harvesting |
| **Target** | Accounts Payable employee |
| **Impact** | Credential compromise → Admin account access |
| **Data at Risk** | 15,000 customer records |

### MITRE ATT&CK Techniques

| ID | Technique | Tactic |
|----|-----------|--------|
| [T1566.001](https://attack.mitre.org/techniques/T1566/001/) | Spearphishing Attachment | Initial Access |
| [T1078](https://attack.mitre.org/techniques/T1078/) | Valid Accounts | Defense Evasion, Persistence |
| [T1110](https://attack.mitre.org/techniques/T1110/) | Brute Force | Credential Access |

---

## 📊 Incident Response Phases

This project follows the **NIST SP 800-61r2** incident response lifecycle:

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ 1. PREPARE  │───▶│ 2. DETECT   │───▶│ 3. CONTAIN  │
└─────────────┘    └─────────────┘    └─────────────┘
                                             │
                                             ▼
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│ 6. LESSONS  │◀───│ 5. RECOVER  │◀───│ 4. ERADICATE│
│   LEARNED   │    │             │    │             │
└─────────────┘    └─────────────┘    └─────────────┘
```

---

## ⏱️ Response Metrics

| Metric | Target | Achieved | Status |
|--------|--------|----------|--------|
| Time to Detect | < 30 min | 15 min | ✅ |
| Time to Contain | < 60 min | 30 min | ✅ |
| Time to Eradicate | < 4 hours | 90 min | ✅ |
| Total Duration | < 4 hours | 2 hours | ✅ |

---

## 🗂️ Deliverables Detail

### 1️⃣ Incident Response Plan
Comprehensive IRP including:
- Severity classification (Critical → Low)
- RACI-defined roles and responsibilities
- NIST-aligned response phases
- Escalation criteria and communication plan
- Evidence handling procedures

### 2️⃣ RACI Matrix
Accountability mapping for:
- 20 IR activities across 6 phases
- 6 stakeholder roles (SOC, IT, IR Lead, Legal, Management, Comms)
- Clear R/A/C/I designations

### 3️⃣ Tabletop Exercise
Simulation scenario with:
- 5 time-stamped injects (09:15 - 10:00 AM)
- MITRE ATT&CK technique mapping
- 7 discussion questions with detailed answers
- Facilitator preparation checklist

### 4️⃣ Workflow Diagram
Interactive HTML diagram featuring:
- 4 swimlanes (SOC, IT, Legal, Management)
- 7 response phases visualized
- Hover effects and professional styling

### 5️⃣ Lessons Learned Report
Post-incident analysis including:
- Root cause analysis (5 Whys method)
- 8 control gaps identified
- 12 recommendations with owners and due dates
- Remediation tracking dashboard

---

## 🚀 Getting Started

### View the Project
```bash
# Clone the repository
git clone https://github.com/sharada-rani/Incident-Response-Project.git

# Open the workflow diagram in your browser
start 04-IR-Workflow-Diagram.html

# Import RACI Matrix to spreadsheet
# Open 02-RACI-Matrix.csv in Excel or Google Sheets
```

### Use as Template
1. Fork this repository
2. Customize organization names and contacts
3. Adapt scenarios for your industry
4. Update severity thresholds as needed

---

## 💼 Resume Bullets

Use these on your resume:

> **Standard:**
> Developed an incident response plan aligned with NIST SP 800-61 and conducted a tabletop exercise simulating a phishing incident.

> **With Impact:**
> Developed an incident response plan and led a tabletop exercise simulating a phishing incident, identifying 8 control gaps and recommending remediation actions.

> **Metrics-Based:**
> Created incident response documentation achieving 15-minute detection time and 30-minute containment, with MITRE ATT&CK technique mapping.

---

## 🎤 Interview Questions You Can Answer

After completing this project, you can confidently answer:

- ✅ "Walk me through how you would handle a phishing incident"
- ✅ "What's the difference between containment and eradication?"
- ✅ "Who should be notified during a security incident?"
- ✅ "How do you measure incident response effectiveness?"
- ✅ "What is MITRE ATT&CK and how do you use it?"
- ✅ "How does incident response tie into compliance?"

---

## 📚 Resources & References

| Resource | Description |
|----------|-------------|
| [NIST SP 800-61r2](https://csrc.nist.gov/publications/detail/sp/800-61/rev-2/final) | Computer Security Incident Handling Guide |
| [MITRE ATT&CK](https://attack.mitre.org/) | Adversarial Tactics, Techniques & Knowledge |
| [SANS IR Handbook](https://www.sans.org/white-papers/33901/) | Incident Handler's Handbook |

---

## 🤝 Contributing

Contributions are welcome! See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

**Ideas for contribution:**
- Additional tabletop scenarios (ransomware, insider threat)
- Industry-specific IR templates
- Translated versions
- Improved visualizations

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](./LICENSE) for details.

---

## 👤 Author

**Sharada Rani**

- GitHub: [@sharada-rani](https://github.com/sharada-rani)

---

<p align="center">
  <i>Built with ❤️ for the cybersecurity community</i>
</p>
