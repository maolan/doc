# Getting Started

Maolan is currently available for FreeBSD, Linux, and Windows.

## Download

### FreeBSD

Install from packages:

```bash
pkg install maolan
```

### Linux

Download the x86_64 Fedora, Debian, and Ubuntu package from the release page:

[github.com/maolan/maolan/releases/tag/0.2.3](https://github.com/maolan/maolan/releases/tag/0.2.3)

### Windows

Download the x86_64 installer (EXE) for Windows 10 and 11 from the release page:

[github.com/maolan/maolan/releases/tag/0.2.3](https://github.com/maolan/maolan/releases/tag/0.2.3)

## Build from Source

Maolan is open source. If you prefer to build manually clone the repository and build with Cargo:

```bash
git clone https://github.com/maolan
cd maolan
cargo run --release
```

The main application is in the `maolan/` directory. The repository root is a multi-crate project directory, not a single Cargo workspace, so build commands must be run from the relevant crate directory:

```bash
cd maolan
cargo build --workspace
cargo run
```

### Release build

```bash
cd maolan
cargo build --workspace --release
```

### Platform prerequisites

- **Linux / FreeBSD:** `pkg-config`, JACK/ALSA dev packages, `liblilv-dev`, `libsuil-dev`, `libgtk2.0-dev`, FFmpeg libraries, LLVM/Clang (for bindgen).
- **Windows:** Visual Studio Build Tools, LLVM/Clang, NSIS, vcpkg packages (`sentencepiece:x64-windows`), FFmpeg NuGet package. See `maolan/scripts/build.ps1` and `plugins/build.ps1` for the automated setup.

## Next Steps

- [Review the feature set](./features.md)
- [Read the workflow reference](./workflow.md)
- [Check keyboard shortcuts](./shortcuts.md)
- [Explore OSC support](./osc.md)
- [Browse the Maolan plugin collection](./plugins.md)
- [Use Maolan Generate](./maolan-generate.md)
- [Control Behringer mixers with MixOSC](./mixosc.md)
