Technical Research – M-VAVE FM-1 MultiBoot

1. Objective

Develop an on-device firmware manager for the M-VAVE FM-1.

The user should be able to select and switch between multiple firmware versions stored on a microSD card without requiring a PC during normal operation.

2. Target Hardware

* Device: M-VAVE FM-1
* SoC: JieLi AC791N (WL82 family)
* CPU: pi32v2, 32-bit
* Internal storage: 1 MiB SPI NOR flash
* Firmware execution: XIP (Execute In Place)
* Display: 240 × 240 TFT

3. Existing Projects

m-bootloader

An existing open-source bootloader for the FM-1.

Relevant capabilities:

* Recovery menu
* Firmware integrity checks
* USB recovery mode
* microSD support with an m-card hardware modification
* Loading and executing /MBOOT/MENU.BIN

Important distinction:

The SD-card feature loads a second-stage menu program. It does not establish that complete firmware images can execute directly from the SD card.

m-card

A proposed microSD expansion board.

* Connects through the LCD connector J12.
* Shares the LCD SPI bus.
* Uses a microSD socket.
* Designed without soldering to the FM-1 mainboard.

Status: Untested prototype.

4. Internal Flash Layout

The documented stock layout is:

Address range	Purpose
0x00000–0x03FFF	Boot area
0x04000–0x92FFF	Firmware application
0x93000–0xE8FFF	VM storage
0xE9000–0xE9FFF	Bluetooth data
0xEA000–0xFBFFF	User resources
0xFF000–0xFFFFF	Reserved area

This layout must be verified against the actual device before any write operation.

5. Proposed MultiBoot Architecture

1. A persistent bootloader remains in internal flash.
2. A firmware selection menu is loaded.
3. Firmware packages are stored on microSD.
4. The user selects a firmware.
5. The selected firmware is checked for compatibility and integrity.
6. The firmware is installed into the appropriate internal flash area.
7. The device restarts using the selected firmware.

The bootloader must never be overwritten during normal firmware switching.

6. Important Technical Questions

* Can the existing m-bootloader safely support firmware selection?
* Can the SD-card menu read and identify multiple firmware packages?
* Which firmware package formats must be supported?
* How can the bootloader area be protected?
* How can interrupted installations be recovered?
* How do different flash chip variants affect compatibility?
* How can firmware settings be preserved when switching versions?

7. Safety Requirements

* Never modify the device before a complete flash backup exists.
* Never assume that all FM-1 devices have identical flash chips.
* Verify firmware packages before installation.
* Never overwrite the bootloader during normal switching.
* Provide a recovery path before enabling firmware installation.

8. Current Status

Research phase.

No hardware modifications or firmware flashing have been performed.

9. Reference Projects

* m-bootloader
* m-card
* m-flasher
* FM-1 Firmware Developers’ Wiki

10. Next Development Milestone

Build a read-only proof of concept:

* Detect the microSD card.
* Read its directory.
* List available firmware files.
* Display firmware names in a menu.

No internal flash writing at this stage.