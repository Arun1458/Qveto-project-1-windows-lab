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

E09–E10 show both VMs using the VirtualBox Internal Network named `LabNet` on Adapter 1, with Adapters 2–4 disabled. Kali's address is persistent after restart (E12, E16). Some network and recovery checks remain open, as summarized below.

Kali's lab IP address was initially assigned manually, then configured in its NetworkManager profile. E12 and E16 show `10.10.10.10/24` after restart.

## Repository Structure

- `docs/baseline-checklist.txt` — Week 1 task tracking and completion status
- `docs/lab-design.txt` — Lab architecture and network design
- `docs/rules-of-engagement.txt` — Authorized scope and safety rules
- `docs/vm-inventory.txt` — VM resources and configuration
- `docs/network-validation.txt` — Connectivity tests and results
- `docs/change-log.txt` — Configuration changes and troubleshooting history
- `docs/week1-virtualization-network-isolation.md` — Week 1 setup report
- `evidence/README.md` — Evidence index, review findings, and open evidence items
- `evidence/screenshots/` — VM, adapter, IP configuration, and connectivity screenshots

## Network Configuration and Isolation

The lab network uses a VirtualBox Internal Network named `LabNet` with the intended subnet `10.10.10.0/24`.

| Machine    | Interface address | Subnet mask     |
| ---------- | ----------------- | --------------- |
| Windows 11 | `10.10.10.20/24`  | `255.255.255.0` |
| Kali Linux | `10.10.10.10/24`  | `255.255.255.0` |

The intended configuration has no default gateway or DNS server on the lab interfaces. E11 shows no IPv4 default gateway on Windows, but lists three DNS values in deprecated IPv6 site-local range `fec0::/10`; their configured or fallback status needs clarification. E12 shows Kali's persistent address and connected subnet route with no default route; resolver output is still needed.

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

### Pending verification

- Determine whether Windows' `fec0::/10` DNS entries are configured or fallback values; capture Kali resolver details (E17–E18).
- Reconcile the Kali snapshot details showing Adapter 1 as NAT with the current `LabNet` configuration before relying on that snapshot for recovery (E19).
- Reconfirm Windows Update and Defender real-time protection status; capture supporting evidence (E20–E21).
- Record the host OS version/build (E22).

## Evidence

See [`evidence/README.md`](evidence/README.md) for the screenshots currently committed and the remaining evidence needed to close verification gaps. Remove personal or sensitive information before sharing screenshots.

## Safety and Rules of Engagement

- Only the Windows and Kali VMs explicitly included in this lab are authorized targets.
- Do not test external systems, public IP addresses, or third-party infrastructure.
- Keep the lab isolated from regular host and external networks unless a separately documented, authorized configuration requires otherwise.
- Keep Windows Firewall enabled and make only necessary, documented rule changes.
- Do not upload VM disk images, ISO files, passwords, private keys, access tokens, or other sensitive information to the repository.
- Use recovery snapshots before future exercises that could modify the target environment.
- Document configuration changes and restore the baseline when an exercise is complete.

---

**Documentation status reviewed (11 November 2026):** The repository includes screenshots documenting successful bidirectional ping tests, all VM adapter states, the guest OS versions, named snapshots, Kali's post-restart address, and parts of the Windows security status. Review findings and open items are tracked in [`evidence/README.md`](evidence/README.md) and the baseline checklist. Windows output lists DNS values in deprecated IPv6 site-local space whose active/configured status remains to be checked; Kali snapshot details show NAT while the current VM adapter is on LabNet. Complete isolation has not been confirmed. This Week 1 branch documents setup and connectivity; future controlled security exercises are outside its completed scope. Evidence was captured between 18 and 31 October 2026.
