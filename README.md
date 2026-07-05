# soemdsp-rsmet

DSP built in the lineage of Robin Schmidt's (RS-MET) work -- plus one
plain circuit that started the whole thing.

## What's here

- **Passive Filter** — a 1-pole RC filter in three modes (LP, HP, BP).
  Not RS-MET's design, just the plainest, oldest circuit in the book --
  the filter every other thing here eventually gets compared back to.
- **Ladder Filter** — the general-purpose RS-MET-lineage ladder design,
  gain-compensated, resonant stages.
- **RSMET Filter** — a ladder filter preceded by a tanh soft clipper and
  noise injection stage, exponential frequency/resonance curves, 10 modes.
- **TB-303 Filter** — based on Robin Schmidt's TeeBeeFilter (RS-MET /
  Open303): feedback highpass, resonance skewing, 15 output modes
  (LP/HP/BP at 6/12/18/24 dB/octave).
- **RobinSupersaw** — a direct transcription of Robin Schmidt's pitch
  dithering technique (RS-MET's `PitchDitherOscs`): instead of a
  bandlimited sawtooth built via PolyBLEP correction or a DSF closed
  form, this oscillator dithers its own cycle length in the time domain,
  stacking up to 9 independently-dithered, detuned voices into a
  wall-of-saws supersaw.

Each compiled to a dependency-free WebAssembly module under
`native_modules/`.

## Attribution

Ladder Filter, RSMET Filter, TB-303 Filter, and RobinSupersaw are all
built directly on Robin Schmidt's (RS-MET) published designs --
TeeBeeFilter / Open303 for the filters, `PitchDitherOscs` for
RobinSupersaw. Credited here explicitly -- none of these four are
original designs.
