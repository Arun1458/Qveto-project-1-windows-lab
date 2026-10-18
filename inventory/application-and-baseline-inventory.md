# Week 1 Deliverable: Application & Baseline Configuration Inventory (M3)

## 1. Operating System & Patch State Baseline
| Target Hostname | OS Version & Build | Architecture | Installed Hotfixes (KB) | Patch Status |
|-----------------|--------------------|--------------|-------------------------|--------------|
| WIN-LAB-TARGET  | Windows 10/11 Pro  | x64          | Pending `wmic qfe` scan | Baseline     |

## 2. Installed Applications Inventory
| Application Name | Version | Vendor | Install Path | Service Account | Known CVE / Config Note |
|------------------|---------|--------|--------------|-----------------|-------------------------|
| Approved Lab App | TBD     | TBD    | `C:\Program Files\...` | LocalSystem | Check service binary ACLs |

## 3. Baseline Security Settings & Privileges
* **Windows Defender Status:** Real-time protection state to be recorded prior to testing.
* **UAC Configuration:** `ConsentPromptBehaviorAdmin` registry value baseline.
* **Service Path Hygiene:** Check for unquoted service paths with spaces running as `SYSTEM`.
* **Folder/Registry Permissions:** Check `icacls` on non-default service directories and `AlwaysInstallElevated` registry keys.
* **Telemetry Readiness:** Confirm Event Viewer, Sysmon, and Process Monitor logging with M5.
