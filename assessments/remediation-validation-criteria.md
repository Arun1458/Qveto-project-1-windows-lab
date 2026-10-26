# Week 3 Deliverable: Remediation Verification & Audit Standards (M3)

**Project:** Windows Exploitation & Privilege Escalation Lab  
**Prepared by:** Shrinidhi Shankar (M3 — Vulnerability Assessment Analyst)  
**Date:** 26 October 2026  
**Target Environment:** `windows11-lab` (`10.10.10.20/24`) — Build `10.0.26300.9457`  
**Collaborating Role:** M6 (Remediation & Retesting Lead)  

---

## 1. Objective
Establish technical pass/fail criteria for verifying that the vulnerabilities and misconfigurations cataloged in Week 2 have been remediated on `windows11-lab`. These criteria define the re-assessment checks M3 will execute during Week 4 validation.

---

## 2. Technical Remediation & Audit Verification Standards

| Finding ID | Vulnerability / Misconfiguration | Expected Remediation Action (M6) | Audit Verification Command (M3) | Success / Pass Criteria |
|---|---|---|---|---|
| **FIND-01** | Mounted Unattended Setup Media | Eject virtual media from SATA Port 1; remove plaintext answer files (`autounattend.xml`) | `Get-Volume` / `dir C:\Windows\Panther` | Optical drive is empty; no setup answer files containing credentials exist on the file system. |
| **FIND-02** | Inbound ICMPv4 Firewall Rule | Review exception scope; document requirement for lab validation | `netsh advfirewall firewall show rule name="ICMPv4-In"` | Rule is strictly scoped to `10.10.10.10` or documented as an authorized exception under RoE. |
| **FIND-03** | Unquoted Service Path (`QvetoVulnService`) | Enclose executable binary path in double quotes (`"..."`) in service registry configuration | `wmic service where "name='QvetoVulnService'" get pathname` | Path string contains enclosing quotes around the full executable target path. |
| **FIND-04** | Insecure Directory Permissions (ACLs) | Strip write/modify rights from standard accounts (`Users`, `Everyone`) on application directories | `icacls "C:\Program Files\Qveto Vulnerable App"` | Only `SYSTEM` and `Administrators` retain Full Control (`(F)`); standard users retain Read & Execute (`(RX)`). |
| **FIND-05** | Standard Account Privilege Scope | Verify standard user is not added to local administrative groups; maintain default UAC behavior | `net localgroup administrators` / `reg query ...\Policies\System /v EnableLUA` | `LABWIN` is absent from administrative group; `EnableLUA` returns `0x1`. |
| **FIND-06** | Windows Installer Elevation Policy | Remove or disable `AlwaysInstallElevated` registry DWORD keys | `reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated` | Key returns `ERROR: The system was unable to find the specified registry key or value` or evaluates to `0x0`. |

---

## 3. Retest Protocol & Safety Guardrails
* **Pre-Retest Requirement:** M6 applies changes and notifies M3 with updated configuration notes.
* **Execution Boundary:** Re-tests will follow the same non-destructive commands documented in `test-cases/m3-audit-test-cases.md`[cite: 7, 8, 9].
* **Logging Requirement:** Retest activity must be coordinated with M5 to ensure baseline telemetry reflects clean or blocked events[cite: 2, 8].
