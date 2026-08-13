# Maolan Generate

`maolan-generate` is Maolan's prompt-driven music generation crate. It can run
as a standalone command-line tool, and it also exposes the runtime pieces that
the main DAW uses for in-process generation and decode.

- Text or lyrics prompts with optional style tags
- CPU and Vulkan backends
- HeartMuLa token generation with HeartCodec decode
- ACE-Step 1.5 instrumental generation
- Decode-only mode from saved frame JSON
- Local model directory overrides or Hugging Face cache resolution

## What It Provides

The crate has three main surfaces:

- `maolan-generate`: the CLI for generating audio from prompts.
- `heartmula_runtime`: HeartMuLa token generation and HeartCodec decode helpers.
- `heartcodec`: model loading and decode support for the packaged HeartCodec path.

The command writes a WAV file and, for HeartMuLa generation, also writes a
`*.frames.json` file next to the output. That frames file can be decoded again
with different decode settings without rerunning token generation.

## Models

| Model | CLI value | Use |
|-------|-----------|-----|
| HeartMuLa Happy New Year | `happy-new-year` | Default HeartMuLa music generation model |
| HeartMuLa RL | `RL` | Alternate HeartMuLa RL checkpoint |
| ACE-Step 1.5 Turbo | `acestep-turbo` | Instrumental generation with 8-step turbo DiT |
| ACE-Step 1.5 SFT | `acestep-sft` | Instrumental generation with 50-step SFT DiT |

The default backend is Vulkan. Use `--backend cpu` when Vulkan is unavailable
or when running on a machine without suitable GPU support.

## Basic Usage

Run from the `generate/` repository:

```bash
cargo run --release -- "warm pads, slow build, distant vocal"
```

Choose a model, backend, output path, and generation controls:

```bash
cargo run --release -- \
  --model happy-new-year \
  --backend vulkan \
  --tags "ambient, cinematic, downtempo" \
  --length 12000 \
  --cfg-scale 1.5 \
  --topk 50 \
  --temperature 1.0 \
  --ode-steps 10 \
  --output output.wav \
  --lyrics "stars drift over the late train home"
```

Run from the main Maolan workspace, when the crate is available as a package:

```bash
cargo run -p maolan-generate --release -- "warm pads, slow build, distant vocal"
```

## Decode-Only Mode

Decode a saved frames JSON without rerunning generation:

```bash
cargo run --release -- \
  --decode-only \
  --backend cpu \
  --frames-json output.frames.json \
  --output output.wav
```

For CPU decode workloads, `--decode-threads <count>` sets the Rayon worker
thread count. `--decoder-seed <int>` controls deterministic HeartCodec decoder
latents.

## ACE-Step 1.5

ACE-Step generation is instrumental only in this crate. Lyrics or vocal
conditioning are not currently implemented for ACE-Step; the lyric encoder
receives a dummy token.

`--model acestep-turbo` uses the turbo DiT path and runs 8 Euler steps.
`--model acestep-sft` uses the SFT DiT path and runs 50 steps. Both support
metadata conditioning for tempo, key or scale, and time signature.

```bash
cargo run --release -- \
  --model acestep-turbo \
  --backend vulkan \
  --bpm 128 \
  --key-scale "A minor" \
  --time-signature "4/4" \
  --length 10000 \
  --output loop.wav \
  "dark rolling techno groove"
```

The ACE-Step pipeline uses:

- Qwen3 embedding for the caption.
- A 5 Hz LM planner for FSQ audio codes.
- A DiT renderer for 25 Hz latents.
- An Oobleck VAE decoder for 48 kHz stereo audio.

## Model Files

By default, model files are resolved through the Hugging Face cache. Current
expected repositories are:

- `maolandaw/HeartMuLa-happy-new-year-burn`
- `maolandaw/HeartMuLa-RL-oss-3B-20260123`
- `maolandaw/HeartCodec-oss-20260123-burn`
- `maolandaw/ACE-Step-1.5-burn`
- `maolandaw/ACE-Step-1.5-sft-burn`

Use `--model-dir <path>` to bypass Hugging Face lookup and load a local Burn
export layout.

HeartMuLa directories must include:

- `heartmula.bpk`
- `tokenizer.json`
- `gen_config.json`
- `heartcodec.bpk`

ACE-Step directories must include:

- `qwen3-encoder.bpk`, `qwen3_config.json`, `tokenizer.json`
- `acestep-lm.bpk`, `lm_config.json`, `lm_tokenizer.json`
- `acestep-dit.bpk`, `dit_config.json`
- `acestep-condition.bpk`
- `acestep-vae.bpk`, `vae_config.json`
- `silence_latent.bpk`

## Converting ACE-Step Weights

Convert official safetensors checkpoints into BurnPack files with the bundled
converter:

```bash
cargo run --release --bin acestep_convert -- \
  --component dit \
  --input model.safetensors \
  --output acestep-dit.bpk
```

`--component` accepts `text-encoder`, `lm`, `dit`, `condition`, `vae`, or
`silence`.

To download the official checkpoints from Hugging Face and convert them in one
step:

```bash
bin/convert_acestep.sh /path/to/out
bin/convert_acestep.sh /path/to/out --lm 1.7B
bin/convert_acestep.sh /path/to/out --snapshot-dir /data/Ace-Step1.5
```

## CLI Options

Run `maolan-generate --help` for the full current option list.

Important options:

- `--model <happy-new-year|RL|acestep-turbo|acestep-sft>`
- `--backend <cpu|vulkan>`
- `--model-dir <path>`
- `--output <path>`
- `--lyrics <text>`
- `--tags <text>`
- `--cfg-scale <float>`
- `--length <milliseconds>`
- `--topk <int>`
- `--temperature <float>`
- `--ode-steps <int>`
- `--decode-only`
- `--frames-json <path>`
- `--decode-threads <int>`
- `--decoder-seed <int>`
- `--bpm <float>`
- `--key-scale <text>`
- `--time-signature <N/D>`

## Development

Build and check the crate from `generate/`:

```bash
cargo build
cargo clippy --all-targets
```

Release builds are preferred for real generation runs:

```bash
cargo run --release -- "prompt text"
```

Windows builds require MSVC. The repository includes `build.ps1` for the
Windows packaging path.

- [View on GitHub](https://github.com/maolan/generate)
- [View on crates.io](https://crates.io/crates/maolan-generate)
