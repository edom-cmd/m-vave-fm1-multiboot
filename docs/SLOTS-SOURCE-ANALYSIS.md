Analysis of the Existing m-apps Slots Implementation

1. Source Repository

Project: m-apps
Developer: jvitkauskas
Source files:

* apps/slots/slots.c
* apps/slots/slotfile.c
* apps/slots/slotfile.h

Source repository: https://github.com/jvitkauskas/m-apps

2. Existing Functionality

The existing slots application implements:

* microSD card detection.
* Firmware slot listing.
* Saving the current flash contents to the card.
* Loading a selected firmware image.
* Deleting firmware slots.
* Firmware image validation.
* Progress display.
* Long-press confirmation before loading or deleting.

The application is designed to switch firmware without a computer.

3. Storage Format

The source code defines:

* Slot image size: 0x100000 bytes (1 MiB).
* Maximum number of slots: 40.
* Image file extension: .BIN.

The storage path is:

/MBOOT/SLOTS/<8 hexadecimal characters>/

Each firmware slot is stored as a separate BIN file.

A STATE.DAT file stores the active and pending slot names.

4. Flash Writing Strategy

The source code defines:

* FIRST = 0x4000
* END = 0xFF000
* Sector size = 0x1000

The loading process:

1. Validates the selected image.
2. Saves the current firmware when necessary.
3. Records the pending slot.
4. Compares the image with internal flash.
5. Erases and writes only where required.
6. Reads back written sectors and compares them.
7. Writes the first firmware sector last.
8. Updates the active slot state.

The code does not write the address range below 0x4000 or from 0xFF000 onward during the slot-loading loop.

Additional preserved sectors are selected by the kept() function for APP_BOARD == 2.

These address ranges and board-specific rules must be verified against the actual FM-1 hardware before use.

5. Interrupted Loading

The application records a pending slot before writing firmware.

If a previous load was interrupted, the application can detect the pending slot and display LAST LOAD STOPPED.

The source also marks the affected slot as STOPPED in the menu.

This is an interruption-detection mechanism. A complete recovery procedure still needs to be tested on the target hardware.

6. Important Safety Features

The source implements:

* Firmware validation before loading.
* Backup of the current flash contents.
* Read-back verification after writing.
* Long-press confirmation.
* A watchdog/guard mechanism during the loading process.
* Pending-slot tracking.

These mechanisms are valuable and should be preserved if we build on this project.

7. FM-1 Compatibility Status

The source code alone does not prove that the current application works correctly on every FM-1 hardware revision.

Before using its flash-writing functions, we must verify:

* Exact flash chip and capacity.
* Actual FM-1 flash layout.
* Bootloader and key storage boundaries.
* Correct APP_BOARD configuration.
* microSD hardware compatibility.
* Successful recovery after an interrupted load.

No destructive test should be performed before these checks.

8. MultiBoot Project Decision

The existing slots application is a strong candidate as the technical foundation for our project.

Preferred approach:

1. Understand and build the existing application.
2. Verify its hardware compatibility.
3. Preserve its existing safety mechanisms.
4. Develop our own MultiBoot interface if needed.
5. Test SD-card reading before any flash-writing operation.

9. Current Status

Source-code analysis: completed.

Hardware compatibility verification: pending.

Read-only SD-card test: pending.

Flash-writing tests: not started.

Recovery tests: not started.