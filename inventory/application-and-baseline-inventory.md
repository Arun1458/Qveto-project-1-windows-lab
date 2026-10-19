# Week 1 Deliverable: VM & Baseline Configuration Inventory (M3)

## 1. Confirmed Virtual Machine Specifications (From Lab Setup)
* **VM Name:** `windows11-lab`
* **Operating System:** Windows 11 (64-bit)
* **Base Memory (RAM):** 4096 MB (4 GB)
* **Processors:** 3 vCPUs
* **Boot Order:** Hard Disk, Optical, Floppy
* **Platform Security Features:**
  * **TPM Type:** 2.0
  * **EFI:** Enabled
  * **Secure Boot:** Enabled
  * **Hardware Virtualization:** VT-x/AMD-V, Nested Paging, Hyper-V Paravirtualization
* **Distribution Method:** Standardized team `.ova` appliance image for reproducible assessment across all team roles.

## 2. Operating System & Patch State Baseline
| Target VM Name | OS Version & Build | Architecture | Installed Hotfixes (KB) | Patch Status |
|----------------|--------------------|--------------|-------------------------|--------------|
| `windows11-lab` | Windows 11 (64-bit) | x64 | Pending `.ova` import & `systeminfo` check | Baseline |

## 3. Baseline Security Settings & Audit Scope (M3)
* **Windows Defender Status:** Real-time protection and tamper protection baseline to be verified upon `.ova` import.
* **UAC Configuration:** `EnableLUA` and `ConsentPromptBehaviorAdmin` registry baseline.
* **Service Path Hygiene:** Audit non-default services for unquoted service paths running as `LocalSystem`.
* **Directory/Binary ACLs:** Inspect `icacls` permissions on third-party application directories.
