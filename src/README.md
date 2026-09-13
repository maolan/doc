# Maolan

> Open source digital audio workstation built in Rust for recording, MIDI editing, automation, routing, and modern production workflows.

Maolan is a free, open-source DAW written in Rust. It prioritizes transparency, performance, and community-driven development.

Inspect the code. Build custom features. Contribute improvements. Own your tools.

- 100% open source under a permissive license
- Built with Rust for safety and performance
- Community-driven development and improvements
- Forever free, no licensing fees

## Quick Start

```bash
git clone https://github.com/maolan
cd maolan
cargo run --release
```

## Key Capabilities

### Multi-Track Audio & MIDI

Record and arrange unlimited audio and MIDI tracks with precise timing and flexible mixing.

### Piano Roll MIDI Editing

Intuitive piano roll interface for composing, editing, and refining MIDI performances.

### Automation & Envelopes

Create track and plugin automation for volume, balance, mute, and loaded CLAP, VST3, or LV2 parameters. Save session and track templates for repeatable setups.

### Plugin Hosting & Routing

Load CLAP, VST3, and LV2 plugins, create complex routing chains, and design custom signal flows with explicit audio, MIDI, and sidechain paths.

### Export & Format Support

Export mixdowns or stems to WAV and FLAC with normalization and master-limiter options saved in the session.

### Autosave & Recovery

Automatic project backups and recovery features protect your work from unexpected interruptions.

### Ecosystem Tools

Use the in-house [Maolan plugin collection](./plugins.md), generate audio with
[Maolan Generate](./maolan-generate.md), and control Behringer X32 or X-Air
mixers with [MixOSC](./mixosc.md).

## Complete Production Workflow

1. **Recording:** capture audio and MIDI from microphones, instruments, and controllers.
2. **Editing and composition:** shape clips, notes, harmonies, and arrangements with piano-roll tools.
3. **Plugin and routing:** load CLAP, VST3, and LV2 plugins and connect explicit audio, MIDI, and sidechain paths.
4. **Automation:** write volume, pan, send, and plugin automation across the timeline.
5. **Mixing and mastering:** balance levels and processing for a final production-ready session.
6. **Export:** render full mixes or stems to standard delivery formats.

## Open Source & Community Driven

Maolan is open source because audio production tools should be transparent, accessible, and shaped by their users.

You can inspect the code, understand how features work, and contribute improvements directly.

- **Contribute code** to core features and plugins.
- **Report bugs** and propose improvements.
- **Write documentation** and tutorials.
- **Build extensions** for your own workflow.

### Project Stats

| Item | Value |
| --- | --- |
| GitHub | [github.com/maolan](https://github.com/maolan) |
| License | BSD-2-Clause |
| Language | Rust |
| Status | Active Development |

### Download

Download the x86_64 Fedora, Debian, Ubuntu, macOS and Windows package from the release page:

[github.com/maolan/maolan/releases/tag/0.2.3](https://github.com/maolan/maolan/releases/)

### Build from Source

Maolan is open source. If you prefer to build manually clone the repository and build with Cargo:

```bash
git clone https://github.com/maolan
cd maolan
cargo run --release
```

#### Platform prerequisites

- **Linux:** `pkg-config`, ALSA dev packages, and JACK dev packages.
- **FreeBSD:** `pkg-config` and the JACK dev package.
- **macOS:** Xcode Command Line Tools (provides the linker and system headers). Audio I/O is CoreAudio and MIDI is CoreMIDI, both accessed directly with no extra libraries.
- **Windows:** Visual Studio Build Tools with the C++ workload. NSIS is only needed to build the installer. See `maolan/scripts/build.ps1` and `plugins/build.ps1` for the automated setup.
