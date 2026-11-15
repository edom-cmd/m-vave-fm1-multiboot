Contributing to M-VAVE FM-1 MultiBoot

Thank you for your interest in M-VAVE FM-1 MultiBoot!

MultiBoot is an open-source research and development project exploring a way to store multiple firmware versions on a microSD card, select one directly on the FM-1, and switch firmware without connecting a computer during normal use.

The project is in an early research phase. Contributions of all sizes are welcome — including technical research, documentation, code, hardware testing, and careful review.

Project goals

* Store multiple firmware images on a microSD card.
* Select a firmware directly on the FM-1.
* Switch firmware without a computer during normal operation.
* Keep a recovery-capable bootloader available.
* Check firmware images before attempting an installation.
* Recover safely from an interrupted or unsuccessful installation.

The architecture is still a proposal. Some assumptions and hardware details require further verification.

Current status

The repository currently contains initial technical research, bootloader research, a proposed architecture, and an analysis of the existing slots application.

Related community projects:

* m-bootloader
* m-card
* m-apps
* m-flasher

These projects are useful references, not proof that the complete MultiBoot concept is already implemented or validated.

Ways to contribute

Technical research

Investigate hardware revisions, flash-chip variants, memory layout, firmware formats, compatibility checks, and recovery options. Include sources and evidence wherever possible.

Software development

Potential tasks include:

* Read-only SD-card browser.
* Firmware file discovery and metadata parsing.
* On-device firmware selection menu.
* Firmware package validation.
* Cross-platform build and test workflow.
* Automated tests for parsing, selection, and failure handling.

Hardware testing

FM-1 owners with compatible SD-card hardware can help verify card detection, menu behavior, hardware differences, and recovery procedures.

Please document the exact device revision, flash-chip identifier where available, hardware modifications, software versions, and test procedure.

Documentation and review

Documentation improvements, source-code reviews, issue reports, corrections, and beginner-friendly explanations are all valuable.

First milestone: read-only SD-card proof of concept

The first milestone is deliberately limited:

1. Detect a compatible microSD card.
2. Read its directory structure.
3. Find candidate firmware files or package folders.
4. Read available firmware metadata.
5. Display available entries in a simple menu.

This milestone must not erase, program, or otherwise modify internal flash.

Only after this works reliably should the project consider a separate firmware installation design.

Safety requirements

* Do not write to internal flash during the initial read-only milestone.
* Do not assume all FM-1 units have the same flash chip or memory layout.
* Do not overwrite the bootloader during normal firmware switching.
* Verify the flash layout and recovery procedure before installation.
* Require a suitable backup and tested recovery procedure before destructive operations.
* Verify firmware format, compatibility, and integrity before installation.
* Document test conditions and risks.

Experimental instructions must not be treated as safe for everyday devices.

How to contribute

1. Read the project README and research documents in docs/.
2. Search existing issues before opening a new one.
3. For bugs, include reproduction steps and expected versus actual results.
4. For research, include sources and explain what they demonstrate.
5. For code changes, describe how they were built and tested.
6. Open a pull request with a clear summary and relevant test results.

If you are unsure where to start, open an issue describing your area of interest. Discussion and review are welcome before implementation begins.

Reporting test results

Include as much of the following as possible:

* FM-1 hardware revision.
* Flash-chip identifier.
* SD-card expansion hardware and wiring.
* SD-card type and format.
* Bootloader and application versions.
* Exact test steps.
* Expected and observed results.
* Logs, photos, or other evidence where appropriate.

Never publish private information or device-specific secrets in logs.

Project status and expectations

MultiBoot is experimental and is not currently a validated firmware-switching solution. The proposed architecture, compatibility assumptions, and installation strategy may change as research and testing progress.

There are no guarantees that a particular firmware, hardware revision, or flash-chip variant will be supported.

Thank you for helping make the project safer, clearer, and more useful.