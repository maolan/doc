# Maolan Engine

`maolan-engine` is the audio and MIDI processing library used by the Maolan
DAW. It is a separate Rust crate, so other Rust applications can also build on
it. The engine handles device IO and session processing; Maolan's graphical
interface and command-line tools communicate with it through messages.

## What it does

The engine processes audio and MIDI tracks for recording, playback, and
timeline editing. Tracks can be routed to other tracks and through plugin
graphs. It also provides automation and modulation processing, audio and MIDI
recording, clip playback, and helpers for offline rendering and export.

Track work is distributed across engine workers. A render plan describes the
work for an audio cycle, including track dependencies and routing, so
independent work can run in parallel while connected tracks retain the
required processing order. The engine also supports offline rendering, where
audio can be processed without running against a live device clock.

When opening a session, Maolan keeps the loading screen visible until plugin
state, connections, clip caches, and the render plan have been restored.
Playback shortcuts are inactive during loading.

## Audio backends

The available device backend depends on the operating system:

| Operating system | Audio backends |
| --- | --- |
| Linux | ALSA, JACK |
| FreeBSD | OSS, JACK |
| macOS | CoreAudio |
| Windows | WASAPI |

Sample rates, buffer sizes, channel counts, and device selection depend on the
backend and hardware. Maolan's device settings expose the options available
for the selected device.

## Plugin hosting

CLAP, VST3, LV2 (on Unix systems), and Audio Unit (on macOS) plugins run in
separate host processes, one process per plugin instance. The engine and
plugin host exchange audio, MIDI, parameter, and state data through shared
memory and lightweight inter-process events. Keeping plugin code outside the
DAW process means a plugin crash can be isolated: the engine can detect the
failed host, bypass that plugin, and keep the main application running.

## Using the engine from another application

`maolan-engine` is an independent Rust crate that applications can add as a
Cargo dependency. A host application can provide its own interface and use
the engine for device IO, audio and MIDI processing, routing, plugin hosting,
and offline rendering without embedding the Maolan DAW interface.

Applications control the engine through its message interface: send requests
to open devices, control transport, and edit tracks, then handle the resulting
events and state updates. The crate also exposes reusable modules for audio
codecs, MIDI, routing, plugin interfaces, render plans, and worker execution.
Consult the `maolan-engine` crate documentation for the public API and
platform-specific modules available to your application.
