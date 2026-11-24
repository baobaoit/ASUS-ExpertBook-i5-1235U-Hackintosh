# ASUS ExpertBook i5-1235U Hackintosh

OpenCore EFI for the ASUS ExpertBook with an Intel Core i5-1235U. The internal EFI booted macOS Tahoe 26.7.3 and passed a built-in speaker playback test. The internal microphone still needs a fix.

## Hardware specifications

| Component | Details |
| --- | --- |
| Laptop | ASUS ExpertBook (exact model suffix unconfirmed) |
| Processor | Intel Core i5-1235U (Alder Lake-U), 2 performance cores, 8 efficiency cores, 12 threads |
| Integrated graphics | Intel integrated graphics (Iris Xe eligible) |
| Memory | 16 GB DDR4, 3200 MHz reported by macOS |
| NVMe storage | Solidigm SSDPFKNU512GZ |
| Audio codec | Realtek ALC256 |
| Display panel and wireless card | Exact models unconfirmed |

[Intel processor specifications](https://www.intel.com/content/www/us/en/products/sku/226261/intel-core-i51235u-processor-12m-cache-up-to-4-40-ghz/specifications.html)

## Test environment

| Item | Recorded value |
| --- | --- |
| macOS | Tahoe 26.7.3 (25G342), booted from the internal EFI |
| BIOS revision | Unconfirmed |
| OpenCore release | Exact version of the bundled binary is unverified |
| SMBIOS model | `MacBookPro16,2` |

## Feature status

| Feature | Result | Test or configuration detail |
| --- | --- | --- |
| Boot | Working | Internal EFI booted the Tahoe build listed above. |
| Built-in speakers | Working | Playback confirmed with `alcid=41`. |
| Internal microphone | Needs a fix | Microphone capture remains unresolved. |
| Graphics and brightness | Working | Display output and brightness control confirmed. Metal acceleration remains unverified. |
| Wi-Fi | Working | Wireless connectivity confirmed with ForbiddenItlwm 0.6.0 enabled. |
| Bluetooth and Continuity | Unverified | IntelBluetoothFirmware and BlueToolFixup are enabled. |
| Ethernet | Unverified | IntelMausiEthernet is enabled. |
| Keyboard and trackpad | Working | Keyboard input works in the OpenCore picker and in macOS. Trackpad input and multitouch gestures work in macOS. |
| USB and battery | Working | USB connectivity and battery reporting confirmed. |
| Webcam and sleep/wake | Unverified | No test results recorded. |

## EFI configuration

| Component | Configuration |
| --- | --- |
| Audio | Lilu loads before AppleALC 1.9.8 and SimpleHDA 1.0.2. SimpleHDA targets x86_64 on Darwin 25 or later. `DisableLinkeditJettison` is enabled. |
| Graphics | WhateverXe is enabled. Check the [WhateverXe release notes](https://github.com/b00t0x/WhateverXe/releases) for macOS-side requirements. |
| Keyboard and trackpad | Ps2KeyboardDxe provides picker keyboard support. VoodooPS2Keyboard handles the macOS keyboard. VoodooI2C and VoodooI2CHID handle the trackpad. |
| UEFI drivers | OpenRuntime, OpenCanopy, ResetNvramEntry, Ps2KeyboardDxe, HfsPlus, apfs_aligned, ext4_x64, and OpenLinuxBoot are enabled. |
| ACPI | Eleven enabled SSDTs cover devices including the embedded controller, GPIO, backlight, and USB. |

See the [EFI directory tree](docs/efi-oc-tree.md) for exact filenames and the [OpenCore configuration](EFI/OC/config.plist) for load order.

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
