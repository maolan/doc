# AI and Generative Tools

Maolan includes tools for generating audio and MIDI from prompts, along with
neural analysis and resynthesis for pitch correction. Generated material is
created inside an open session and added to the arrangement as a new track.

## Audio generation

The audio generator offers two model families:

- **HeartMuLa** provides the `happy-new-year` and `RL` model options. It
  generates music from a text or lyrics prompt, with optional style tags.
- **ACE-Step 1.5** provides `acestep-turbo` and `acestep-sft` options for
  prompt-driven instrumental generation. The turbo option also lets you choose
  a language-model planner size.

The generator can condition output on tempo, key, and time signature. You can
also adjust duration and generation settings such as guidance scale and step
count. Generated audio is imported into the session as a new audio track.

Generation runs on the CPU or Vulkan backend. Model weights are not bundled
with Maolan and may need to be downloaded on first use; model availability and
hardware requirements vary by model and backend.

## MIDI generation

Maolan offers two prompt-to-MIDI approaches:

- **Text to MIDI** interprets prompt details such as tempo, key, time
  signature, instrument, and style, then creates a MIDI sequence
  deterministically without loading a neural model.
- **MIDI-LLM** uses a Llama 3.2 1B checkpoint fine-tuned with a music-token
  vocabulary to generate MIDI from a text prompt.

Both options can use tempo, key, and time-signature settings. MIDI-LLM also
provides token limit and sampling controls; Text to MIDI provides sequence
length and seed settings. Generated MIDI is imported as a new MIDI track.

## Neural pitch correction

Pitch correction can analyze a vocal clip with the FCPE pitch detector. In
resynthesis mode, Maolan uses the PC-NSF-HiFiGAN vocoder to render audio using
the edited pitch contour while retaining the source timbre. Model weights are
downloaded when needed. This mode requires a working Vulkan GPU; there is no
CPU fallback for the neural pitch models.

Maolan also includes non-neural pitch correction modes. See [Keyboard
Shortcuts and Gestures](./shortcuts.md#pitch-correction) for how to open and
edit pitch correction in the application.
