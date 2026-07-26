# Windows Privilege Escalation: Unquoted Service Paths

This section covers the practical exploitation and detection of a common Windows local privilege escalation vector: **Unquoted Service Paths**. The attack exploits ambiguity in the Windows API command-line parser when resolving unquoted file paths containing spaces.

---

## 1. Attack Vector Overview

When a Windows service is registered with a binary path that contains spaces and is **not enclosed in double quotes**, the Service Control Manager (SCM) attempts to locate the executable by sequentially searching each space-delimited segment:

* **Configured Path:** `C:\Program Files\My App\service.exe`
* **Execution Attempt Order:**
  1. `C:\Program.exe`
  2. `C:\Program Files\My.exe`
  3. `C:\Program Files\My App\service.exe`

If a low-privileged user has write permissions to any intermediate directory (e.g., `C:\`), they can drop a malicious payload named `Program.exe`. Upon service startup (often under `NT AUTHORITY\SYSTEM`), the payload executes with elevated privileges.

---

## 2. Attack Simulation

### Step 1: Enumeration
Identifying vulnerable unquoted services using `WMIC` or PowerShell:

cmd
:: Command Prompt Enumeration
wmic service get name,displayname,pathname,startmode | findstr /i /v "C:\Windows\\" | findstr /i /v
PowerShell# PowerShell Enumeration
Get-WmiObject win32_service | Where-Object { $_.PathName -notlike '"*' -and $_.PathName -like '* *' } | Select-Object Name, PathName, StartMode
Step 2: Exploitation SetupTarget Identification: Service VulnerableService running with path C:\Program Files\My App\service.exe.Payload Delivery: Place a custom binary or reverse shell payload at C:\Program.exe.Trigger Execution: Restart the service or reboot the system:DOSsc stop VulnerableService
sc start VulnerableService

## 3. SOC Detection
To detect this behavior, SOC analysts monitor specific Windows Event Logs for service creation and suspicious binary executions from root paths.Key Event LogsSystem Log — Event ID 7045 (Service Creation)Fires when a new service is installed. Analyzed to detect unquoted paths at creation time.Security Log — Event ID 4688 (Process Creation)Fires when Program.exe or My.exe is executed directly from non-standard system directories like C:\.Captured Log Example (Event ID 7045)PlaintextLog Name:      System
Source:        Service Control Manager
Event ID:      7045
Level:         Information
Task Category: None
Description:
A service was installed in the system.

Service Name:  VulnerableService
Service File Name: C:\Program Files\My App\service.exe
Service Type:  user mode service
Service Start Type: auto start
Account Name:  LocalSystem

### 4. IoCs

Directory Access Controls (ACLs): Restrict write/modify permissions on C:\ and C:\Program Files\ for standard users (BUILTIN\Users).Automated Audit: Run periodic PowerShell audits or GPO checks to automatically fix unquoted service paths across the domain.
