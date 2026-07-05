# soemdsp-rsmet

DSP modules built in the lineage of Robin Schmidt (RS-MET) designs,
compiled to native WebAssembly.

## Build target

`--target=wasm32 -O3 -nostdlib -fno-exceptions -fno-rtti`. Compiled
with clang++.

## Modules

| Module | Export prefix | `_sample` parameters | Return / getters | Reference |
|---|---|---|---|---|
| Passive Filter | `soemdsp_passive_filter` | `input, mode (0=LP/1=HP/2=BP), lowFrequency, highFrequency, sampleRate` | `double` (direct return) | LP mode matches RS-MET's `OnePoleFilter` `LOWPASS_IIT` coefficient formula (`a1 = exp(-w); b0 = 1 - a1`); HP mode matches its matched-Z-transform highpass (`b0 = 0.5*(1+a1)`), BP cascades both: https://github.com/RobinSchmidt/RS-MET/blob/work/Libraries/RobsJuceModules/rapt/Filters/General/OnePoleFilter.h |
| Ladder Filter | `soemdsp_ladder_filter` | `input, frequency, resonance, mode (0-3), stages, sampleRate` | `double` (direct return) | RS-MET general-purpose ladder design |
| RSMET Filter | `soemdsp_rsmet_filter` | `input, frequency (0-1 normalized), resonance (0-1 normalized), chaosAmount (0-1), mode (0-9), sampleRate` | `double` (direct return) | Ladder + tanh soft clip + noise injection, exponential frequency/resonance response curves |
| TB-303 Filter | `soemdsp_tb303_filter` | `input, cutoff, resonance, mode, drive, sampleRate` | `double` (direct return) | Robin Schmidt's TeeBeeFilter (RS-MET / Open303): https://github.com/RobinSchmidt/RS-MET |
| RobinSupersaw | `soemdsp_robin_supersaw` | `frequencyHz, sampleRate, detuneCents, voices, level` | `_left(handle)`, `_right(handle)`, `_mono(handle)` | Direct transcription of RS-MET's `PitchDitherOscs`: https://github.com/RobinSchmidt/RS-MET/blob/work/Libraries/RobsJuceModules/rapt/Generators/PitchDitherOscs.h |

`Passive Filter`, `Ladder Filter`, `RSMET Filter`, and `TB-303 Filter`
export `create(handle)`/`destroy(handle)`/`sample(...)`/`version()`.
`RobinSupersaw` additionally exports `reset(handle)`.

## RobinSupersaw implementation note

Instead of bandlimiting a sawtooth via PolyBLEP correction or a DSF
closed form, cycle length is dithered in the time domain: each cycle
randomly selects one of 3 neighboring integer sample-counts
(`lenMid-1, lenMid, lenMid+1`) with probabilities computed so the
long-run average cycle length equals the desired fractional length.
Up to 9 independently-dithered, detuned voices are summed per call.
Max voice count: `kMaxVoices`.

## Attribution

Passive Filter, Ladder Filter, RSMET Filter, TB-303 Filter, and
RobinSupersaw are all derived from Robin Schmidt's (RS-MET) published
work.
