# Week 1 & 2 Deliverable: VM, OS & Configuration Baseline Inventory (M3)

**Project:** Windows Exploitation & Privilege Escalation Lab  
**Prepared by:** Shrinidhi Shankar (M3 — Vulnerability Assessment Analyst)  
**Date Updated:** 21 October 2026  
**Target Environment:** `LabNet` (`10.10.10.0/24`) on Oracle VirtualBox 7.2.20  

---

## 1. Verified Guest OS & User Account Inventory (From Lab Evidence)

| Property | Target VM (`windows11-lab`) | Testing VM (`kali-linux-2026.2-virtualbox-amd64`) |
|----------|-----------------------------|---------------------------------------------------|
| **Exact OS Version / Build** | Microsoft Windows 11 (64-bit) — `Version 10.0.26300.9457` | Kali Linux 2026.2 (Debian 64-bit) |
| **Active Local User Account** | `C:\Users\LABWIN` (`LABWIN`) | `kali@kali` |
| **Allocated CPU / RAM** | 3 vCPUs / 4096 MB RAM | 2 vCPUs / 2048 MB RAM |
| **Virtual Storage (VDI)** | `windows11-lab.vdi` (80.00 GB, SATA Port 0) | `kali-linux-2026.2-virtualbox-amd64.vdi` (80.09 GB, SATA Port 0) |
| **Optical Drive (SATA Port 1)** | `Unattended-cddcb9b5-b668-4185-910b-88e884f7a503-aux-iso.viso` | Empty |
| **Platform Security Controls** | TPM 2.0, EFI Enabled, Secure Boot Enabled | PAE/NX, Nested Paging, KVM Paravirtualization |
| **Snapshots Recorded** | `windows11-clean-install`, `w1-network-verified` | `kali-clean-install`, `w1-network-verified` |

---

## 2. Verified Network & Isolation Baseline

| Parameter | Target VM (`windows11-lab`) | Testing VM (`kali-linux-2026.2-virtualbox-amd64`) |
|-----------|-----------------------------|---------------------------------------------------|
| **Network Attachment** | Internal Network (`LabNet`) | Internal Network (`LabNet`) |
| **Adapter Hardware Type** | Intel PRO/1000 MT Desktop (`82540EM`) | Intel PRO/1000 MT Desktop (`82540EM`) |
| **MAC Address** | `080027A225CD` | `0800275A87BC` |
| **Promiscuous Mode** | `Deny` | `Deny` |
| **IPv4 Address / Subnet** | `10.10.10.20` / `255.255.255.0` (`/24`) | `10.10.10.10/24` (`eth0`) |
| **Link-Local IPv6 Address** | `fe80::bfce:cc09:d8c9:3173%4` | N/A (IPv4 scope link confirmed via `ip route`) |
| **Default Gateway / DNS** | Blank (None configured — Confirmed Isolated) | None (`10.10.10.0/24 dev eth0 proto kernel scope link`) |

---

## 3. M3 Baseline Configuration Audit Observations (Week 1 Verification)

1. **OBS-M3-01 (Firewall Exception Change):** The Windows Firewall inbound ICMPv4 Echo Request rule was enabled on `windows11-lab` to permit ICMP echo requests from `10.10.10.10` (`0% packet loss`, TTL=128).
2. **OBS-M3-02 (Validation Test Command Discrepancy):** In `ping-windows-to-kali.png`, the Windows host `LABWIN` executed `ping 10.10.10.20` (loopback ping to its own IPv4 address) rather than `ping 10.10.10.10`. Bidirectional connectivity is confirmed via the ARP/ICMP reply in `ping-kali-to-windows.jpeg`, and `ping 10.10.10.10` should be re-captured from `LABWIN`.
3. **OBS-M3-03 (Pre-Isolation Adapter Snapshot Check):** `Kali VM Config 2.png` captured Adapter 1 in `NAT` mode prior to switching to `Internal Network ('LabNet')` in `kali-network-settings.png`. Both VMs must remain locked to `LabNet` under snapshot `w1-network-verified` prior to Week 2 testing.
4. **OBS-M3-04 (Mounted Unattended Provisioning ISO):** `windows11-lab` currently has `Unattended-...-aux-iso.viso` mounted on SATA Port 1. Unattended installation media should be unmounted and inspected so no plaintext setup scripts remain accessible to standard users.
