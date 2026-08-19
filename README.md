# Active Directory & Endpoint Security Lab

*Focused on host-based analysis, Windows operating system internals, and Active Directory security fundamentals. This repository documents the transition from network-level observation to endpoint-level investigation.*

---

## 🛠 Technical Stack

* **Log Analysis & Detection:** Windows Event Logs (EVTX), Audit Policy Configuration.
* **Identity Management:** Active Directory Domain Services (AD DS).

---

## 🔧 Tools & Techniques

* **SIEM & Logging:** Event Viewer analysis, Advanced Security Audit Policy tweaking.
* **Network & AD:** LDAP Enumeration protocols, Kerberos authentication workflows.
* **System Internals:** Registry auditing, process tracking.

---

## 📁 Labs

This section contains the core practical work for this sprint, including lab setups, attack simulations, and detection methodology.

| #  | Lab                                                         | Key Findings                                                 | Focus Area |
| -- | ----------------------------------------------------------- | ------------------------------------------------------------ | ---------- |
| 01 | [AD Lab Deployment](./active-directory/setup-lab.md)        | Step-by-step DC 2019 & Win10 setup, user creation, forest configuration | Infrastructure |
| 02 | [AD Attacks & Detection](./active-directory/ad-attacks-analysis.md)     | Simulating attack techniques and log correlation             | Active Directory |
| 03 | [Windows Privilege Escalation](windows/privesc-report.md) | Exploiting Unquoted Service Paths and insecure service execution paths | Privilege Escalation |


---

## 🚩 Objectives

* Analyze post-exploitation activities after a malicious PE execution.
* Deepening knowledge of Kerberos authentication attacks.

---

## ⚠️ Disclaimer
All activities were performed in a controlled, isolated lab environment for educational purposes.

---
[![Back to Profile](https://img.shields.io/badge/BACK_TO_PROFILE-333333?style=plastic&logo=github&logoColor=white)](https://github.com/lewandovskii9)
