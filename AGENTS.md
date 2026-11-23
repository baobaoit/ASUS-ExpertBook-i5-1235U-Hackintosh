# Repository Guidelines

## Project Structure

This repository contains the OpenCore configuration for an ASUS ExpertBook with an Intel Core i5-1235U (Alder Lake-U). The root `README.md` introduces the project, `LICENSE` contains its license, and `.gitignore` covers macOS metadata and temporary files.

- `EFI/OC/` contains `config.plist` and `OpenCore.efi`. Supply the matching `EFI/BOOT/BOOTx64.efi` separately when preparing a standalone USB boot drive.
- `EFI/OC/ACPI/`, `EFI/OC/Drivers/`, and `EFI/OC/Kexts/` hold compiled ACPI tables, UEFI drivers, and kernel extensions, respectively.
- `EFI/OC/Resources/` holds picker fonts, images, and labels. The repository tracks `EFI/OC/Tools/.gitkeep` to keep the tools directory in fresh checkouts.
- `docs/efi-oc-tree.md` records the expected `EFI/OC/` paths. `docs/licenses/` holds the notices and licenses for the bundled audio kexts.

## Development and Verification

There is no build system or automated test runner. After EFI changes, run `plutil -lint EFI/OC/config.plist` on macOS to check plist syntax. Confirm the bundled OpenCore release and use its matching `ocvalidate` binary to check the configuration with `ocvalidate EFI/OC/config.plist`. If the release or validator is unavailable, record which checks you completed.

Use the [EFI directory baseline](docs/efi-oc-tree.md) when verifying the repository or internal EFI. Account for the documented differences and update the baseline only for intentional layout changes.

When importing changes from the internal EFI, back up the repository's `EFI/OC/` before editing and verify the backup's exact paths and file contents. Keep a local backup such as `OC.BAK/` out of commits using `.git/info/exclude`. Apply the intended plist changes to the tracked configuration so it retains its blank SMBIOS identifiers. After the import, compare the destination against the backup and the internal EFI to verify the intended changes and confirm that all other files match the backup byte-for-byte.

When verifying a mounted internal EFI such as `/Volumes/NO NAME/EFI/OC`, enumerate the actual entries under `Kexts/` and recursively compare their relative paths with the intended source. Every file and folder name must match exactly, including capitalization and nested `Contents/PlugIns/` paths. Report any missing, extra, or misnamed paths. Compare actual names so a case-insensitive filesystem cannot hide a mismatch. Repeat this check on the destination after any copy or move, including operations performed by Python scripts.

Check `VoodooPS2Controller.kext/Contents/PlugIns/` for the keyboard and `VoodooI2C.kext/Contents/PlugIns/` for the trackpad. A directory such as `FSCK0000.000` in either bundle is a mismatch even if its contents match the expected plug-in. Confirm that every enabled `Kernel → Add` entry uses the exact on-disk names for its `BundlePath`, `PlistPath`, and any `ExecutablePath`.

For hardware testing, record the exact ExpertBook model, BIOS revision, macOS build, and observed boot and device behavior. For keyboard changes, test input in the OpenCore picker and in macOS. The configuration enables `Ps2KeyboardDxe.efi` for the picker and `VoodooPS2Keyboard.kext` for macOS.

Run `git status --short` to review changed and untracked files. Run `git diff --check` for unstaged changes and `git diff --cached --check` for staged changes. For documentation changes, check Markdown rendering, links, and command examples.

## Audio Configuration and Testing

The Realtek ALC256 speaker configuration uses `alcid=41` in `NVRAM → Add → boot-args`. `Kernel → Add` loads `Lilu.kext`, `AppleALC.kext` 1.9.8, and `SimpleHDA.kext` 1.0.2 in that order. SimpleHDA is configured for `x86_64` with `MinKernel=25.0.0`, and `Kernel → Quirks → DisableLinkeditJettison` is enabled.

For audio layout tests, change one `alcid` at a time in a test EFI and keep `41` as the speaker fallback. After rebooting, confirm the active layout and check speaker playback and graphics responsiveness. Record microphone capture separately by checking whether the input level responds to speech. The [README](README.md#feature-status) records the current audio test results.

## Style and Configuration

Use descriptive Markdown headings, backticks for paths and commands, and fenced blocks for multiline examples. Preserve filename capitalization and update the corresponding `config.plist` entries when adding, renaming, or removing components. Check `ACPI → Add`, `UEFI → Drivers`, `Kernel → Add`, or `Misc → Tools` as applicable. For enabled kexts, verify the bundle path, plist path, and executable path when present, including paths for nested plug-ins.

Keep `MLB`, `ROM`, `SystemSerialNumber`, and `SystemUUID` blank under `PlatformInfo → Generic` in the tracked configuration. Set personal values in a private test EFI and remove identifying information from shared logs and screenshots.

When comparing `config.plist` files, exclude the entire `PlatformInfo` section from the comparison and its output unless the user explicitly asks to compare it.

## Commits and Pull Requests

Use a short, descriptive commit subject. Recent EFI commits use the `feat(efi):` prefix for feature changes. In pull requests, summarize the change, explain why it is needed, and state how you verified it. Link related issues when available and include screenshots when they help reviewers verify a result.

Include `Co-authored-by: Codex <codex@openai.com>` in every commit Codex creates, with a blank line before the trailer block.
