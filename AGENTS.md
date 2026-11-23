# Repository Guidelines

## Project Structure

This repository contains the OpenCore configuration for an ASUS ExpertBook with an Intel Core i5-1235U (Alder Lake-U). The root `README.md` introduces the project, `LICENSE` contains its license, and `.gitignore` covers macOS metadata and temporary files.

- `EFI/OC/` contains `config.plist` and `OpenCore.efi`. Supply the matching `EFI/BOOT/BOOTx64.efi` separately when preparing a standalone USB boot drive.
- `EFI/OC/ACPI/`, `EFI/OC/Drivers/`, and `EFI/OC/Kexts/` hold compiled ACPI tables, UEFI drivers, and kernel extensions, respectively.
- `EFI/OC/Resources/` holds picker fonts, images, and labels. The repository tracks no entries under `EFI/OC/Tools/`.

## Development and Verification

There is no build system or automated test runner. After EFI changes, run `plutil -lint EFI/OC/config.plist` on macOS to check plist syntax. Confirm the bundled OpenCore release and use its matching `ocvalidate` binary to check the configuration with `ocvalidate EFI/OC/config.plist`. If the release or validator is unavailable, record which checks you completed.

For hardware testing, record the exact ExpertBook model, BIOS revision, macOS build, and observed boot and device behavior. For keyboard changes, test input in the OpenCore picker and in macOS. The configuration enables `Ps2KeyboardDxe.efi` for the picker and `VoodooPS2Keyboard.kext` for macOS.

Run `git status --short` to review changed and untracked files. Run `git diff --check` for unstaged changes and `git diff --cached --check` for staged changes. For documentation changes, check Markdown rendering, links, and command examples.

## Style and Configuration

Use descriptive Markdown headings, backticks for paths and commands, and fenced blocks for multiline examples. Preserve filename capitalization and update the corresponding `config.plist` entries when adding, renaming, or removing components. Check `ACPI → Add`, `UEFI → Drivers`, `Kernel → Add`, or `Misc → Tools` as applicable. For enabled kexts, verify the bundle path, plist path, and executable path when present, including paths for nested plug-ins.

Keep `MLB`, `ROM`, `SystemSerialNumber`, and `SystemUUID` blank under `PlatformInfo → Generic` in the tracked configuration. Set personal values in a private test EFI and remove identifying information from shared logs and screenshots.

When comparing `config.plist` files, exclude the entire `PlatformInfo` section from the comparison and its output unless the user explicitly asks to compare it.

## Commits and Pull Requests

Use a short, descriptive commit subject. Recent EFI commits use the `feat(efi):` prefix for feature changes. In pull requests, summarize the change, explain why it is needed, and state how you verified it. Link related issues when available and include screenshots when they help reviewers verify a result.

Include `Co-authored-by: Codex <codex@openai.com>` in every commit Codex creates, with a blank line before the trailer block.
