M-VAVE FM-1 MultiBoot – Architecture

1. Project Objective

MultiBoot aims to provide an on-device firmware manager for the M-VAVE FM-1.

The user should be able to store multiple firmware versions on a microSD card, select one directly on the device and switch firmware without connecting a PC.

2. Core Principle

The most important requirement is a permanently available bootloader.

The bootloader must remain intact when the user switches between firmware versions.

Normal firmware switching must never overwrite the protected bootloader area.

3. Proposed System Components

A. Permanent Bootloader

Based on the existing m-bootloader project.

Responsibilities:

* Start the device.
* Provide recovery functionality.
* Load the MultiBoot menu.
* Protect the bootloader area.

B. MultiBoot Manager

A menu application loaded from microSD.

Responsibilities:

* Detect available firmware packages.
* Display firmware names and versions.
* Allow the user to select a firmware.
* Check package integrity.
* Start the installation process.

C. microSD Storage

The microSD card will contain:

* Firmware packages.
* Firmware information files.
* Optional menu application.
* Configuration data.

Proposed directory structure:

/MBOOT/
MENU.BIN
/FIRMWARES/
firmware_01/
firmware_02/
firmware_03/

D. Firmware Installer

The installer is a planned component.

Responsibilities:

* Identify the selected firmware.
* Verify its format and compatibility.
* Back up relevant flash data.
* Install the firmware into the correct internal flash region.
* Verify the written data.
* Restart the device.

This functionality has not yet been implemented.

4. Proposed Boot Sequence

1. Device is switched on.
2. Permanent bootloader starts.
3. Bootloader checks for the MultiBoot menu.
4. MultiBoot menu is loaded from microSD.
5. User selects a firmware.
6. Firmware package is checked.
7. Installation is performed in internal flash.
8. Device restarts with the selected firmware.

5. Important Technical Limitation

The existing m-bootloader can load a secondary program from microSD.

This does not prove that complete FM-1 firmware images can execute directly from microSD.

The initial architecture therefore assumes that selected firmware must be installed into internal flash.

6. Safety and Recovery

The following requirements are mandatory:

* Protect the permanent bootloader.
* Never flash an unverified firmware package.
* Verify the flash layout before writing.
* Provide recovery after interrupted installation.
* Preserve a complete backup before modifying internal flash.
* Do not perform destructive operations without a verified recovery procedure.

7. Current Development Status

Current phase: Architecture and research.

Implemented:

* Project repository.
* Initial technical research.
* Bootloader research.
* Proposed architecture.

Not yet implemented:

* MultiBoot menu.
* Firmware package format.
* Firmware installer.
* Flash protection mechanism.
* Recovery testing.

8. Next Milestone

Develop a read-only microSD proof of concept.

The first prototype should:

1. Detect the microSD card.
2. Read the directory.
3. Find firmware package folders.
4. Read firmware information.
5. Display available firmware versions.

No internal flash writing will be performed in this milestone.

9. References

* https://github.com/jvitkauskas/m-bootloader
* https://github.com/jvitkauskas/m-card
* https://github.com/jvitkauskas/m-flasher
* https://sbegueria.github.io/fm1-dev-wiki/