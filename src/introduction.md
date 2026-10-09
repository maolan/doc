# Introduction

Maolan is a digital audio workstation for recording, editing, routing, and
producing audio. It is built in Rust as a set of separate components: an audio
engine, a graphical application, and command-line tools. This structure lets
the engine handle audio work independently of the interface, while the GUI
provides the workspace for arranging and managing a session.

## Working with sessions

Maolan combines timeline-based recording and playback with non-destructive
editing. Your source material remains available while you arrange and refine a
session, so you can make changes without treating each edit as a permanent
rewrite of the original audio. The engine processes audio and MIDI tracks,
routes signals between tracks and plugins, and provides tools for recording,
playback, and exporting a finished mix.

The live session view is designed for working with a session as it is being
performed. Alongside the timeline, it offers a way to work with session
material in a more immediate, performance-oriented setting.

## Plugins and audio devices

Maolan supports the CLAP and VST3 plugin formats on its supported platforms,
and LV2 on Unix systems. Plugins run in separate host processes, which helps
keep a plugin failure from taking down the main application. Compatibility
depends on the plugin and platform, and support continues to evolve.

Audio device support varies by operating system. Maolan uses ALSA and JACK on
Linux, OSS and JACK on FreeBSD, CoreAudio on macOS, and WASAPI on Windows.

## Components and platforms

The engine, graphical interface, and command-line tools are maintained as
separate libraries and binaries. This gives the project distinct places for
audio processing, interactive session work, and command-line operations.

Maolan targets FreeBSD, Linux, Windows, and macOS. Available audio backends and
plugin formats differ between these systems, so check the relevant platform
notes when choosing devices or plugins.
