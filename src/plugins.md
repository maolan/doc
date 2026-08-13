# Maolan Plugins

The complete Maolan in-house plugin collection. Built in Rust as CLAP plugins with Iced-based GUIs in the TokyoNight theme.

- 18 exported variants
- 13 distinct products
- Iced TokyoNight GUI
- BSD-2 license

## Dynamics

Compressors, limiters, and de-essers for controlling dynamics and taming peaks.

### Compressor

Plugin ID: `rs.maolan.compressor`

Multiband compressor with LR4 crossovers. Peak/RMS sidechain, FabFilter Pro-MB-style Compress/Expand modes with signed Range, lookahead, sidechain boost, and classic/modern topology. Double-click the spectrum display to add bands. Drag crossover lines to move splits. Drag the white gain contour to adjust Gain/Makeup for the band under the cursor; middle-drag it to adjust Range; right-drag it to adjust Threshold. Drag the yellow contour to adjust Range directly, or the blue contour to adjust Threshold directly. Negative Range draws below gain and positive Range draws above it.

### Limiter

Plugin ID: `rs.maolan.limiter`

Adaptive clipper/limiter with Vintage and Modern variants. Multiple limiting modes from subtle attenuation to aggressive clipping. Stereo I/O.

### DeEsser

Plugin ID: `rs.maolan.deesser`

Sibilance reduction processor. Detects ess sounds via slew-rate patterns across a configurable window. IIR smoothing, dynamic ratio reduction, and monitor mode. Stereo I/O.

## EQ

Precise tone shaping with 32 bands in both graphic and parametric flavors.

### Parametric EQ

Plugin ID: `rs.maolan.equalizer`

32-band parametric equalizer using peaking biquad filters. Each band has independent Frequency, Gain, Q, Type, Slope, and Dynamics controls. Middle-drag a selected bell band dot to create or adjust its dynamic range target. Input and output gain with global bypass. Mono or stereo I/O depending on host channel count.

## Time & Space

Delays and reverbs for depth, dimension, and atmosphere.

### Delay

Plugin ID: `rs.maolan.delay`

Delay with millisecond or tempo-synced note divisions. Circular buffers with linear interpolation and smooth delay-time chasing. Reads host BPM from CLAP transport.

### Reverb

Plugin ID: `rs.maolan.reverb`

Stereo reverb built from three allpass-like delay blocks with cross-feedback, vibrato predelay, and input/output lowpass filters. Based on Airwindows Reverb.

## Stereo

Stereo width processors and imagers for spatial control.

### Stereo

Plugin ID: `rs.maolan.stereo`

Stereo width processor. Mid/side processing with density controls and delay-based focus. Stereo I/O. Best suited for mastering.

### Widener

Plugin ID: `rs.maolan.widener`

Multiband stereo width processor with independent Low, Mid, and High band controls. Uses LR4 crossovers and mid/side processing per band. Monitor mode for checking stereo, mono, and side signals. Stereo I/O. Best suited for single instruments.

## Tone & Character

Saturation, color, and monitoring reference tools.

### Saturator

Plugin ID: `rs.maolan.saturator`

Waveshape saturation with sine-based distortion and intensity-dependent blend. Stereo I/O.

### Monitoring

Plugin ID: `rs.maolan.monitoring`

Monitoring toolbox with 17 reference modes for checking mixes on different playback systems. Stereo I/O.

## Instruments & Modeling

Drum sampling and neural amp modeling.

### Drust

Plugin ID: `rs.maolan.drust`

Drum sampler CLAP plugin inspired by DrumGizmo. Async kit loading, MIDI triggering, velocity mapping, round-robin, humanization, per-output balancing, and built-in limiter. 16 mono outputs (Kick L/R, Snare L/R, HiHat L/R, Toms L/R, Ride L/R, Crash L/R, China/Splash L/R, Ambience L/R).

### Maolan Kick

Plugin ID: `rs.maolan.kick`

Percussive synthesizer with layered oscillators and noise. MIDI note-triggered with 16 mono outputs, velocity sensitivity, and a multi-layer DSP engine. Suitable for designing kick and percussion sounds from scratch without sample content.

### Rural Modeler

Plugin ID: `rs.maolan.ruralmodeler`

Neural Amp Modeler (NAM) plugin. Loads neural network amp models and impulse responses. Includes a noise gate, tone stack (Bass/Mid/Treble), input/output calibration, and DC blocking. Mono I/O.

## Per-Process Plugin Hosting

Each plugin instance runs in its own isolated OS process. A plugin crash cannot bring down the DAW or stop playback on other tracks.

### Crash Isolation

If a plugin segfaults, the OS kills only its host process. The DAW detects the death, mutes the track, and continues playback for all other tracks without interruption.

### Shared-Memory IPC

Audio buffers are exchanged through memory-mapped shared memory (<200 µs round-trip per block). Lock-free ring buffers carry parameters, MIDI, and transport state without blocking the real-time audio thread.

### DAW-Owned Scheduling

The DAW controls how many worker threads each plugin process may use per audio block. Plugins request work via `clap_host_thread_pool`; the DAW decides based on global CPU load, eliminating core collisions.

### Sample-Accurate Automation

Parameter changes carry an exact sample offset within each block. Automation curves are subdivided into per-sample events and delivered through the IPC ring buffer with no smoothing layer added by the host.

### Format Coverage

Out-of-process hosting covers CLAP, VST3, and LV2. CLAP gets native thread-pool sharing; VST3 and LV2 run as single-threaded workers with the same IPC protocol and crash recovery path.

### Windows Support

The IPC layer uses `CreateFileMapping` on Windows and `shm_open` on Unix. Plugin processes are spawned with `CreateProcess` and GUI embedding uses `SetParent`. CLAP and VST3 are supported on Windows; LV2 remains Unix-only.

## Plugin Format

All Maolan plugins are distributed as CLAP (CLever Audio Plugin) binaries with embedded Iced GUIs. They support Linux, FreeBSD, and Windows.

The plugin collection is developed in the [plugins](https://github.com/maolan/plugins) repository. UI windowing is handled by [baseview](https://github.com/maolan/baseview), a low-level window system interface for audio plugin UIs.
