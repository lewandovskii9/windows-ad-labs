# Active Directory

*Focused on host-based analysis, Windows operating system internals, and Active Directory security fundamentals. This repository documents the transition from network-level observation to endpoint-level investigation.*

---

## 🛠 Technical Stack

* **Endpoint Monitoring:** Sysinternals Suite (Process Explorer, Autoruns, Procmon), Sysmon.
* **Log Analysis:** Event Viewer (EVTX), PowerShell (Get-WinEvent).
* **Identity Management:** Active Directory Domain Services (AD DS).
* **Linux Security:** Privilege Escalation via SUID and weak permissions.

---

## 🔧 Tools & Techniques

* **Sysinternals:** Process Explorer, Autoruns, Process Monitor (Procmon).
* **Built-in Tools:** Event Viewer (EVTX), Registry Editor, PowerShell.
* **Network & AD:** Wireshark (AD protocol analysis), BloodHound (theoretical), Mimikatz (theoretical).
* **Linux:** SUID/GUID analysis, permission auditing.

---

## 📁 Labs

This section contains the core practical work for this sprint, including lab setups, attack simulations, and detection methodology.

| #  | Lab                                           | Key Findings                                | Focus Area |
| -- | ----------------------------------------------------------- | --------------------------------------------------------- | ---------- |
| 01 | [AD Lab Deployment](./active-directory/setup-lab.md)        | Step-by-step DC & Win10 setup, user creation, forest configuration | Infrastructure |
| 02 | [Linux Privilege Escalation](./linux/privesc-report.md)     | Exploiting SUID bits and misconfigured file permissions   | Privilege Escalation |
| 03 | [Event ID Analysis Guide](./event-ids/guide.md)             | Mapping Event IDs (4624, 4688, 4769) to attack stages     | Detection |
| 04 | [AD Attacks & Detection](./active-directory/attacks.md)     | Simulating Kerberoasting and PtH with log correlation     | Active Directory |
| 05 | [SOC PowerShell Library](./powershell/commands.md)          | Practical automation for live incident triage and hunting | Tooling |

---

## 🚩 Current Objectives

* Analyze post-exploitation activities after a malicious PE execution.
* Deepening knowledge of Kerberos authentication attacks.
* Automating log collection via PowerShell.

---

## ⚠️ Disclaimer
All activities were performed in a controlled, isolated lab environment for educational purposes.

---
[![Back to Profile](https://img.shields.io/badge/←_Back_to_Profile-grey?style=flat-square)](https://github.com/lewandovskii9)
*Return to [Main Portfolio](https://github.com/lewandovskii9)*
