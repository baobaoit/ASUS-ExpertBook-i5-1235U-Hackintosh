# Repository Guidelines

## Project Structure

This repository contains the OpenCore configuration for an ASUS ExpertBook with an Intel Core i5-1235U (Alder Lake-U). The root `README.md` introduces the project, `LICENSE` contains its license, and `.gitignore` covers macOS metadata and temporary files.

- `EFI/OC/` contains `config.plist` and `OpenCore.efi`. The standard UEFI fallback loader `EFI/BOOT/BOOTx64.efi` is absent from the current tree.
- `EFI/OC/ACPI/`, `Drivers/`, and `Kexts/` hold compiled ACPI tables, UEFI drivers, and kernel extensions, respectively.
- `EFI/OC/Resources/` holds picker fonts, images, and labels. `EFI/OC/Tools/` is currently empty.

## Development and Verification

There is currently no build system or automated test runner. Run `plutil -lint EFI/OC/config.plist` on macOS to check plist syntax. Use `ocvalidate EFI/OC/config.plist` with the `ocvalidate` binary from the same OpenCore release as `OpenCore.efi` to check the configuration. For hardware testing, record the model, macOS version, and boot behavior you verified.

Run `git status --short` to review changed and untracked files. Run `git diff --check` for unstaged changes and `git diff --cached --check` for staged changes. For documentation changes, check Markdown rendering, links, and command examples.

## Style and Configuration

Use descriptive Markdown headings, backticks for paths and commands, and fenced blocks for multiline examples. Preserve filename capitalization and update matching `config.plist` entries when adding, renaming, or removing ACPI tables, drivers, or kexts. Review `PlatformInfo → Generic` for machine-specific serial numbers and UUIDs before sharing the configuration. Remove personal information from logs and screenshots.

## Commits and Pull Requests

The history starts with `Initial commit` and has no established commit format. Use a short, descriptive subject such as `Document BIOS settings`. In pull requests, summarize the change, explain why it is needed, and state how you verified it. Link related issues when available and include screenshots when they help reviewers verify a result.

Include `Co-authored-by: Codex <codex@openai.com>` in every commit Codex creates, with a blank line before the trailer block.
