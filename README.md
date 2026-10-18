# Windows Exploitation & Privilege Escalation Lab

## Project Overview

This project establishes an isolated virtual cybersecurity lab for learning Windows security fundamentals, system enumeration, vulnerability assessment, and privilege escalation concepts.

All exercises are limited to the authorized virtual machines described in the project documentation.

## Objectives

- Set up Windows 11 and Kali Linux virtual machines.
- Establish an isolated virtual network.
- Record VM configurations and baseline security settings.
- Create and verify recovery snapshots.
- Document network validation and security controls.
- Prepare the environment for future controlled security exercises.

## Lab Environment

- Virtualization platform: Oracle VirtualBox 7.2.20
- Target operating system: Windows 11
- Testing operating system: Kali Linux
- Network type: Internal Network
- Network name: LabNet
- Subnet: 10.10.10.10/24

## Virtual Machine Addresses

| Machine    | IPv4 Address   | Role                     |
| ---------- | -------------- | ------------------------ |
| Windows 11 | 10.10.10.20/24 | Authorized lab target    |
| Kali Linux | 10.10.10.10/24 | Testing and verification |

## Repository Structure

- `docs/baseline-checklist.txt` — Week 1 task tracking
- `docs/lab-design.txt` — Lab architecture and network design
- `docs/rules-of-engagement.txt` — Authorized scope and safety rules
- `docs/vm-inventory.txt` — VM resources and configuration
- `docs/network-validation.txt` — Connectivity test results
- `docs/windows-security-baseline.txt` — Windows security status
- `docs/change-log.txt` — Configuration changes and troubleshooting
- `evidence/` — Sanitized screenshots and test evidence

## Network Isolation

Both VMs are configured to use the VirtualBox Internal Network named LabNet. The lab interfaces are intended to have no default gateway or DNS configuration.

The intended design restricts lab communication to the authorized virtual environment. The actual network configuration should be reviewed periodically.

## Week 1 Status

- Windows and Kali VMs created and booting.
- Lab network configured.
- Windows-to-Kali ping test successful.
- Kali-to-Windows ping test successful after enabling the relevant Windows inbound ICMPv4 Echo Request rule.
- VM snapshots recorded in the inventory.
- Remaining security baseline and documentation tasks tracked in the checklist.

## Safety

No external systems are authorized targets. Do not upload VM disk images, passwords, private keys, access tokens, or other sensitive information to the repository.

## Next Steps

- Complete Windows and Kali OS version records.
- Record Windows Defender, Firewall, and update status.
- Finish baseline evidence and documentation.
