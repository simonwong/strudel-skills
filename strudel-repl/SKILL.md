---
name: strudel-repl
description: >
  Write, debug, and explain Strudel REPL code for browser-based live coding music.
  Strudel is a JavaScript port of TidalCycles — a pattern language for algorithmic music.
  Use this skill whenever the user mentions Strudel, TidalCycles, live coding music,
  mini-notation, algorithmic composition, or wants to create music with code in the browser.
  Also trigger on: drum patterns, euclidean rhythms, pattern transformations, sample manipulation,
  synth patches in Strudel, or any question about strudel.cc syntax and functions.
---

# Strudel REPL Skill

You are an expert in Strudel — a browser-based live coding environment for algorithmic music, running at [strudel.cc](https://strudel.cc). You help users write, debug, and understand Strudel code.

## Core Concepts

Strudel expresses music as **patterns** — cyclic sequences of events that repeat every **cycle** (default: 2 seconds at 0.5 CPS). Everything is a pattern: sounds, notes, effects, even random values.

### Quick Start

```js
// Drums — the simplest starting point
sound("bd hh sd hh")

// Notes — letter names or MIDI numbers
note("c e g b").sound("piano")

// Scales — use numbers with scale()
n("0 2 4 6").scale("C:major").sound("piano")

// Stack layers with $:
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
$: note("<c2 bb1 f2 eb2>").sound("gm_synth_bass_1").lpf(800)
```

### Key Controls

- **Ctrl+Enter**: Play / update pattern
- **Ctrl+.**: Stop all sound

## Mini-Notation Reference

Mini-notation is Strudel's compact pattern language. For full details, read `references/mini-notation.md`.

| Syntax | Meaning | Example |
|--------|---------|---------|
| `"a b c"` | Sequence (squished into 1 cycle) | `sound("bd sd hh")` |
| `"<a b c>"` | One per cycle (alternation) | `sound("<bd sd hh>")` |
| `"[a b]"` | Sub-sequence | `sound("bd [sd sd] hh")` |
| `"*n"` | Speed up n times | `sound("hh*8")` |
| `"/n"` | Slow down n times | `note("[c e g]/2")` |
| `"@n"` | Elongate by factor n | `note("c@3 e")` |
| `"!n"` | Replicate n times | `note("c!3 e")` |
| `"~"` or `"-"` | Rest (silence) | `sound("bd ~ sd ~")` |
| `","` | Parallel (stack) | `sound("bd*4, hh*8")` |
| `"?"` | Random removal (50%) | `sound("hh?")` |
| `"|"` | Random choice per cycle | `sound("bd \| sd \| hh")` |
| `"(beats,steps,offset)"` | Euclidean rhythm | `sound("bd(3,8)")` |
| `":n"` | Sample index | `sound("hh:0 hh:1")` |
| `` ` `` | Multi-line pattern | Use backticks for line breaks |

## Essential Functions

### Sound & Notes

- `sound("name")` / `s("name")` — play a named sound or waveform
- `note("c3 e3")` — set pitch by name or MIDI number
- `n("0 2 4").scale("C:major")` — scale degree indexing
- `freq(440)` — set frequency directly
- `bank("RolandTR909")` — select drum machine bank

### Drum Abbreviations

`bd` kick, `sd` snare, `hh` hihat, `oh` open hihat, `rim` rimshot, `cp` clap, `cr` crash, `rd` ride, `ht/mt/lt` toms, `sh` shaker, `cb` cowbell, `tb` tambourine, `perc` percussion, `misc` misc, `fx` effects

### Audio Effects, Envelopes, Synthesis, Signals, Transforms

For complete documentation on audio effects, ADSR/filter/pitch envelopes, FM synthesis, vibrato, continuous modulation (LFO/signals), and pattern transforms — read `references/audio.md` and `references/functions.md`.

### Time & Tempo

```js
setcpm(120/4)    // 120 BPM in 4/4 (30 cycles/min)
setcps(0.5)      // 0.5 cycles per second (default)
```

BPM formula: `setcpm(bpm / beatsPerCycle)`

### Creating Patterns (Functions)

| Function | Mini-notation equivalent |
|----------|--------------------------|
| `cat(a, b)` | `"<a b>"` |
| `seq(a, b)` | `"a b"` |
| `stack(a, b)` | `"a, b"` |
| `stepcat([3,x],[1,y])` | `"x@3 y"` |
| `arrange([4, pat1], [2, pat2])` | Section arrangement |
| `silence` | `"~"` |
| `run(n)` | `"0 1 2 ... n-1"` |

### Tonal Functions

```js
n("0 2 4 6").scale("C:major")        // scale degrees
note("c3 e3 g3").transpose(7)         // transpose by semitones
n("0 2 4").scaleTranspose("<0 1 2>")  // transpose within scale
chord("<Am C F G>").voicing()         // auto voicing with voice leading
"<C^7 Dm7 G7>".rootNotes(2)          // chord root notes
```

Scale format: `"Root:Type"` e.g. `"C:major"`, `"A2:minor"`, `"D:dorian"`, `"F:major:pentatonic"`

### Visualization

- `._scope()` — 显示实时波形/示波器动画（在 REPL 底部）
- `._pitchwheel()` — 显示音高轮可视化
- `.punchcard()` — 显示钢琴卷帘式可视化

### Parallel Patterns with `$:` and MIDI

Use `$:` to run multiple pattern layers simultaneously. Use `_$:` to mute a layer. For MIDI output, see `references/audio.md`.

## Workflow

When helping users:

1. **Understand intent** — Are they building a beat, writing a melody, exploring sounds, or learning syntax?
2. **Start simple** — Begin with a basic pattern and iterate. Don't write 20 lines of code upfront.
3. **Explain the why** — Strudel has non-obvious behaviors (e.g., adding notes speeds them up). Explain tradeoffs.
4. **Use mini-notation first** — It's more concise than function-based patterns. Only use JS functions when mini-notation can't express the idea.
5. **Suggest `.log()` for debugging** — `.log()` shows event timing and parameter values.

## Common Pitfalls

- `note("c e g")` without `.sound()` uses default triangle wave — always set a sound
- Adding more notes in a sequence speeds it up (they're squished into 1 cycle) — use `<>` or `/n` to prevent this
- `n` vs `note`: `n` indexes into scales/samples, `note` names specific pitches
- Effects are single-use per event — duplicates override, not stack
- Parameters are sampled at note onset only — use `.seg(n)` for continuous modulation
- `setcpm(120)` is NOT 120 BPM — it's 120 cycles/min. For 120 BPM in 4/4: `setcpm(120/4)`

## Reference Files

For complete documentation, read these files as needed:

- `references/mini-notation.md` — Full mini-notation syntax with all operators
- `references/functions.md` — Complete function reference (pattern creation, time modifiers, control params, signals, random, conditionals, accumulation, tonal, stepwise)
- `references/audio.md` — Audio effects, synths, samples, and MIDI in detail

### Examples (read on demand)

Start with `references/examples/README.md` for the full index, then load only the relevant module.

**By technique** — load when the user asks about a specific topic:
- `references/examples/drums.md` — Drum patterns (basic to breakbeat)
- `references/examples/euclidean.md` — Euclidean rhythms (tresillo, clave, etc.)
- `references/examples/melodies.md` — Melodies & basslines
- `references/examples/chords.md` — Chords & voicings
- `references/examples/effects.md` — Audio effects showcase
- `references/examples/transforms.md` — Pattern transforms (off, echo, iter, etc.)
- `references/examples/modulation.md` — Continuous modulation / LFO
- `references/examples/synths.md` — Synth engines (FM, wavetable, additive)
- `references/examples/samples.md` — Sample loading, slicing, granular
- `references/examples/midi.md` — MIDI output
- `references/examples/parallel.md` — Parallel patterns with `$:`
- `references/examples/visualization.md` — Scope, punchcard, pitchwheel
- `references/examples/workflow.md` — Debug, tempo, arrangement

**By music genre** — load when the user mentions a style:
- `references/examples/genre/folk.md` — 民谣 / Folk
- `references/examples/genre/soul-rnb.md` — Soul / R&B
- `references/examples/genre/jazz-blues.md` — Jazz / Blues
- `references/examples/genre/electronic.md` — Electronic (Techno/House/Dub/Ambient/DnB)
- `references/examples/genre/rock.md` — Rock (classic/punk/post-rock)
- `references/examples/genre/hiphop-lofi.md` — Hip-Hop / Lo-Fi
- `references/examples/genre/world.md` — World music (African/Latin/Asian/Celtic)
- `references/examples/genre/classical.md` — Classical & contemporary composition
- `references/examples/genre/gamemusic.md` — Game music / Chiptune
- `references/examples/genre/experimental.md` — Experimental & avant-garde

**Full compositions** — load for inspiration or complete examples:
- `references/examples/compositions.md` — Multi-layer pieces (official + community)
