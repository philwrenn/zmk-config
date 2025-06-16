# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a ZMK (Zephyr Mechanical Keyboard) configuration repository for the Cradio/Sweep keyboard - a 34-key wireless split mechanical keyboard. ZMK is an open-source keyboard firmware built on the Zephyr RTOS, designed for wireless keyboards with Bluetooth support.

## Build System

This repository uses GitHub Actions for all builds. There are no local build commands.

- **Automatic builds**: Triggered on push, pull request, or manual workflow dispatch
- **Build artifacts**: GitHub Actions produces firmware files (.uf2) for flashing to the keyboard
- **Build configuration**: Defined in `build.yaml` for nice_nano_v2 boards with cradio_left and cradio_right shields

To trigger a build:
1. Push changes to GitHub
2. Check the Actions tab for build status
3. Download firmware artifacts from successful builds

## Architecture and Key Files

### Configuration Structure
- `config/cradio.keymap`: Main keymap definition with 4 layers and key bindings
- `config/cradio.conf`: Board configuration (keyboard name, features)
- `config/west.yml`: West manifest pointing to ZMK dependencies
- `build.yaml`: Build matrix for GitHub Actions

### Keymap Architecture
The keymap uses a 34-key layout (3x5 + 2 thumb keys per half) with:
- **Layer 0**: Default QWERTY with home row modifiers (A/S/D/F = Shift/Alt/Ctrl/GUI when held)
- **Layer 1**: Numbers and navigation (activated by right thumb)
- **Layer 2**: Symbols and brackets (activated by left thumb)
- **Layer 3**: Function keys and Bluetooth controls (activated when both thumbs held)

### Key Bindings Format
Keymaps use ZMK's binding syntax:
- `&kp KEY`: Regular keypress
- `&mt MOD KEY`: Mod-tap (modifier when held, key when tapped)
- `&lt LAYER KEY`: Layer-tap (layer when held, key when tapped)
- `&bt BT_*`: Bluetooth commands
- `&reset` / `&bootloader`: Firmware controls

## Development Notes

- Keymap changes are made in `config/cradio.keymap`
- Use ZMK documentation for behavior references: https://zmk.dev/docs
- The nice_nano_v2 board requires .uf2 firmware files
- Flash by putting the board in bootloader mode (double-tap reset) and copying the .uf2 file