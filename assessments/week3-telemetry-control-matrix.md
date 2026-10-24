# Week 3 Deliverable: Vulnerability-to-Telemetry Control Matrix (M3 / M5)

**Project:** Windows Exploitation & Privilege Escalation Lab  
**Prepared by:** Shrinidhi Shankar (M3 — Vulnerability Assessment Analyst)  
**Target Host:** `windows11-lab` (`10.10.10.20/24`) — Build `10.0.26300.9457`  
**Network Scope:** Isolated Internal Network (`LabNet`)  
**Coordination Roles:** M3 (Assessment Audit) & M5 (Detection & Telemetry Engineer)  

---

## 1. Objective & Scope
The objective of this matrix is to map each audit finding identified during the Week 2 vulnerability review to the expected defensive telemetry sources on Windows 11. During Week 3, this record guides M5 in identifying whether local endpoint controls (Windows Defender, Event Viewer, Sysmon, Process Monitor, and UAC) successfully log, alert on, or constrain unauthorized privilege adjustments.

---

## 2. Telemetry & Control Mapping Matrix

| Finding ID | Weakness Description | Expected Primary Telemetry Source | Relevant Event ID / Alert Source | Expected Defensive Behavior | Status for M5 Review |
|---|---|---|---|---|---|
| **FIND-01** | Unattended Setup Media on Optical Drive | Windows Security Event Log | Event ID 4663 (Object Access) / File System Auditing | File access attempts to mounted setup media logged | Pending Log Review |
| **FIND-02** | Inbound ICMPv4 Firewall Rule Exception | Windows Firewall with Advanced Security | Event ID 2005 / 2006 (Firewall Rule Modification) | Configuration changes to firewall rule profile captured | Logged in Week 1 |
| **FIND-03** | Unquoted Service Path (`QvetoVulnService`) | Sysmon / Security Log / Process Monitor | Sysmon Event ID 1 (Process Create) / Event ID 4688 | Subprocess launch and process tree path recorded | Pending Test Verification |
| **FIND-04** | Insecure Directory Permissions (ACLs) | Security Log / Access Auditing | Event ID 4670 (Permissions Changed) / Event ID 4663 | Modification attempts on application directories recorded | Pending Test Verification |
| **FIND-05** | Local User Integrity & Privilege Scope | Local Security Authority / Sysmon | Event ID 4624 (Logon) / Event ID 4648 (Explicit Creds) / Sysmon Event ID 1 | Token elevation prompts and integrity switches observed | Pending Test Verification |
| **FIND-06** | Windows Installer Elevation Policy | Windows Application Log / Sysmon | MsiInstaller Event ID 1040 / 1042 / Sysmon Event ID 1 | Package execution with elevated token logged in application channel | Pending Test Verification |

---

## 3. Defensive Evaluation Guidelines (KPI Alignment)
* **Detection Coverage:** Proportion of simulated audit test cases (`TC-M3-01` through `TC-M3-03`) that produce an observable event or alert.
* **Prevention Coverage:** Proportion of unapproved actions blocked or constrained by default security controls (e.g., UAC consent blocking, file permission denial).
* **Telemetry Verification Note:** M3 documents expected baseline indicators; M5 executes log capture and correlates timestamps within Event Viewer and Sysmon.
