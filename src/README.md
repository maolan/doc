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

## Frequently Asked Questions

### Is Maolan free?

Yes. Maolan is completely free and open source with no licensing fees, subscriptions, or paywalls.

### Which platforms are supported?

Maolan supports Linux, FreeBSD, macOS, and Windows.

- Linux and FreeBSD builds run on Wayland when available and fall back to X11 (Xorg) when Wayland is unavailable. Plugin UI embedding still uses X11, so an X11 server must be reachable even under Wayland (for example via XWayland).
- macOS uses CoreAudio for audio and CoreMIDI for MIDI.
- Windows uses WASAPI for audio and the Win32 API for windowing.

### Which plugin formats are supported?

Maolan supports CLAP, VST3, and LV2 on Linux and FreeBSD. macOS and Windows builds support CLAP and VST3. LV2 remains Unix-only. All supported formats use per-process plugin hosting for crash isolation.

### How does autosave and recovery work?

Maolan writes autosave snapshots every 15 seconds into `.maolan_autosave/snapshots/` beside the live session, for example:

`<session>/.maolan_autosave/snapshots/<timestamp>/`

When opening a session, Maolan can detect a newer snapshot, preview the differences, and recover the latest valid autosave first.

### Does Maolan support templates?

Yes. Session templates preserve track structure, routing, plugin graphs, plugin state, metadata, and export settings. Track templates preserve one track's settings, plugin graph, plugin state, and that track's connections, while intentionally leaving out audio and MIDI clips.

### How can I contribute?

There are many ways to contribute to Maolan:

- **Code:** Submit pull requests for features, bug fixes, or improvements
- **Documentation:** Help improve guides, tutorials, and API docs
- **Testing:** Report bugs, test features, and provide feedback
- **Design:** Contribute UI/UX improvements and design ideas
- **Community:** Help other users, answer questions, and promote the project

Visit the GitHub repository to get started. All contributors are welcome!

### Can I reuse it in my Rust project?

Maolan is a two-part project: engine and GUI. The engine is independent of the GUI and can be reused in your own Rust project.

```bash
cargo add maolan_engine
```
