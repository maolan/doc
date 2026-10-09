# Maolan Editor

Maolan Edit is a waveform editor built as a reusable Rust crate. It runs as a
standalone application and its interface can also be embedded in Maolan, where
it is used to inspect and edit audio within a session. The editor shares
Maolan's audio decoding, encoding, and UI components.

## Working with audio

Open an audio file to view its waveform, select a range, and preview playback.
Edits include fades, gain changes, reverse, deleting a selection, and replacing
a selection with silence. Changes can be undone and redone. The editor also
supports moving the playhead, jumping to a zero crossing, and working with
markers to identify useful regions in a file.

Marker ranges can be exported as separate audio files. Export options include
the output format, bit depth where applicable, and sample rate. The editor can
also save the edited audio as a new file, leaving the original available if a
different output path is chosen.

## Audio formats

The open dialog supports WAV, FLAC, MP3, Ogg/Vorbis, and M4A/AAC/ALAC files.
Export supports WAV, FLAC, Ogg FLAC, and MP3. Unsupported output extensions
are rejected. Available format details and options may vary by export format.

## Standalone and embedded use

As a standalone application, Maolan Edit can open files, play them through a
configured audio device, edit and save them, and export marker ranges. When
embedded in Maolan, the editor can open a session audio clip for waveform-based
editing. Clip edits are stored as actions in the session and remain
non-destructive; save the session to keep them. The DAW connects the editor to
session playback and handles loading the clip, while the standalone application
manages its own file and device workflow.
