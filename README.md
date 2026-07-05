# soemdsp-rsmet

Filters built in the lineage of Robin Schmidt's (RS-MET) DSP designs --
plus one plain circuit that started the whole thing.

## What's here

- **Passive Filter** — a 1-pole RC filter in three modes (LP, HP, BP).
  Not RS-MET's design, just the plainest, oldest circuit in the book --
  the filter every other filter here eventually gets compared back to.
- **Ladder Filter** — the general-purpose RS-MET-lineage ladder design,
  gain-compensated, resonant stages.
- **RSMET Filter** — a ladder filter preceded by a tanh soft clipper and
  noise injection stage, exponential frequency/resonance curves, 10 modes.
- **TB-303 Filter** — based on Robin Schmidt's TeeBeeFilter (RS-MET /
  Open303): feedback highpass, resonance skewing, 15 output modes
  (LP/HP/BP at 6/12/18/24 dB/octave).

Each compiled to a dependency-free WebAssembly module under
`native_modules/`.

## Attribution

Ladder Filter, RSMET Filter, and TB-303 Filter are built in the lineage
of Robin Schmidt's (RS-MET) published filter designs, including
TeeBeeFilter / Open303. Credited here explicitly -- these three are not
original designs.
