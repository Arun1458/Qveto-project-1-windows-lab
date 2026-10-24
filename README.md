# Windows Exploitation & Privilege Escalation Lab

## Project Overview

This project establishes an isolated virtual cybersecurity lab for learning Windows security fundamentals, system enumeration, vulnerability assessment, and privilege escalation concepts.

All exercises are limited to the authorized virtual machines described in this repository. The lab is intended for controlled learning and testing within the virtual environment.

## Objectives

- Set up Windows 11 and Kali Linux virtual machines.
- Configure an isolated VirtualBox Internal Network.
- Record VM configurations and baseline security settings.
- Create and verify recovery snapshots.
- Validate communication between the authorized lab VMs.
- Document network configuration, security controls, and troubleshooting.
- Prepare the environment for future controlled security exercises.

## Lab Environment

| Setting                  | Configuration            |
| ------------------------ | ------------------------ |
| Virtualization platform  | Oracle VirtualBox 7.2.20 |
| Target operating system  | Windows 11               |
| Testing operating system | Kali Linux               |
| Network type             | Internal Network         |
| Network name             | `LabNet`                 |
| Lab subnet               | `10.10.10.0/24`          |

## Virtual Machine Inventory

| Machine                                           | IPv4 Address     | Resources                                              | Role                     |
| ------------------------------------------------- | ---------------- | ------------------------------------------------------ | ------------------------ |
| Windows 11 (`windows11-lab`)                      | `10.10.10.20/24` | 3 vCPUs, 4096 MB RAM, 80 GB virtual disk               | Authorized lab target    |
| Kali Linux (`kali-linux-2026.2-virtualbox-amd64`) | `10.10.10.10/24` | 2 vCPUs, 2048 MB RAM, approximately 80 GB virtual disk | Testing and verification |

Both VMs are configured to use the VirtualBox Internal Network named `LabNet`.

Kali's lab IP address was assigned manually during setup.

## Repository Structure

- `docs/baseline-checklist.txt` — Week 1 task tracking and completion status
- `docs/lab-design.txt` — Lab architecture and network design
- `docs/rules-of-engagement.txt` — Authorized scope and safety rules
- `docs/vm-inventory.txt` — VM resources and configuration
- `docs/network-validation.txt` — Connectivity tests and results
- `docs/change-log.txt` — Configuration changes and troubleshooting history
- `docs/week1-virtualization-network-isolation.md` — Week 1 setup report
- `evidence/` — Sanitized screenshots and test evidence

## Network Configuration and Isolation

The lab network uses a VirtualBox Internal Network named `LabNet` with the intended subnet `10.10.10.0/24`.

| Machine    | Interface address | Subnet mask     |
| ---------- | ----------------- | --------------- |
| Windows 11 | `10.10.10.20/24`  | `255.255.255.0` |
| Kali Linux | `10.10.10.10/24`  | `255.255.255.0` |

The intended configuration has no default gateway or DNS server on the lab interfaces.

Both VMs have been configured to use `LabNet`, and connectivity between them has been tested successfully. A complete isolation review—including checking all VM adapters and routing configuration—remains necessary before claiming that the environment has been fully verified as isolated.

## Week 1 Progress

### Completed

- Created and booted the Windows 11 and Kali Linux virtual machines.
- Configured the VMs to use the VirtualBox Internal Network `LabNet`.
- Assigned the intended lab IPv4 addresses.
- Verified Windows-to-Kali ICMP connectivity.
- Verified Kali-to-Windows ICMP connectivity.
- Enabled the relevant Windows inbound ICMPv4 Echo Request rule to allow the Kali-to-Windows ping test. Windows Firewall remains enabled.
- Troubleshot the Windows link-local address issue (`169.254.x.x`) and configured the intended lab address.
- Recorded the intended VM snapshot names.

## Evidence

The `evidence/` directory should contain sanitized screenshots documenting the configuration and validation process.

Suggested evidence files:

- `windows-vm-settings.png`
- `kali-vm-settings.png`
- `windows-network-settings.png`
- `kali-network-settings.png`
- `windows-ipconfig.png`
- `kali-ip-config.png`
- `ping-windows-to-kali.png`
- `ping-kali-to-windows.png`

Only mark evidence as collected after the corresponding screenshot has been captured and checked.

## Safety and Rules of Engagement

- Only the Windows and Kali VMs explicitly included in this lab are authorized targets.
- Do not test external systems, public IP addresses, or third-party infrastructure.
- Keep the lab isolated from regular host and external networks unless a separately documented, authorized configuration requires otherwise.
- Keep Windows Firewall enabled and make only necessary, documented rule changes.
- Do not upload VM disk images, ISO files, passwords, private keys, access tokens, or other sensitive information to the repository.
- Use recovery snapshots before future exercises that could modify the target environment.
- Document configuration changes and restore the baseline when an exercise is complete.

---

**Current status:** Windows 11 and Kali Linux have been configured for the intended lab network, and bidirectional ICMP connectivity has been demonstrated. Final verification of all enabled network adapters, routing, gateway/DNS settings, and the Windows security baseline remains in progress.
