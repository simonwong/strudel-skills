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

### Audio Effects

| Effect | Function | Example |
|--------|----------|---------|
| Low-pass filter | `lpf` | `.lpf(800)` or `.lpf("400 2000")` |
| High-pass filter | `hpf` | `.hpf(1000)` |
| Band-pass filter | `bpf` | `.bpf(500)` |
| Resonance | `lpq` / `hpq` / `bpq` | `.lpf(800).lpq(10)` |
| Filter type | `ftype` | `.ftype("<0 1 2>")` — 12db/ladder/24db |
| Vowel filter | `vowel` | `.vowel("<a e i o>")` |
| Gain | `gain` | `.gain("[.25 1]*4")` |
| Velocity | `velocity` | `.velocity(".4 1")` |
| Delay | `delay` | `.delay(.5)` |
| Delay time | `delaytime` | `.delay(.5).delaytime(1/4)` |
| Delay feedback | `delayfeedback` | `.delayfeedback(.5)` |
| Reverb | `room` | `.room(.5)` |
| Room size | `roomsize` / `size` | `.room(.8).size(2)` |
| Pan | `pan` | `.pan("0 1")` |
| Stereo width | `jux` | `.jux(rev)` |
| Speed | `speed` | `.speed("<1 2 -1>")` |
| Sample start | `begin` | `.begin(0.25)` |
| Sample end | `end` | `.end(.5)` |
| Cut group | `cut` | `s("[oh hh]*4").cut(1)` |
| Compressor | `compressor` | `.compressor("-20:20:10:.002:.02")` |
| Bit crush | `crush` | `.crush("<16 8 4>")` |
| Distortion | `distort` | `.distort(2)` |
| Phaser | `phaser` | `.phaser(2)` |
| Tremolo | `tremolosync` | `.tremolosync(4)` |

### ADSR Envelope

```js
note("c3 e3 g3").sound("sawtooth")
  .attack(0).decay(.1).sustain(.5).release(.2)
// Or shorthand:
  .adsr("0:.1:.5:.2")
```

### Filter Envelope

```js
note("c2 e2 g2").sound("sawtooth").lpf(300)
  .lpa(.5).lpd(.3).lps(.2).lpr(.1).lpenv(4)
```

### Pitch Envelope

```js
note("c").sound("sine")
  .penv(12).pdec(.5).pcurve(1) // exponential pitch drop
```

### FM Synthesis

```js
note("c e g b").fm(4).fmh("<1 2 1.5>")
  .fmattack(0).fmdecay(.1).fmsustain(.5)
```

### Vibrato

```js
note("a e").vib("<.5 1 2 4>:12")
```

### Signals (Continuous Modulation)

```js
s("hh*16").lpf(sine.range(200, 4000).slow(4))
```

Available signals: `sine`, `cosine`, `saw`, `tri`, `square`, `rand`, `perlin`
Bipolar variants (-1 to 1): `sine2`, `saw2`, etc.

### Pattern Transforms

| Function | Description | Example |
|----------|-------------|---------|
| `fast(n)` | Speed up | `.fast(2)` |
| `slow(n)` | Slow down | `.slow(2)` |
| `rev` | Reverse | `.rev()` |
| `jux(fn)` | Stereo split + transform | `.jux(rev)` |
| `ply(n)` | Repeat each event n times | `.ply(2)` |
| `off(time, fn)` | Offset + transform | `.off(1/8, x=>x.add(7))` |
| `echo(n, time, fb)` | Echo with feedback | `.echo(3, 1/6, .8)` |
| `superimpose(fn)` | Layer with transform | `.superimpose(x=>x.add(2))` |
| `layer(fn...)` | Replace with transforms | `.layer(x=>x.add("0,7"))` |
| `palindrome` | Forward/backward alternation | `.palindrome()` |
| `iter(n)` | Rotate subdivisions | `.iter(4)` |
| `every(n, fn)` | Apply every n cycles | `.every(4, rev)` |
| `sometimes(fn)` | Apply 50% of the time | `.sometimes(x=>x.speed(2))` |
| `often(fn)` | Apply 75% of the time | `.often(x=>x.degrade())` |
| `rarely(fn)` | Apply 25% of the time | `.rarely(x=>x.rev())` |
| `degradeBy(p)` | Random removal by probability | `.degradeBy(0.3)` |
| `chunk(n, fn)` | Apply fn to nth part | `.chunk(4, x=>x.add(7))` |
| `struct(pattern)` | Apply rhythm structure | `.struct("x ~ x ~")` |
| `mask(pattern)` | Mute where mask is 0 | `.mask("<1 0>")` |
| `add(n)` | Add to pitch | `.add(7)` |
| `range(lo, hi)` | Remap 0..1 to lo..hi | `sine.range(200, 4000)` |

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

### Samples

```js
// Load custom samples
samples({ mydrum: 'path/to/file.wav' }, 'https://base-url/')
samples('github:user/repo')  // GitHub shortcut with strudel.json

// Granular
s("rhodes").chop(4).rev().loopAt(2)

// Slicing
s("breaks165").slice(8, "0 1 2 3 4 5 6 7")

// Loop
s("casio").loop(1).loopBegin(0).loopEnd(.5)
```

### Visualization

- `._scope()` — 显示实时波形/示波器动画（在 REPL 底部）
- `._pitchwheel()` — 显示音高轮可视化
- `.punchcard()` — 显示钢琴卷帘式可视化

### MIDI Output

```js
note("c a f e").midi('IAC Driver')
chord("<C^7 Dm7 G7>").voicing().midi()
```

### Parallel Patterns with `$:`

```js
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
$: note("<c2 bb1 f2 eb2>").sound("gm_synth_bass_1").lpf(800)
$: n("0 2 4 <6 7>").scale("C4:minor").sound("piano")

// Mute with _$
_$: note("<c2 bb1>").sound("gm_synth_bass_1")
```

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
- `references/examples.md` — Curated examples from simple beats to full compositions
