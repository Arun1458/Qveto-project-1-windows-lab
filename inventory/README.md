# M3 System, Application & Baseline Inventory

**Role:** Vulnerability Assessment Analyst (M3)  
**Target Environment:** `windows11-lab` (`10.10.10.20/24`)  

## 1. Folder Purpose
This directory maintains the authoritative baseline record for the isolated Windows 11 virtual machine prior to any authorized vulnerability testing or remediation actions. It fulfills the Week 1 project requirement to document operating system parameters, patch states, and installed applications.

## 2. Inventory Scope
The baselines documented here include:
* **Host & OS Specifications:** Exact Windows 11 build version (`10.0.26300.9457`), architecture, and hardware resource allocations.
* **Network Isolation Details:** VirtualBox internal network (`LabNet`) configurations, MAC addresses, and IPv4 parameters ensuring strict isolation.
* **Security Baselines:** Initial state of Windows Defender, Windows Firewall profiles, and User Account Control (UAC) registry policies prior to M6 remediation.

## 3. Lifecycle Relevance
This baseline inventory serves as the "Before" state. During Week 4 (Retesting & Analysis), M3 will compare the final remediated state of `windows11-lab` against these initial records to verify that security controls (such as `AlwaysInstallElevated` and unquoted service paths) have been successfully corrected without breaking baseline system functionality.
