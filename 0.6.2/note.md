
# Download OS ✔

# Create USB ✔

# Copy EFI folder ✔

# Gathering files

- Reminder:
SSDTs and custom DSDTs(.aml) go in ACPI folder
Kexts(.kext) go in Kexts folder
Firmware drivers(.efi) go in the Drivers folder

## Firmware Drivers

These files must be placed under `EFI/OC/Drivers/`
For the majority of systems, you'll only need 2 .efi drivers to get up and running:

* [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
Needed for seeing HFS volumes(ie. macOS Installers and Recovery partitions/images). Do not mix other HFS drivers
For Sandy Bridge and older(as well as low end Ivy Bridge(i3 and Celerons), see the legacy section below

* [OpenRuntime.efi](https://github.com/acidanthera/OpenCorePkg/releases)
Replacement for AptioMemoryFix.efi, used as an extension for OpenCore to help with patching boot.efi for NVRAM fixes and better memory management.

## Kexts

These files must be placed under `EFI/OC/Kexts/`. All kext listed below can be found pre-compiled in the [Kext Repo](http://kexts.goldfish64.com/). Kexts here are compiled each time there's a new commit.

Must haves:
Without the below 2, no system is bootable:

* VirtualSMC https://github.com/acidanthera/VirtualSMC/releases/latest
Emulates the SMC chip found on real macs, without this macOS will not boot
Alternative is FakeSMC which can have better or worse support, most commonly used on legacy hardware.
Requires OS X 10.6 or newer

* Lilu https://github.com/acidanthera/Lilu/releases/latest
A kext to patch many processes, required for AppleALC, WhateverGreen, VirtualSMC and many other kexts. Without Lilu, they will not work.
Note that Lilu and plugins requires OS X 10.8 or newer to function

## Graphics

* WhateverGreen https://github.com/acidanthera/WhateverGreen/releases
Used for graphics patching DRM, boardID, framebuffer fixes, etc, all GPUs benefit from this kext.

## Audio

* AppleALC https://github.com/acidanthera/AppleALC/releases
Used for AppleHDA patching, allowing support for the majority of on-board sound controllers

## Ethernet

* IntelMausi https://github.com/acidanthera/IntelMausi/releases
Required for the majority of Intel NICs, chipsets that are based off of I211 will need the SmallTreeIntel82576 kext
Intel's 82578, 82579, i217, i218 and i219 NICs are officially supported
Requires OS X 10.9 or newer, 10.8-10.8 users can use the IntelSnowMausi instead for older OSes

## USB

* USBInjectAll https://github.com/Sniki/OS-X-USB-Inject-All/releases
Used for injecting Intel USB controllers on systems without defined USB ports in ACPI

# SSDTs

* Tools:
https://github.com/acidanthera/MaciASL/releases/tag/1.5.8

https://github.com/corpnewt/SSDTTime

* Steps:
    - Dump DSDT: https://dortania.github.io/Getting-Started-With-ACPI/Manual/dump.html#uefi-shell
    - Use SSDTTime generate SSDT files from dsdt.aml (dsdt.dat)