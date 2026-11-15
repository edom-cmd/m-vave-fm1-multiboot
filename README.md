M-VAVE FM-1 MultiBoot

One device. Multiple firmwares. One permanent bootloader.

MultiBoot is an open-source development project exploring an on-device firmware manager for the M-VAVE FM-1.

The goal is to make it possible to store multiple firmware versions on a microSD card, select one directly on the device, and switch between them without connecting a computer.

Project Goals

* Store multiple firmware images on a microSD card.
* Select firmware directly on the FM-1.
* Switch firmware without using a PC during normal operation.
* Preserve a permanent bootloader.
* Provide a recovery mechanism if a firmware installation fails.
* Verify firmware images before installation.

Planned Architecture

The proposed architecture consists of:

1. Permanent Bootloader – remains protected in internal flash.
2. Firmware Manager – provides a firmware selection menu.
3. microSD Storage – stores firmware images and configuration files.
4. Firmware Installer – installs the selected firmware into internal flash.

This architecture is a proposal and still requires technical verification.

Hardware

Target device: M-VAVE FM-1
Target platform: JieLi AC791N / WL82 family
Storage concept: microSD expansion

Project Status

Early research and development

No firmware modifications or hardware changes have been made as part of this project yet.

Hardware compatibility, flash layout, SD-card communication and bootloader protection still need to be verified.

Safety

This project is experimental.

Flashing firmware can permanently damage the device if performed incorrectly. No firmware installation should be attempted until the flash layout and recovery procedure have been verified.

License

License not yet selected.