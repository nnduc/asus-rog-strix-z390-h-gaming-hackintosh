# Done

[x] Download OS
[x] Create USB
[x] Copy EFI folder
    - EFI/OC/Drivers: Keep `OpenRuntime.efi`, remove everything else.
    - EFI/OC/Tools: Keep `OpenShell.efi`

[x] Gathering files
    `SSDTs` and custom `DSDTs(.aml)` go in `ACPI` folder
    `Kexts(.kext)` go in `Kexts` folder
    `Firmware drivers(.efi)` go in the `Drivers` folder

    - Drivers
        [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
        [OpenRuntime.efi](https://github.com/acidanthera/OpenCorePkg/releases)

    - Kexts
        VirtualSMC https://github.com/acidanthera/VirtualSMC/releases/latest
        Lilu https://github.com/acidanthera/Lilu/releases/latest
        AppleALC https://github.com/acidanthera/AppleALC/releases
        IntelMausi https://github.com/acidanthera/IntelMausi/releases
        USBInjectAll https://github.com/Sniki/OS-X-USB-Inject-All/releases

    - SSDTs
        * Tools:
        https://github.com/acidanthera/MaciASL/releases/latest
        https://github.com/corpnewt/SSDTTime

        * Steps:
            - Dump DSDT: https://dortania.github.io/Getting-Started-With-ACPI/Manual/dump.html###uefi-shell
            - Use SSDTTime generate SSDT files from `dsdt.aml (dsdt.dat)` of the previous step
            - Add SSDT files to AHCI folder

[x] Creating your config.plist

    * Tools
    https://github.com/corpnewt/ProperTree
    https://github.com/corpnewt/GenSMBIOS

    * Steps:
        - Copy `Docs/Sample.plist` to `EFI/OC/config.plist`
        - Open `EFI/OC/config.plist` on ProperTree
        - After the config is opened, press Cmd/Ctrl + Shift + R and point it at your EFI/OC folder to perform a "Clean Snapshot"


[] Configuration

    Link: https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html###starting-point


[] Intel BIOS settings

    Note: Most of these options may not be present in your firmware, we recommend matching up as closely as possible but don't be too concerned if many of these options are not available in your BIOS

    - Disable
        Fast Boot
        Secure Boot
        Serial/COM Port
        Parallel Port
        VT-d (can be enabled if you set DisableIoMapper to YES)
        CSM
        Thunderbolt(For initial install, as Thunderbolt can cause issues if not setup correctly)
        Intel SGX
        Intel Platform Trust
        CFG Lock (MSR 0xE2 write protection)(This must be off, if you can't find the option then enable both AppleCpuPmCfgLock and AppleXcpmCfgLock under Kernel -> Quirks. Your hack will not boot with CFG-Lock enabled)

    - Enable
        VT-x
        Above 4G decoding
        Hyper-Threading
        Execute Disable Bit
        EHCI/XHCI Hand-off
        OS type: Windows 8.1/10 UEFI Mode
        DVMT Pre-Allocated(iGPU Memory): 64MB
        SATA Mode: AHCI