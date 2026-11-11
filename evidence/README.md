# Week 1 Evidence Index

Project: Windows Exploitation & Privilege Escalation Lab
Evidence captured: 18–31 October 2026
Documentation status reviewed: 11 November 2026

This index maps the screenshots currently in the repository and notes material verification limits. Screenshots document the observed state at capture time; they do not by themselves establish complete isolation.

## Evidence files

| ID | Evidence | Files |
| --- | --- | --- |
| E01 | Windows VM configuration | [`screenshots/E01/windows VM config 1.png`](screenshots/E01/windows%20VM%20config%201.png), [`screenshots/E01/windows VM config 2.png`](screenshots/E01/windows%20VM%20config%202.png) |
| E02 | Kali VM configuration | [`screenshots/E02/Kali VM Config 1.png`](screenshots/E02/Kali%20VM%20Config%201.png), [`screenshots/E02/Kali VM Config 2.png`](screenshots/E02/Kali%20VM%20Config%202.png) |
| E03 | Windows Adapter 1 settings | [`screenshots/E03/windows-network-settings.png`](screenshots/E03/windows-network-settings.png) |
| E04 | Kali Adapter 1 settings | [`screenshots/E04/kali-network-settings.png`](screenshots/E04/kali-network-settings.png) |
| E05 | Windows IP configuration | [`screenshots/E05/windows-ip-config.png`](screenshots/E05/windows-ip-config.png) |
| E06 | Kali IP configuration | [`screenshots/E06/kali-ip-config.png`](screenshots/E06/kali-ip-config.png) |
| E07 | Windows-to-Kali ping | [`screenshots/E07/ping-windows-to-kali.png`](screenshots/E07/ping-windows-to-kali.png) |
| E08 | Kali-to-Windows ping | [`screenshots/E08/ping-kali-to-windows.jpeg`](screenshots/E08/ping-kali-to-windows.jpeg) |
| E09 | Windows VirtualBox Adapters 1–4; Adapter 1 uses LabNet, Adapters 2–4 disabled | [`screenshots/E09/windows-adapter-1-labnet.png`](screenshots/E09/windows-adapter-1-labnet.png), [`screenshots/E09/windows-adapter-2-disabled.png`](screenshots/E09/windows-adapter-2-disabled.png), [`screenshots/E09/windows-adapter-3-disabled.png`](screenshots/E09/windows-adapter-3-disabled.png), [`screenshots/E09/windows-adapter-4-disabled.png`](screenshots/E09/windows-adapter-4-disabled.png) |
| E10 | Kali VirtualBox Adapters 1–4; Adapter 1 uses LabNet, Adapters 2–4 disabled | [`screenshots/E10/kali-adapter-1-labnet.png`](screenshots/E10/kali-adapter-1-labnet.png), [`screenshots/E10/kali-adapter-2-disabled.png`](screenshots/E10/kali-adapter-2-disabled.png), [`screenshots/E10/kali-adapter-3-disabled.png`](screenshots/E10/kali-adapter-3-disabled.png), [`screenshots/E10/kali-adapter-4-disabled.png`](screenshots/E10/kali-adapter-4-disabled.png) |
| E11 | Windows IPv4 configuration and IPv4 routes | [`screenshots/E11/windows-ipconfig-all.jpeg`](screenshots/E11/windows-ipconfig-all.jpeg), [`screenshots/E11/windows-route-print.jpeg`](screenshots/E11/windows-route-print.jpeg) |
| E12 | Kali IPv4 address and connected route after restart | [`screenshots/E12/kali-ipv4-and-route-after-restart.jpg`](screenshots/E12/kali-ipv4-and-route-after-restart.jpg) |
| E13 | Windows and Kali snapshot lists and details | [`screenshots/E13/windows-snapshot-list.png`](screenshots/E13/windows-snapshot-list.png), [`screenshots/E13/windows-snapshot-details.png`](screenshots/E13/windows-snapshot-details.png), [`screenshots/E13/kali-snapshot-list.png`](screenshots/E13/kali-snapshot-list.png), [`screenshots/E13/kali-snapshot-details.png`](screenshots/E13/kali-snapshot-details.png) |
| E14 | Windows version/build and Kali release/kernel | [`screenshots/E14/windows-version.jpeg`](screenshots/E14/windows-version.jpeg), [`screenshots/E14/kali-version-and-kernel.jpeg`](screenshots/E14/kali-version-and-kernel.jpeg) |
| E15 | Windows Defender and firewall status | [`screenshots/E15/windows-defender-status.jpeg`](screenshots/E15/windows-defender-status.jpeg), [`screenshots/E15/windows-defender-settings.jpeg`](screenshots/E15/windows-defender-settings.jpeg), [`screenshots/E15/windows-firewall-status.jpeg`](screenshots/E15/windows-firewall-status.jpeg) |
| E16 | Kali IPv4 address after restart, supporting persistence | [`screenshots/E16/kali-ip-after-restart.jpeg`](screenshots/E16/kali-ip-after-restart.jpeg) |

