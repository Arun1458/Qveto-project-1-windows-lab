# Week 1 Deliverable: Application & Security Baseline Inventory (M3)

**Project:** Windows Exploitation & Privilege Escalation Lab  
**Role:** M3 — Vulnerability Assessment Analyst  
**Aligned with M2 Baseline:** `LabNet` (`10.10.10.0/24`) | Oracle VirtualBox 7.2.20  

## 1. Confirmed Lab Environment & Network Parameters
| Component | VM Name | IPv4 Address | Network Attachment | Allocated Resources | Baseline Snapshot |
|-----------|---------|--------------|--------------------|---------------------|-------------------|
| **Target System** | `windows11-lab` | `10.10.10.20/24` | Internal Network (`LabNet`) | 3 vCPUs, 4096 MB RAM, 80.00 GB Disk | `windows11-clean-install` |
| **Testing System** | `kali-linux-2026.2-virtualbox-amd64` | `10.10.10.10/24` (`eth0`) | Internal Network (`LabNet`) | 2 vCPUs, 2048 MB RAM, 80.09 GB Disk | `kali-clean-install` |

* **Isolation Boundary:** No default gateway, no DNS server, and no DHCP configured on `LabNet`.
* **Baseline Firewall Note:** Windows Firewall remains enabled; inbound ICMPv4 Echo Request rule enabled for bidirectional connectivity validation (`10.10.10.10` <-> `10.10.10.20`).

## 2. Windows 11 Guest OS & Security Baseline Status (M3 Audit Scope)
*(Addressing Outstanding Baseline Items from Week 1 Virtualization Report)*

| Baseline Check Area | Inspection Command / Tool | Current Recorded State |
|---------------------|---------------------------|------------------------|
| **Exact Guest OS Build** | `systeminfo` / `winver` | Windows 11 64-bit (Exact build version to be logged from VM) |
| **Windows Defender Status** | `Get-MpComputerStatus` | Pending baseline verification on `windows11-lab` |
| **Windows Firewall Profiles** | `netsh advfirewall show allprofiles` | Enabled (Inbound ICMPv4 Echo Request allowed on `LabNet`) |
| **Windows Update / Patch State** | `wmic qfe list brief` | Pending KB hotfix enumeration |
| **UAC Configuration** | `reg query ...\Policies\System` | Pending baseline verification |
| **Installed Applications & Services** | `sc query` / `wmic service` | Pending Week 2 service & permission audit |
