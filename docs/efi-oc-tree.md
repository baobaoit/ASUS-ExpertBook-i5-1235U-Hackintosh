# OpenCore directory baseline

## Snapshot

Captured from `/Volumes/NO NAME/EFI/OC` on 2026-11-23. The tree records 156 files and 122 directories under `EFI/OC/`. It records paths only and omits macOS Finder and AppleDouble metadata such as `.DS_Store` and `._*`. The root `config.plist` appears by filename only.

## Expected differences

- `Kexts/AppleALC.kext/` and `Kexts/SimpleHDA.kext/` and their contents are present on the internal EFI. The repository omits these bundles.
- `Tools/` is empty in this snapshot. A fresh Git checkout may omit it.

## Full directory tree

```text
EFI/OC/
├── .contentFlavour
├── .contentVisibility
├── ACPI/
│   ├── SSDT-ALS0.aml
│   ├── SSDT-EC.aml
│   ├── SSDT-GPI0.aml
│   ├── SSDT-MCHC.aml
│   ├── SSDT-PLUG-ALT.aml
│   ├── SSDT-PNLF.aml
│   ├── SSDT-RTCAWAC.aml
│   ├── SSDT-SBUS.aml
│   ├── SSDT-USB-Reset.aml
│   ├── SSDT-USBX.aml
│   └── SSDT-XOSI.aml
├── Drivers/
│   ├── HfsPlus.efi
│   ├── OpenCanopy.efi
│   ├── OpenLinuxBoot.efi
│   ├── OpenRuntime.efi
│   ├── Ps2KeyboardDxe.efi
│   ├── ResetNvramEntry.efi
│   ├── apfs_aligned.efi
│   └── ext4_x64.efi
├── Kexts/
│   ├── AMFIPass.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       ├── MacOS/
│   │       │   └── AMFIPass
│   │       └── _CodeSignature/
│   │           └── CodeResources
│   ├── AppleALC.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── AppleALC
│   ├── AsusSMC.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── AsusSMC
│   ├── BTLEAdvFixup.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── BTLEAdvFixup
│   ├── BlueToolFixup.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── BlueToolFixup
│   ├── BrightnessKeys.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── BrightnessKeys
│   ├── CpuTopologyRebuild.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── CpuTopologyRebuild
│   ├── ForbiddenItlwm.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── ForbiddenItlwm
│   ├── ForgedInvariant.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── ForgedInvariant
│   ├── IntelBluetoothFirmware.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── IntelBluetoothFirmware
│   ├── IntelMausiEthernet.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       ├── MacOS/
│   │       │   └── IntelMausiEthernet
│   │       └── _CodeSignature/
│   │           └── CodeResources
│   ├── Lilu.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── Lilu
│   ├── NVMeFix.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── NVMeFix
│   ├── RestrictEvents.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── RestrictEvents
│   ├── SMCBatteryManager.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       ├── MacOS/
│   │       │   └── SMCBatteryManager
│   │       └── Resources/
│   │           └── SSDT-BATC.dsl
│   ├── SMCLightSensor.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── SMCLightSensor
│   ├── SMCProcessor.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── SMCProcessor
│   ├── SMCSuperIO.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── SMCSuperIO
│   ├── SimpleHDA.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── SimpleHDA
│   ├── USBToolBox.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── USBToolBox
│   ├── UTBDefault.kext/
│   │   └── Contents/
│   │       └── Info.plist
│   ├── UTBMap.kext/
│   │   └── Contents/
│   │       └── Info.plist
│   ├── VirtualSMC.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── VirtualSMC
│   ├── VoodooI2C.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       ├── MacOS/
│   │       │   └── VoodooI2C
│   │       └── PlugIns/
│   │           ├── VoodooGPIO.kext/
│   │           │   └── Contents/
│   │           │       ├── Info.plist
│   │           │       ├── MacOS/
│   │           │       │   └── VoodooGPIO
│   │           │       └── _CodeSignature/
│   │           │           └── CodeResources
│   │           ├── VoodooI2CServices.kext/
│   │           │   └── Contents/
│   │           │       ├── Info.plist
│   │           │       ├── MacOS/
│   │           │       │   └── VoodooI2CServices
│   │           │       └── _CodeSignature/
│   │           │           └── CodeResources
│   │           └── VoodooInput.kext/
│   │               └── Contents/
│   │                   ├── Info.plist
│   │                   ├── MacOS/
│   │                   │   └── VoodooInput
│   │                   └── _CodeSignature/
│   │                       └── CodeResources
│   ├── VoodooI2CHID.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       ├── MacOS/
│   │       │   └── VoodooI2CHID
│   │       └── _CodeSignature/
│   │           └── CodeResources
│   ├── VoodooPS2Controller.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       ├── MacOS/
│   │       │   └── VoodooPS2Controller
│   │       └── PlugIns/
│   │           ├── VoodooInput.kext/
│   │           │   └── Contents/
│   │           │       ├── Info.plist
│   │           │       ├── MacOS/
│   │           │       │   └── VoodooInput
│   │           │       └── _CodeSignature/
│   │           │           └── CodeResources
│   │           ├── VoodooPS2Keyboard.kext/
│   │           │   └── Contents/
│   │           │       ├── Info.plist
│   │           │       └── MacOS/
│   │           │           └── VoodooPS2Keyboard
│   │           ├── VoodooPS2Mouse.kext/
│   │           │   └── Contents/
│   │           │       ├── Info.plist
│   │           │       └── MacOS/
│   │           │           └── VoodooPS2Mouse
│   │           └── VoodooPS2Trackpad.kext/
│   │               └── Contents/
│   │                   ├── Info.plist
│   │                   └── MacOS/
│   │                       └── VoodooPS2Trackpad
│   ├── WhateverXe.kext/
│   │   └── Contents/
│   │       ├── Info.plist
│   │       └── MacOS/
│   │           └── WhateverXe
│   └── XHCI-unsupported.kext/
│       └── Contents/
│           └── Info.plist
├── OpenCore.efi
├── Resources/
│   ├── Font/
│   │   ├── Font_1x.bin
│   │   ├── Font_1x.png
│   │   ├── Font_2x.bin
│   │   ├── Font_2x.png
│   │   ├── Terminus.hex
│   │   └── TerminusCore.hex
│   ├── Image/
│   │   └── Acidanthera/
│   │       └── GoldenGate/
│   │           ├── AppleRecv.icns
│   │           ├── AppleTM.icns
│   │           ├── Background.icns
│   │           ├── BtnFocus.icns
│   │           ├── Cursor.icns
│   │           ├── Dot.icns
│   │           ├── Enter.icns
│   │           ├── ExtAppleRecv.icns
│   │           ├── ExtAppleTM.icns
│   │           ├── ExtHardDrive.icns
│   │           ├── FirmwareSettings.icns
│   │           ├── HardDrive.icns
│   │           ├── Left.icns
│   │           ├── Lock.icns
│   │           ├── NetworkBoot.icns
│   │           ├── OpticalDrive.icns
│   │           ├── Password.icns
│   │           ├── Restart.icns
│   │           ├── Right.icns
│   │           ├── Selected.icns
│   │           ├── Selector.icns
│   │           ├── SetDefault.icns
│   │           ├── Shell.icns
│   │           ├── ShutDown.icns
│   │           ├── Tool.icns
│   │           └── Windows.icns
│   └── Label/
│       ├── Apple.l2x
│       ├── Apple.lbl
│       ├── AppleRecv.l2x
│       ├── AppleRecv.lbl
│       ├── AppleTM.l2x
│       ├── AppleTM.lbl
│       ├── EFIBoot.l2x
│       ├── EFIBoot.lbl
│       ├── FirmwareSettings.l2x
│       ├── FirmwareSettings.lbl
│       ├── NetworkBoot.l2x
│       ├── NetworkBoot.lbl
│       ├── Other.l2x
│       ├── Other.lbl
│       ├── ResetNVRAM.l2x
│       ├── ResetNVRAM.lbl
│       ├── SIPDisabled.l2x
│       ├── SIPDisabled.lbl
│       ├── SIPEnabled.l2x
│       ├── SIPEnabled.lbl
│       ├── Shell.l2x
│       ├── Shell.lbl
│       ├── Tool.l2x
│       ├── Tool.lbl
│       ├── Windows.l2x
│       └── Windows.lbl
├── Tools/
└── config.plist
```

## Verification and updates

1. Enumerate actual entries under the `EFI/OC/` being verified. Compare relative paths, file and directory types, and exact capitalization at every depth, including `Contents/PlugIns/` directories. Apply the listed expected differences when checking the repository.
2. After copying or moving components, repeat the comparison on the destination. Verify that each enabled `Kernel → Add` entry matches the exact on-disk `BundlePath`, `PlistPath`, and any `ExecutablePath`.
3. Report unexpected missing, extra, or misnamed paths. Refresh this snapshot only for intentional layout changes after verifying the new tree against the intended source.
