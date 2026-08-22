# Sonic Advance — Recompilation Project

A native, high-performance C/C++ port of **Sonic Advance** (Game Boy Advance) for modern platforms, created via static recompilation using `GBARecomp`.

This project translates the original GBA machine code into clean, platform-agnostic C/C++, running natively without CPU emulation overhead, input lag, or reliance on legacy J2ME adaptations.

---

## Features

* **100% Native Execution:** Zero CPU emulation. Direct compilation to x86_64 and ARM64 architectures.
* **Ultra-Low Latency:** Instantaneous input response powered by an SDL2 backend.
* **CRT & Display Shaders:** Crisp subpixel/CRT panel simulation matching the original GBA screen.
* **Enhanced Audio:** Per-channel sinc interpolation, soft-clipping, and shadow HLE audio processing.
* **Cross-Platform:** Out-of-the-box support for Linux, Windows, macOS, Android, and embedded retro handhelds.

---

## Prerequisites

* **C++ Compiler:** `clang` (version 18+ recommended) or `gcc`
* **Build System:** `cmake` and `ninja-build`
* **Development Libraries:** `libsdl2-dev`
* **Game Assets:**
* Original *Sonic Advance* GBA ROM (`SonicAdvance.gba`)
* Official GBA BIOS image (`gba_bios.bin`)



---

## Quick Start (Linux)

### 1. Install Dependencies

```bash
sudo apt update
sudo apt install -y build-essential cmake ninja-build clang libsdl2-dev

```

### 2. Configure `pack.toml`

Verify your ROM and BIOS SHA-256 checksums using `sha256sum`:

```bash
sha256sum SonicAdvance.gba
sha256sum gba_bios.bin

```

Update your `pack.toml` with the generated hashes:

```toml
[package]
name = "SonicAdvance"
version = "0.1.0"
platforms = ["linux", "windows", "macos", "android"]

[image]
rom-sha256  = "YOUR_ROM_SHA256_HASH_HERE"
bios-sha256 = "YOUR_BIOS_SHA256_HASH_HERE"

[runtime]
menu = true
enhanced-audio = true
screen-sim = true
engine-hle = "auto"
interpreter = true

[build]
compiler = "clang"

[output]
binary = true
c-source = true

```

### 3. Build & Run

Execute the recompilation pipeline:

```bash
gba-pack pack.toml

```

---

## Cross-Platform Targets

### Android (ARM64)

1. Set `c-source = true` in `pack.toml` to emit the recompiled C codebase.
2. Import the C source tree into an Android Studio C++/NDK project.
3. Link against `libSDL2.so` using the `SDLActivity` wrapper for touch overlay controls.
4. Build the final standalone `.apk`.

### Windows & macOS

* **Windows:** Cross-compile using `mingw-w64` or build natively via MSVC/Clang.
* **macOS:** Compile directly using Apple Clang or run via GitHub Actions (`macos-latest`).

---

## Disclaimer

This repository contains **no copyrighted assets, ROMs, or proprietary BIOS code**. You must provide your own legally obtained copy of *Sonic Advance* and a GBA BIOS file to compile and run the project. All Sonic the Hedgehog trademarks belong to SEGA.
