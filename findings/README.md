# M3 Vulnerability & Misconfiguration Findings

**Role:** Vulnerability Assessment Analyst (M3)  
**Target Environment:** `windows11-lab` (`10.10.10.20/24`)  

## 1. Folder Purpose
This directory houses the Vulnerability Register for Project 1. It catalogs all security weaknesses, unquoted service paths, weak folder permissions (ACLs), and registry misconfigurations identified during the Week 2 M3 baseline audit.

## 2. Severity Rationale & Scoring
Findings are assigned a severity rating based on their potential impact on local privilege escalation:
* **Critical:** Direct bypass of security boundaries (e.g., `AlwaysInstallElevated` allowing standard users to execute `.msi` payloads as `SYSTEM`).
* **High:** Misconfigurations requiring minor prerequisites to achieve privilege escalation (e.g., writable application directories combined with unquoted service paths).
* **Medium/Low:** Hygiene issues, standard user privilege scope deviations, or baseline firewall exceptions.

## 3. Assessment Limitations
* **Scope Confinement:** All recorded findings are isolated to the authorized `windows11-lab` VM on the internal `LabNet` network.
* **No Active Exploitation:** Vulnerabilities were identified via non-destructive administrative queries (`wmic`, `icacls`, `reg query`). No exploit payloads were executed to validate these findings, adhering strictly to the Week 1 Rules of Engagement.
* **Telemetry Dependency:** Defensive detection of these findings relies on Windows Event Logs and Sysmon, which is coordinated with the Detection Engineer (M5).
