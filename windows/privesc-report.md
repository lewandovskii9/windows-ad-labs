# Windows Privilege Escalation: Unquoted Service Paths

This section covers the practical exploitation and detection of a common Windows local privilege escalation vector: **Unquoted Service Paths**. The attack exploits ambiguity in the Windows API command-line parser when resolving unquoted file paths containing spaces.

## 1. Attack Vector Overview

When a Windows service is registered with a binary path that contains spaces and is **not enclosed in double quotes**, the Service Control Manager (SCM) attempts to locate the executable by sequentially searching each space-delimited segment:

- **Configured Path:** `C:\Program Files\My App\service.exe`
    
- **Execution Attempt Order:**
    
    1. `C:\Program.exe`
        
    2. `C:\Program Files\My.exe`
        
    3. `C:\Program Files\My App\service.exe`
        

If a low-privileged user has write permissions to any intermediate directory (e.g., `C:\`), they can drop a malicious payload named `Program.exe`. Upon service startup (often under `NT AUTHORITY\SYSTEM`), the payload executes with elevated privileges.

#### **Scenario :**

Some administrator created folder with wrong rights.

Threat actor already in system, and found this folder. Uploaded in malware, and wait until administrator refresh it.

## 2. Attack Simulation

### Step 1: Enumeration

First, we search the system using PowerShell to find services where path has spaces and no quotes. We found `VulnerableService` with path `C:\Program Files\My service\service.exe`.

![[Pasted image 20260727175810.png|697]]

### Step 2: Exploitation

Because Windows checks `C:\Program.exe` first before going into `Program Files`, we copy `whoami.exe` into `C:\Program.exe` as a test binary. Then we try to start the service:

Commands used:

1 - `copy C:\Windows\System32\whoami.exe C:\Program.exe`

2 - `sc.exe start VulnerableService`

**Result :**

The service fails with **Error 1053**. This happens because `whoami.exe` is just a simple CLI tool and not a real Windows service. But this error **100% proves** that Windows actually executed our hijacked `C:\Program.exe` file instead of original binary!

![[Pasted image 20260727181159.png]]

## 3. SOC Detection

When this fake binary fails to respond like a normal service, Windows Service Control Manager automatically logs two error events in the **System** log.

**EventID 7000:**

This event shows that `VulnerableService` failed to start because of error `1053`.

![[Pasted image 20260727183208.png|537]]

**EventID 7009:**

This event logs a timeout — system waited 30000 ms (30 seconds) for `VulnerableService` to connect, but got no response from `C:\Program.exe`.

![[Pasted image 20260727183318.png|544]]

#### IoCs

**File & Service Indicators**

|**Type**|**Value**|
|---|---|
|Dropped Payload|`C:\Program.exe`|
|Target Service Name|`VulnerableService`|
|Unquoted Service Path|`C:\Program Files\My service\service.exe`|

**Target Object Indicators**

|**Type**|**Value**|
|---|---|
|Target Computer|`DC01.lewa9-soc.lab`|
|Channel|`System`|
|Provider Name|`Service Control Manager`|

**Technical Parameters**

|**Type**|**Value**|
|---|---|
|EventID|`7000`, `7009`|
|EventRecordID|`5946` (7000), `5945` (7009)|
|ProcessID / ThreadID|`616` / `6060`|
|Timeout Value|`30000` ms|
|Error Code|`1053`|

#### Recommended Actions

1. **Delete file** `C:\Program.exe` from system root.
   
2. **Restrict permissions** on `C:\` folder so regular users cannot write there.
   
3. **Set SIEM alert** for EventIDs `7000` and `7009` with error `1053`.
