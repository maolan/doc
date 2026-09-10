# Getting Started

Maolan is currently available for FreeBSD, Linux, macOS, and Windows. Prebuilt packages are provided for FreeBSD, Linux, and Windows; on macOS build from source.

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

- **Linux:** `pkg-config`, ALSA dev packages, and JACK dev packages if you want the JACK backend.
- **FreeBSD:** `pkg-config` and the JACK dev package if you want the JACK backend; the OSS backend uses the in-kernel OSS API (no extra packages).
- **macOS:** Xcode Command Line Tools (provides the linker and system headers). Audio I/O is CoreAudio and MIDI is CoreMIDI, both accessed directly with no extra libraries.
- **Windows:** Visual Studio Build Tools with the C++ workload. NSIS is only needed to build the installer. See `maolan/scripts/build.ps1` and `plugins/build.ps1` for the automated setup.

## Next Steps

- [Review the feature set](./features.md)
- [Read the workflow reference](./workflow.md)
- [Check keyboard shortcuts](./shortcuts.md)
- [Explore OSC support](./osc.md)
- [Browse the Maolan plugin collection](./plugins.md)
- [Use Maolan Generate](./maolan-generate.md)
- [Control Behringer mixers with MixOSC](./mixosc.md)
