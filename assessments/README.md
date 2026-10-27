# M3 Vulnerability Assessment & Configuration Inventory

**Role:** Vulnerability Assessment Analyst (M3)  
**Target Environment:** `windows11-lab` (Isolated on `LabNet`)  

## 1. Folder Purpose
This directory contains the core defensive auditing and vulnerability assessment deliverables for Project 1. It documents the identification, risk rating, and re-validation of privilege escalation misconfigurations within the authorized Windows 11 virtual machine.

## 2. Methodology & Safe Operating Boundaries
All assessments documented in this folder strictly adhere to the project's Rules of Engagement. 
* **Non-Destructive Testing:** Vulnerability discovery relies exclusively on read-only Windows administrative commands (e.g., `wmic`, `sc qc`, `icacls`, `reg query`).
* **Isolation Compliance:** No external scripts, automated exploitation frameworks, or destructive payloads were executed. All audits were performed locally on `10.10.10.20/24`.

## 3. Directory Index
This folder contains the following M3 lifecycle deliverables:
* **`vulnerability_inventory.md`**: Initial baseline configuration review and permission templates.
* **`week3-telemetry-control-matrix.md`**: Mapping of Week 2 findings to expected Sysmon and Event Viewer defensive telemetry (coordinated with M5).
* **`remediation-validation-criteria.md`**: Technical pass/fail conditions and command references required to verify M6's remediation fixes during Week 4 re-testing.

## 4. How to Interpret Results
Findings are categorized by Severity (Low to Critical) based on the local privilege impact (e.g., Standard User to `NT AUTHORITY\SYSTEM`). Validated fixes will be updated in the vulnerability register upon successful re-execution of the audit test cases.
