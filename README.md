# ASUS ExpertBook i5-1235U Hackintosh

OpenCore configuration for an ASUS ExpertBook with a 12th-generation Intel Core i5-1235U (Alder Lake-U). This repository contains the `EFI/OC` configuration and its bundled components. The standard UEFI fallback loader, `EFI/BOOT/BOOTx64.efi`, must be supplied separately for a standalone USB boot setup.

## Target hardware and configuration

| Item | Details |
| --- | --- |
| Laptop | ASUS ExpertBook. Exact model suffix and BIOS revision are undocumented. |
| CPU | Intel Core i5-1235U, 10 cores (2 performance, 8 efficiency), 12 threads |
| Integrated graphics | Intel Iris Xe-eligible graphics. The EFI enables WhateverXe 0.8.3. |
| OpenCore | Bundled as `EFI/OC/OpenCore.efi`. Exact release is unverified. |
| SMBIOS model | `MacBookPro16,2` |
| macOS | Tahoe (Darwin 25) is a configuration target, inferred from the minimum kernel version for ForbiddenItlwm and BTLEAdvFixup. Tested releases are undocumented. |

Processor specifications are from [Intel](https://www.intel.com/content/www/us/en/products/sku/226261/intel-core-i51235u-processor-12m-cache-up-to-4-40-ghz/specifications.html).

## Feature status

The table describes what the EFI enables and which device checks have been performed.

| Feature | Configuration and verification status |
| --- | --- |
| Graphics and brightness | WhateverXe and BrightnessKeys are enabled. Internal display output, brightness controls, and Metal acceleration are unverified. Check the matching [WhateverXe release instructions](https://github.com/b00t0x/WhateverXe/releases) for any macOS-side requirements. |
| Wi-Fi and Bluetooth | ForbiddenItlwm 0.6.0, IntelBluetoothFirmware, and BlueToolFixup are enabled. The wireless card model, connectivity, and Continuity features are unverified. |
| Ethernet | IntelMausiEthernet is enabled. The controller model and link behavior are unverified. |
| Keyboard and trackpad | VoodooPS2Keyboard and VoodooI2C/VoodooI2CHID are enabled. Input and gestures are unverified. |
| USB and battery | USBToolBox with UTBMap and SMCBatteryManager are enabled. Port mapping and battery reporting are unverified. |
| Audio | AppleALC 1.9.8 and SimpleHDA 1.0.2 are enabled for the Realtek ALC256 with `alcid=41`. The internal EFI completed a built-in speaker playback test on macOS Tahoe 26.7.3 (25G342). The internal microphone still needs a fix. |
| Webcam and sleep/wake | Test results are undocumented. |

## EFI layout

```text
EFI/
└── OC/
    ├── config.plist
    ├── OpenCore.efi
    ├── ACPI/
    ├── Drivers/
    ├── Kexts/
    └── Resources/
```

## Generate your SMBIOS identity

The repository leaves the four machine-specific fields blank. Make a private copy of `EFI/OC/config.plist` for your test EFI and add your own values there.

1. Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and open `GenSMBIOS.command` on macOS or `GenSMBIOS.bat` on Windows.
2. Choose option **1** to install or update MacSerial, then option **3** to generate one identity for `MacBookPro16,2`.
3. In your private copy, enter the generated values under `PlatformInfo → Generic`.

   | GenSMBIOS output | OpenCore field |
   | --- | --- |
   | Type | `SystemProductName` (already set to `MacBookPro16,2`) |
   | Serial | `SystemSerialNumber` |
   | Board Serial | `MLB` |
   | SmUUID | `SystemUUID` |

4. Set `ROM` to six bytes of plist **Data**. You can use your network adapter's MAC address by entering its 12 hexadecimal digits without separators in a plist editor. See [Dortania's PlatformInfo guide](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#platforminfo).

## Prepare and validate a test EFI

1. Back up your working EFI and use a separate USB for testing. Confirm your ExpertBook model and hardware before reusing its ACPI tables or USB map.
2. Identify the bundled OpenCore release before choosing the matching fallback loader and validator. Use the same release for the bootloader, its accompanying OpenCore drivers, and `ocvalidate`. See [OpenCorePkg releases](https://github.com/acidanthera/OpenCorePkg/releases).
3. Generate your SMBIOS identity as described above and add it to your test EFI's private configuration.
4. Run both checks from the repository root. The first checks plist syntax and the second checks OpenCore configuration compatibility.

   ```sh
   plutil -lint EFI/OC/config.plist
   /path/to/ocvalidate EFI/OC/config.plist
   ```

5. Place the prepared `EFI/OC/` and matching `EFI/BOOT/BOOTx64.efi` on the test USB's EFI partition. Record the exact laptop model, BIOS revision, macOS build, and feature results before moving the EFI to an internal disk. See the [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/).

## Credits and license

Thanks to the OpenCore, kext, and tooling maintainers. The repository license is in [LICENSE](LICENSE). Bundled third-party components retain their upstream licenses.

See the [AppleALC license](docs/licenses/AppleALC-LICENSE.txt) and the [SimpleHDA notice](docs/licenses/SimpleHDA-NOTICE.md), along with the licenses packaged with SimpleHDA for [XNU](docs/licenses/SimpleHDA-xnu-APPLE_LICENSE.txt) and [Lilu](docs/licenses/SimpleHDA-Lilu-LICENSE.txt).
