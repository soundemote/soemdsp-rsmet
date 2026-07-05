# soemdsp-rsmet

A home for RS-MET-lineage filter work: native C++/WebAssembly ports built
in the style of Robin Schmidt's RS-MET DSP designs.

Starting simple, on purpose. **Passive Filter** — a 1-pole RC filter in
three flavors (LP, HP, BP) — is the first thing in here: the plainest,
oldest circuit in the book, the kind of filter you'd find in an analog
textbook before anyone put a name on it. Everything that lands in this
repo going forward earns its place the same way that one did: it has to
actually sound like something, not just simulate one.

## What's here now

- `native_modules/passive_filter/` — 1-pole RC filter, LP/HP/BP modes,
  compiled to a dependency-free WebAssembly module (`.cpp` source +
  `.wasm` binary).

More filters are staged for this line and will land here as the
lineup gets finalized.
