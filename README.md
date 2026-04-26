# 🪟 Windows Internals & Active Directory Security (SOC Sprint 03)

Focused on host-based analysis, Windows operating system internals, and Active Directory security fundamentals. This repository documents the transition from network-level observation to endpoint-level investigation.

---

## 🛠 Technical Stack

* **Endpoint Monitoring:** Sysinternals Suite (Process Explorer, Autoruns, Procmon), Sysmon.
* **Log Analysis:** Event Viewer (EVTX), PowerShell (Get-WinEvent).
* **Identity Management:** Active Directory Domain Services (AD DS).
* **Linux Security:** Privilege Escalation via SUID and weak permissions.

---

## 🏛 Projects & Laboratories

### 1. Active Directory Lab Deployment
* **Objective:** Setting up a scalable lab environment for security testing.
* **Scope:** Windows Server 2022 (DC) + Windows 10 Enterprise (Target).
* **Key Findings:** [Step-by-step Setup Guide](./active-directory/setup-lab.md)
* **Status:** ✅ Completed

### 2. Privilege Escalation Analysis (Linux)
* **Technique:** SUID Bit Exploitation and misconfigured permissions.
* **Report:** [Linux PrivEsc Write-up](./linux/privesc-report.md)
* **Status:** ✅ Completed

---

## 📁 Repository Structure

| Folder | Contents | Key Focus |
| :--- | :--- | :--- |
| `event-ids/` | [Event Analysis Guide](./event-ids/guide.md) | Detection of Brute-force, PtH, and Kerberoasting. |
| `powershell/` | [SOC PowerShell Library](./powershell/commands.md) | Practical commands for live incident triage. |
| `active-directory/` | [AD Attacks & Detection](./active-directory/attacks.md) | Correlating attacker actions with Domain Controller logs. |
| `linux/` | [Linux Security Basics](./linux/commands.md) | SUID, file permissions, and basic log monitoring. |

---

## 🔍 Core SOC Competencies Demonstrated

* **Process Analysis:** Distinguishing between legitimate system processes (`lsass.exe`, `svchost.exe`) and malicious masquerading.
* **Registry Forensics:** Investigating persistence mechanisms in `Run` and `RunOnce` keys.
* **Log Correlation:** Mapping Event IDs (**4624**, **4688**, **4769**) to specific stages of the MITRE ATT&CK® framework.

---

## 🚩 Current Objectives

* Deepening knowledge of Kerberos authentication attacks.
* Automating log collection via PowerShell.
* Preparing for SOC L1 interview scenarios.

---

## 📜 Certifications

* **CompTIA Security+** (In Progress - Expected August 2026)

---

## 📬 Contact

* **LinkedIn:** [Aldiyar Bulat](https://www.linkedin.com/in/aldiyar-bulat-194478403/)

---

## ⚠️ Disclaimer
All activities were performed in a controlled, isolated lab environment for educational purposes.
