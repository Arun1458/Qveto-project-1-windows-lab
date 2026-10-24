# Week 1 Technical Report: Virtualization and Network Isolation

**Project:** Windows Exploitation & Privilege Escalation Lab
**Prepared by:** dhruv-sain-hub
**Date:** 18 October 2026
**Virtualization platform:** Oracle VirtualBox 7.2.20

## 1. Objective

Establish a controlled virtual lab using Windows 11 and Kali Linux, configure an isolated virtual network, verify connectivity between the VMs, and document the environment for future authorized exercises.

## 2. Scope

This report covers:

- Virtual machine configuration and resource allocation.
- VirtualBox Internal Network configuration.
- IPv4 addressing.
- Bidirectional ICMP connectivity testing.
- Snapshot inventory.
- Isolation requirements and supporting evidence.

Exploitation and privilege escalation exercises are outside the scope of Week 1.

## 3. Virtualization Environment

| Property                 | Recorded value                 |
| ------------------------ | ------------------------------ |
| Virtualization software  | Oracle VirtualBox 7.2.20       |
| Host operating system    | Windows; windows 11 (64bit)    |
| Target operating system  | Windows 11                     |
| Testing operating system | Kali Linux                     |
| Network type             | Internal Network               |
| Network name             | LabNet                         |

## 4. Virtual Machine Configuration

### 4.1 Windows 11

| Property              | Value                     |
| --------------------- | ------------------------- |
| VM name               | windows11-lab             |
| CPU allocation        | 3 vCPUs                   |
| RAM                   | 4096 MB                   |
| Virtual disk capacity | 80.00 GB                  |
| IPv4 address          | 10.10.10.20/24            |
| Network adapter       | Adapter 1                 |
| Network attachment    | Internal Network — LabNet |
| Snapshot              | windows11-clean-install   |

### 4.2 Kali Linux

| Property              | Value                              |
| --------------------- | ---------------------------------- |
| VM name               | kali-linux-2026.2-virtualbox-amd64 |
| CPU allocation        | 2 vCPUs                            |
| RAM                   | 2048 MB                            |
| Virtual disk capacity | 80.09 GB                           |
| Network interface     | eth0                               |
| IPv4 address          | 10.10.10.10/24                     |
| Network attachment    | Internal Network — LabNet          |
| Snapshot              | kali-clean-install                 |

## 5. Network Design

The lab uses the IPv4 subnet `10.10.10.0/24`.

- Windows 11: `10.10.10.20/24`
- Kali Linux: `10.10.10.10/24`
- Intended default gateway: none
- Intended DNS server: none
- DHCP: not configured

Both VMs use the same named VirtualBox Internal Network. The design is intended to allow communication between the lab VMs without using Bridged networking.

### Logical architecture

```text
             Host Computer
          Windows Operating System
                    |
              VirtualBox
                    |
      Internal Network: LabNet
             10.10.10.0/24
                    |
             +------+------+
             |             |
       Windows 11 VM    Kali Linux VM
       10.10.10.20      10.10.10.10
       Lab target       Testing system
```

## 6. Connectivity Validation

### Test A: Windows to Kali

- Source: `10.10.10.20`
- Destination: `10.10.10.10`
- Command: `ping 10.10.10.10`
- Result: Successful
- Packet loss: 0%

### Test B: Kali to Windows

- Source: `10.10.10.10`
- Destination: `10.10.10.20`
- Command: `ping -c 4 10.10.10.20`
- Initial result: 100% packet loss
- Corrective action: Enabled the relevant Windows inbound ICMPv4 Echo Request rule.
- Final result: Successful
- Packet loss: 0%

## 7. Snapshot and Recovery

The following snapshot names have been recorded:

- Windows: `windows11-clean-install`
- Kali: `kali-clean-install`

These snapshots are intended to preserve baseline states for recovery. Verify their availability in VirtualBox before making significant changes.

## 8. Isolation Requirements

- Keep both lab VMs attached to Internal Network `LabNet`.
- Do not use Bridged networking for this lab.
- Do not enable additional adapters without reviewing the impact.
- Leave the lab interfaces without a default gateway or DNS server unless the approved design changes.
- Review all enabled adapters and routing settings.
- Keep Windows Firewall enabled.
- Do not treat successful ping tests as proof of complete isolation.

## 9. Evidence

Supporting evidence should include VM settings, network adapter settings, IP configuration, successful ping results, and snapshot listings.

See `evidence/README.md` for the evidence checklist.

## 11. Conclusion

The Windows and Kali VMs have been configured on the same VirtualBox Internal Network and successfully exchanged ICMP echo traffic in both directions. The relevant Windows inbound ping rule was enabled to allow the reverse test.

The lab is ready for the remaining Week 1 verification and documentation tasks. Further exercises should begin only after the isolation review and baseline checks are complete.

End of report.