## Review findings and open items

- E09–E10 show Adapter 1 attached to Internal Network `LabNet`; Adapters 2–4 are disabled on both VMs.
- E11 shows Windows `10.10.10.20/24` and no IPv4 default gateway. It lists three DNS values in the deprecated IPv6 site-local range `fec0::/10` (`fec0:0:0:ffff::1%1`, `::2%1`, and `::3%1`). Determine whether these are configured DNS servers or fallback values before claiming the DNS requirement is met. See the [IANA IPv6 address-space registry](https://www.iana.org/assignments/ipv6-address-space) for the range classification.
- E12 shows `10.10.10.10/24` and the connected `10.10.10.0/24` route on Kali after restart, with no default route. Resolver output is not shown; add it if DNS verification is to be evidenced in the repository.
- E13 confirms the named snapshots exist and shows a child snapshot named `w1-network-verified`. The Kali snapshot details image displays Adapter 1 as NAT, while E10 shows the current Adapter 1 as `LabNet`. Verify which Kali snapshot the details correspond to and ensure the recovery point used for the isolated lab does not restore NAT unintentionally.
- E14 records Windows 11 Pro Version 26H2, OS Build 26300.9457, and Kali 2026.2 with kernel `6.19.14+kali-amd64`.
- E15 shows no current threats and “No action needed” in Windows Security, security intelligence marked up to date, and firewall on for Domain, Private, and active Public profiles. It does not show Defender real-time protection. Windows Update was previously recorded in branch history as “Up to date,” but E15 does not show it; reconfirm and capture both current statuses.
- E16 supports the user-reported post-restart persistence of Kali `10.10.10.10/24`.
- The E13 VirtualBox detail images expose local VM paths containing the Windows account name. Redact or crop those paths before publishing the screenshots in a public repository.

## Evidence needed to close remaining items

- **E17 — Windows DNS configuration:** Capture the Ethernet adapter's IPv4 and IPv6 DNS settings and the Windows DNS client server list. This should establish whether the E11 `fec0::/10` values are configured or fallback values.
- **E18 — Kali resolver configuration:** Capture `resolvectl status` or `/etc/resolv.conf` after boot, alongside the `eth0` connection profile.
- **E19 — Kali snapshot selection:** In VirtualBox, select `kali-clean-install` and `w1-network-verified` separately and capture each selected snapshot's Adapter 1 attachment details. This will clarify which state shows NAT.
- **E20 — Windows Update:** Capture the current Windows Update status page.
- **E21 — Defender real-time protection:** Capture the specific real-time protection setting/status; E15's “No action needed” screen does not show that setting.
- **E22 — Host OS version:** Capture `winver` on the host Windows system, outside the guest VM.

Do not include passwords, tokens, private keys, VM disk images, or unrelated personal information. Update verification status only after the open items above are resolved or explicitly accepted and documented.
