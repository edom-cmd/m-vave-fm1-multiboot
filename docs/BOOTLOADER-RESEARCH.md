Bootloader Research – M-VAVE FM-1 MultiBoot

1. Purpose

This document investigates the existing m-bootloader project as a possible foundation for MultiBoot.

Our goal is to develop an on-device firmware manager that allows users to select different firmware versions from a microSD card without connecting a PC during normal operation.

2. Existing Project

Project: m-bootloader
Developer: Julius Vitkauskas
Repository: https://github.com/jvitkauskas/m-bootloader

The project is an open-source bootloader for the M-VAVE FM-1 and related devices using the JieLi AC791N platform.

3. Existing Features

The project documentation and source overview describe these features:

* Boot menu and recovery functions.
* Firmware update support.
* USB MIDI update mode.
* Flash loader.
* Support for loading a second-stage program from a microSD card.
* Model-specific bootloader builds.

4. microSD Support

The source file src/sdboot.c implements functionality to:

1. Detect a microSD card.
2. Find the file /MBOOT/MENU.BIN.
3. Load the program from the card.
4. Run the loaded program.

This is particularly interesting for MultiBoot.

Important distinction:

MENU.BIN is a second-stage program. This does not mean that complete firmware images can run directly from the microSD card.

## 5. Current Bootloader Status

The current m-bootloader version is 2.4.

Repository:
https://github.com/jvitkauskas/m-bootloader

The release identifies the build as 2.4-395e6cc.

The bootloader has been tested on real FM-1 hardware.

It supports loading and executing a secondary program:

/MBOOT/MENU.BIN

from a FAT32 microSD card.

Important limitation:

The SD card hardware modification for the FM-1
has not yet been tested with this release.

The m-card expansion board is still an
untested prototype.

MultiBoot must independently verify SD hardware
compatibility before any installation or flashing.
6. Proposed MultiBoot Approach

The following is a proposal, not an implemented feature:

1. Keep the bootloader in protected internal flash.
2. Load a firmware manager from microSD.
3. Display available firmware versions.
4. Let the user select a firmware.
5. Check the selected firmware package.
6. Install it into the correct internal flash region.
7. Restart the device.

7. Open Technical Questions

* Can the existing SD menu be extended for firmware selection?
* Which firmware package formats are supported?
* How can the bootloader region be protected?
* How can interrupted installations be recovered?
* Can firmware settings be preserved when switching versions?
* Which microSD hardware modification is suitable?

8. Safety Requirements

* Do not write to internal flash before a complete backup exists.
* Do not overwrite the bootloader during normal firmware switching.
* Verify firmware compatibility before installation.
* Verify every flash write.
* Develop and test a recovery procedure before enabling installation.

9. Current Project Status

Research phase.

No hardware modifications or firmware flashing have been performed.

The existing bootloader is a promising starting point, but MultiBoot firmware installation and selection still need to be developed and tested.

10. References

* m-bootloader: https://github.com/jvitkauskas/m-bootloader
* m-card: https://github.com/jvitkauskas/m-card
* m-flasher: https://github.com/jvitkauskas/m-flasher
* FM-1 Developer Wiki: https://sbegueria.github.io/fm1-dev-wiki/