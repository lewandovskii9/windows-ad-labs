# Active Directory & Endpoint Security Lab

*Focused on host-based analysis, Windows operating system internals, and Active Directory security fundamentals. This repository documents the transition from network-level observation to endpoint-level investigation.*

---

## 🛠 Technical Stack

* **Endpoint Monitoring:** Sysinternals Suite (Process Explorer, Autoruns, Procmon), Sysmon.
* **Log Analysis & Detection:** Windows Event Logs (EVTX), Audit Policy Configuration.
* **Identity Management:** Active Directory Domain Services (AD DS).
* **Linux Security:** Privilege Escalation via SUID and weak file permissions.

---

## 🔧 Tools & Techniques

* **SIEM & Logging:** Event Viewer analysis, Advanced Security Audit Policy tweaking.
* **Network & AD:** LDAP Enumeration protocols, Kerberos authentication workflows.
* **System Internals:** Registry auditing, process tracking, SUID binary exploitation.

---

## 📁 Labs

This section contains the core practical work for this sprint, including lab setups, attack simulations, and detection methodology.

| #  | Lab                                                         | Key Findings                                                 | Focus Area |
| -- | ----------------------------------------------------------- | ------------------------------------------------------------ | ---------- |
| 01 | [AD Lab Deployment](./active-directory/setup-lab.md)        | Step-by-step DC & Win10 setup, user creation, forest configuration | Infrastructure |
| 02 | [Linux Privilege Escalation](./linux/privesc-report.md)     | Exploiting SUID bits and misconfigured file permissions    | Privilege Escalation |
| 03 | [Event ID Analysis Guide](./event-ids/guide.md)             | Mapping Event IDs (4624, 4688, 4769) to attack stages       | Detection |
| 04 | [AD Attacks & Detection](./active-directory/attacks.md)     | Simulating attack techniques and log correlation             | Active Directory |

---

## 🚩 Current Objectives

* Analyze post-exploitation activities after a malicious PE execution.
* Deepening knowledge of Kerberos authentication attacks.
* Developing SIEM correlation rules for Active Directory anomalies.

---

## ⚠️ Disclaimer
All activities were performed in a controlled, isolated lab environment for educational purposes.

---
[![Back to Profile](https://img.shields.io/badge/BACK_TO_PROFILE-333333?style=plastic&logo=github&logoColor=white)](https://github.com/lewandovskii9)
