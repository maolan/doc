# Audio Latency Calibration

Maolan measures round-trip latency by sending a signal from an audio output
through a physical loopback cable and receiving it at an audio input. The
`maolan-calibrate` command-line utility runs this measurement through Maolan's
audio engine on Linux, FreeBSD, and macOS. It is not limited to OSS devices.

Connect hardware output to an input, then list available devices:

```sh
cargo run --bin maolan-calibrate -- --list-devices
```

Use the device IDs printed by `--list-devices` in the matching command below.
The examples use channel 1; choose channel numbers that match your loopback
cable and hardware. If input and output use different devices, supply each
device's ID separately.

### Linux (ALSA)

This example selects ALSA card 0, device 0 for both input and output. Replace
`hw:0,0` with the ID shown for a device that supports both directions:

```sh
cargo run --bin maolan-calibrate -- --input-device hw:0,0 --input-channel 1 --output-device hw:0,0 --output-channel 1
```

### FreeBSD (OSS)

Replace `/dev/dsp5` with the OSS device ID reported on your system:

```sh
cargo run --bin maolan-calibrate -- --input-device /dev/dsp5 --input-channel 1 --output-device /dev/dsp5 --output-channel 1
```

### macOS (CoreAudio)

CoreAudio device IDs are UIDs. Replace the placeholders with the exact UIDs
printed by `--list-devices` for your input and output devices:

```sh
cargo run --bin maolan-calibrate -- --input-device "<input-device-UID>" --input-channel 1 --output-device "<output-device-UID>" --output-channel 1
```

### Windows

The `maolan-calibrate` utility is not currently available on Windows, so there
is no Windows command example. The utility supports Linux, FreeBSD, and macOS.

### Tips

Close other applications using the device before calibrating. The utility
opens the normal Maolan audio engine and routes its IO Delay generator to the
selected output and the selected input to a measurement node. For each
supported period, it measures for two seconds, applies the calibration, and
saves the playback lead and recording offset before continuing. A period that
fails to resolve is reported and skipped.

Defaults are 48,000 Hz, 32-bit audio, two periods, sync mode off, and exclusive
mode off. Use `--rate`, `--bits`, `--nperiods`, `--sync-mode`, and `--exclusive`
to configure the device; `--gain` adjusts measurement input gain. Exact options
and device IDs depend on the platform and backend. Use the same engine runtime
environment settings when calibrating and running the DAW.

The current saved-calibration configuration is applied when opening FreeBSD
OSS devices. It matches the input/output device pair, sample rate, bit depth,
period, and mode, and replaces the engine's input and output latency totals.
On Linux and macOS the utility can measure latency, but Maolan does not yet
reload saved measurements as device latency overrides. Older records from the
standalone mmap measurement path are ignored; rerun calibration to replace them
with records marked `engine_io_delay_v1`.
