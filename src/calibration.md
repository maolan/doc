# OSS Latency Calibration

On FreeBSD, connect a physical output to an input and run:

```sh
cargo run --bin maolan-calibrate -- --input-device /dev/dsp5 --input-channel 8 --output-device /dev/dsp5 --output-channel 3
```

Channels are numbered from 1. Close other applications using the device before
calibrating. The tool opens the normal Maolan audio engine and routes its IO Delay
generator to the selected output and the selected input to a measurement node.
For each supported period it measures for two seconds, invokes the same calibration
action as the GUI, and saves the returned playback lead and recording offset to
`~/.config/maolan/daw/config.toml` before moving to the next period. A period that
fails to resolve is reported and skipped.

Defaults are 48,000 Hz, 32-bit audio, two periods, sync mode off, and exclusive
mode off. Use `--rate`, `--bits`, `--nperiods`, `--sync-mode`, and `--exclusive`
to match the GUI's device settings. `--gain` adjusts measurement input gain.
Use the same engine runtime environment settings when calibrating and running
the DAW.

Maolan and maolan-cli load matching device-pair, sample-rate, bit-depth, period,
and mode records when opening audio. The saved values replace the engine's
input/output latency totals, just as the IO Delay calibration button does.
IO Delay splits the measured round trip equally, assigning an odd extra frame
to playback; this is an assumption, not an independent measurement of each direction.
Older records from the standalone mmap measurement path are ignored. Rerun
calibration to replace them with records marked `engine_io_delay_v1`.
