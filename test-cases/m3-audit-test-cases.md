# Week 2 & 3 Deliverable: Approved Non-Destructive Audit Test Cases (M3)

**Project:** Windows Exploitation & Privilege Escalation Lab  
**Prepared by:** Shrinidhi Shankar (M3 — Vulnerability Assessment Analyst)  
**Target VM:** `windows11-lab` (`10.10.10.20/24`) — Build `10.0.26300.9457`  

---

## Test Case 1: Service Path Hygiene & Binary Permission Audit (`TC-M3-01`)
* **Objective:** Identify non-default Windows services running with `LocalSystem` privileges that contain unquoted spaces in their executable path (`ImagePath`).
* **Prerequisites:** Local access as `LABWIN` on isolated `LabNet` (`10.10.10.20`); snapshot `w1-network-verified` confirmed active.
* **Approved High-Level Steps:**
  1. Open standard Command Prompt (`cmd.exe`) as `LABWIN`.
  2. Query non-Windows auto-start services via WMIC/CIM (`wmic service get name,displayname,pathname,startmode`).
  3. Inspect parent directory permissions using `icacls` to verify whether standard users hold write/modify rights.
* **Expected Control Behavior (Week 3 Telemetry Link for M5):** Process creation events logged in Sysmon (Event ID 1) and Windows Security Log (Event ID 4688); no UAC prompt triggered for read-only enumeration.
* **Cleanup Procedure:** Read-only enumeration; no files or registry keys modified.

---

## Test Case 2: Windows Installer Elevation Policy Check (`TC-M3-02`)
* **Objective:** Determine whether the `AlwaysInstallElevated` policy is enabled in both `HKLM` and `HKCU` registry hives.
* **Prerequisites:** Local command prompt access as `LABWIN` on `windows11-lab`.
* **Approved High-Level Steps:**
  1. Run `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`.
  2. Run `reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated`.
* **Expected Control Behavior (Week 3 Telemetry Link for M5):** Sysmon Event ID 1 (Process Creation for `reg.exe`) recorded; standard registry read succeeds or returns `ERROR: The system was unable to find the specified registry key or value` if securely disabled.
* **Cleanup Procedure:** Read-only query; no system state changes required.

---

## Test Case 3: Local Account Token & UAC Configuration Review (`TC-M3-03`)
* **Objective:** Inventory local user token privileges (`whoami /priv`) and User Account Control (`EnableLUA` / `ConsentPromptBehaviorAdmin`) enforcement levels.
* **Prerequisites:** Local session as `LABWIN` on `windows11-lab`.
* **Approved High-Level Steps:**
  1. Execute `whoami /all` to record group SIDs, token privileges (such as `SeShutdownPrivilege`, `SeChangeNotifyPrivilege`, `SeImpersonatePrivilege`), and integrity level (`Medium` vs `High`).
  2. Query `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System` to verify UAC prompt behavior.
* **Expected Control Behavior (Week 3 Telemetry Link for M5):** Standard user session runs under Medium Mandatory Integrity Level unless elevated via UAC consent prompt (Event ID 4648 / 4624).
* **Cleanup Procedure:** Read-only check; no cleanup required.
