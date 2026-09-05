# Maolan Plugins

The complete Maolan in-house plugin collection. Built in Rust as CLAP plugins with Iced-based GUIs in the TokyoNight theme.

- 22 exported variants
- 17 distinct products
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

## Modulation & Vocal Effects

Chorus, phaser, formant filtering, and vocoding.

### Chorus

Plugin ID: `rs.maolan.chorus`

Multi-voice stereo chorus with modulated delay lines. Even voices read from the left channel and odd voices from the right, producing a wide stereo image.

**Parameters**

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Mod Depth | 0.0 ... 10.0 ms | 5.0 | LFO delay modulation depth |
| Mod Rate | 0.1 ... 5.0 Hz | 0.5 | LFO rate |
| Dry/Wet | 0.0 ... 1.0 | 0.5 | Mix balance |
| Voices | 2 ... 16 | 8 | Number of chorus voices |

### Phaser

Plugin ID: `rs.maolan.phaser`

Modulated all-pass cascade phaser. The LFO sweeps the center frequency of up to 12 first-order all-pass stages. Feedback can be taken from the previous output or from a configurable delay line.

**Parameters**

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| LFO Rate | 0.01 ... 2.0 Hz | 0.1 | LFO rate |
| LFO Depth | 0.0 ... 1.0 | 0.5 | LFO modulation depth |
| Manual (Center) | 0.0 ... 1.0 | 0.5 | Manual center position |
| Feedback | −0.98 ... 0.98 | 0.0 | Feedback amount |
| Feedback Delay On | 0 / 1 | 0 | Use delay-line feedback instead of previous output |
| Delay Time | 0.0 ... 20.0 ms | 1.0 | Feedback delay time |
| Stages (All-pass) | 1 ... 12 | 12 | Number of all-pass stages |

### Formant

Plugin ID: `rs.maolan.formant`

Vowel formant filter using three constant-Q bandpass biquads per channel. The Vowel control crossfades between the A, E, I, O, and U vowel tables for continuous timbre shaping.

**Parameters**

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Vowel (A-E-I-O-U) | 0.0 ... 4.0 | 0.0 | Vowel selector with interpolation |
| Sharpness (Q) | 2.0 ... 40.0 | 2.0 | Bandpass filter Q |
| Output Gain | −60.0 ... 20.0 dB | 0.0 | Output gain |

### Vocoder

Plugin ID: `rs.maolan.vocoder`

24-band filter-bank vocoder. Each band has its own envelope follower that shapes the band-limited signal before summing. Spectral Shift transposes the entire filter bank.

**Parameters**

| Parameter | Range | Default | Description |
|-----------|-------|---------|-------------|
| Spectral Shift | 0.5 ... 4.0 | 0.5 | Filter-bank frequency shift multiplier |
| Dry/Wet | 0.0 ... 1.0 | 1.0 | Mix balance |

## Instruments & Modeling

Drum sampling and neural amp modeling.

### Maolan Drums

Plugin ID: `rs.maolan.drums`

Drum sampler CLAP plugin inspired by DrumGizmo. Async kit loading, MIDI triggering, velocity mapping, round-robin, humanization, per-output balancing, and built-in limiter. 16 mono outputs (Kick L/R, Snare L/R, HiHat L/R, Toms L/R, Ride L/R, Crash L/R, China/Splash L/R, Ambience L/R).

### Maolan Kick

Plugin ID: `rs.maolan.kick`

Percussive synthesizer with layered oscillators and noise. MIDI note-triggered with 16 mono outputs, velocity sensitivity, and a multi-layer DSP engine. Suitable for designing kick and percussion sounds from scratch without sample content.

### Maolan Sampler

Plugin ID: `rs.maolan.sampler`

Polyphonic sample player supporting **SFZ (v1/v2)** and **SoundFont 2 (SF2.01/SF2.04)** instruments in addition to standalone WAV files.

- **SFZ Format Engine:** Includes preprocessor for `#include` relative path imports, `#define` macros, `#if`/`#else`/`#endif` blocks, and header scope precedence (`control` → `global` → `master` → `group` → `region`). Supports core v1/v2 opcodes for key/velocity mapping, key crossfades, tuning, panning, loops, playback directions, keyswitches, round-robin / random variants, envelope generators, LFOs, and multimode filters.
- **SoundFont 2 (SF2) Engine:** Parses RIFF SoundFont files with 16-bit and 24-bit PCM sample data, `INFO` metadata, multi-preset bank structures, generator hierarchy merging (`GeneratorSet`), and default/custom `imod` modulators mapped to the modulation matrix.
- **Background Loading:** Instrument parsing and resample rendering occur asynchronously on a background worker thread. New patches swap into the audio engine atomically (`AtomicArc`) without interrupting active voices or causing audio dropouts.
- **Interactive GUI:** Supports drag-and-drop file loading, bank/preset dropdown selection, real-time loading progress indicator, instant reload button for SFZ editing, and scrollable diagnostic error logging.

### Synth

Plugin ID: `rs.maolan.synth`

Polyphonic synthesizer inspired by Surge XT. Features three oscillators with multiple synthesis
modes (including wavetable, FM, and physical-modeling flavors), two multimode filters with
configurable routing, three envelopes, six LFOs, a 12-slot modulation matrix, an MSEG, a step
sequencer, noise and waveshaper sections, and microtonal tuning support. Stereo I/O.

**Parameter groups**

| Group | Description |
|-------|-------------|
| Osc1–Osc3 | Type, octave, semitone, fine, shape, skew, formant, level, unison, sync, sub, routing, solo/mute |
| Filter1–Filter2 | Type, subtype, cutoff, resonance, EG amount, key tracking, drive, feedback, enable |
| Filter | Filter routing and balance |
| AmpEG / FilterEG / PitchEG | Attack, decay, sustain, release, mode, shapes, retrigger, tempo sync, uber release |
| LFO1–LFO6 | Rate, shape, amount, deform, trigger, sync mode/division, envelope, phase, unipolar |
| Mod | Fixed mod depths (velocity/key/LFO to filter, mod wheel/aftertouch to filter) |
| ModRoute1–12 | Source, target, depth, curve |
| Noise | Type, level, color, filter, stereo, enabled |
| Waveshaper | Shape, drive, mix, enable |
| Flavor | Additional filter-like flavor stage |
| Step Seq | 16 step values, loop start/end, shuffle, trigger targets |
| MSEG | 128 nodes, 127 segment curves, loop, retrigger targets |
| Macros | Macro1–8 modulation sources |
| Master | Volume, pan, width, polyphony, portamento, pitch-bend range, play mode, voice priority |
| Tuning | Scale, root, SCL index |
| FM / Twist / String / Alias | Oscillator-specific parameters for FM, twist, string, and alias engines |

### Maolan Modeler

Plugin ID: `rs.maolan.modeler`

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
