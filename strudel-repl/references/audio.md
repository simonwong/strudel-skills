# Strudel Audio Reference: Effects, Synths, Samples, MIDI

## Signal Chain Order

Effects apply in this fixed order (duplicates override, not stack):
Phase vocoder → Gain/ADSR → LPF → HPF → BPF → Vowel → Coarse → Crush → Shape → Distort → Tremolo → Compressor → Pan → Phaser → Postgain → Dry/Delay/Reverb sends → Orbit (duck) → Mixer

## Filters

### Low-pass: `lpf` (synonyms: `cutoff`, `ctf`, `lp`)
- Frequency: 0-20000 Hz
- Resonance: `lpq` (synonyms: `resonance`), 0-50
- Mini-notation: `"1000:10"` sets lpf=1000, lpq=10

### High-pass: `hpf` (synonyms: `hp`, `hcutoff`)
- Resonance: `hpq` (synonyms: `hresonance`)

### Band-pass: `bpf` (synonyms: `bandf`, `bp`)
- Resonance: `bpq` (synonyms: `bandq`)

### Filter type: `ftype`
- `0` = 12db, `1` = ladder (aggressive), `2` = 24db

### Vowel: `vowel`
Values: `a e i o u ae aa oe y uh un en an on`

## ADSR Envelope

- `attack` / `att` — time to peak (seconds)
- `decay` / `dec` — time to sustain level
- `sustain` / `sus` — sustain level (0-1)
- `release` / `rel` — time to zero after offset
- `adsr("a:d:s:r")` — shorthand

## Filter Envelopes

Prefix with `lp`, `hp`, or `bp`:
- `lpattack`/`lpa`, `lpdecay`/`lpd`, `lpsustain`/`lps`, `lprelease`/`lpr`
- `lpenv`/`lpe` — modulation depth (0 to n)
- Same pattern for `hp*` and `bp*`

## Pitch Envelope

- `pattack`/`patt`, `pdecay`/`pdec`, `prelease`/`prel`
- `penv` — semitones of pitch change
- `pcurve` — 0=linear, 1=exponential
- `panchor` — 0=up from note, 1=down from note

## Amplitude Modulation (Tremolo)

- `tremolosync`/`tremsync` — speed in cycles
- `tremolodepth`/`tremdepth` — depth
- `tremoloskew`/`tremskew` — waveform shape (0-1)
- `tremolophase`/`tremphase` — phase offset
- `tremoloshape`/`tremshape` — `tri|square|sine|saw|ramp`

## Dynamics

- `gain` — exponential volume (0-1+)
- `velocity`/`vel` — velocity (0-1), multiplied with gain
- `compressor` — `"threshold:ratio:knee:attack:release"`
- `postgain` — gain after all effects

## Panning

- `pan` — stereo position (0=left, 1=right)
- `jux(fn)` — original left, modified right
- `juxBy`/`juxby` — jux with adjustable width (0=mono, 1=full)

## Waveshaping

- `coarse` — fake sample rate reduction (Chromium only)
- `crush` — bit crusher (1=drastic, 16=minimal)
- `distort`/`dist` — waveshaping distortion. Optional: `"amount:postgain:type"`

## Delay (Global — per orbit)

- `delay` — send level (0-1). Mini-notation: `"level:time:feedback"`
- `delaytime`/`delayt`/`dt` — time in seconds
- `delayfeedback`/`delayfb`/`dfb` — feedback (0-1, >=1 = infinite!)

## Reverb (Global — per orbit)

- `room` — send level (0-1). Mini-notation: `"level:size"`
- `roomsize`/`rsize`/`size` — room size (0-10)
- `roomfade`/`rfade` — fade time (seconds)
- `roomlp`/`rlp` — lowpass frequency (Hz)
- `roomdim`/`rdim` — lowpass at -60dB (Hz)
- `iresponse`/`ir` — impulse response sample

## Phaser (Global — per orbit)

- `phaser`/`ph` — modulation speed
- `phaserdepth`/`phd` — depth (0-1, default 0.75)
- `phasercenter`/`phc` — center frequency (Hz, default 1000)
- `phasersweep`/`phs` — sweep range (default 2000)

## Duck / Sidechain (Global)

- `duckorbit`/`duck` — target orbit. Mini-notation: `"2:3"` for multiple
- `duckattack`/`duckatt`/`datt` — recovery time
- `duckdepth` — amount (0-1)

## Orbits

Orbits group patterns for shared global effects (delay, reverb, duck).
- `orbit`/`o` — set orbit number (default 1)
- Same orbit = shared delay/reverb. Different orbits = independent.
- Multiple orbits create copies — reduce gain to avoid clipping.

## Synths

### Basic Waveforms
`sine`, `sawtooth`, `square`, `triangle` — selected via `sound()`/`s()`

Default: if `note` set without `sound`, uses `triangle`.

### Noise Sources
`white`, `pink`, `brown` — from hard to soft.
- `noise` param adds pink noise to oscillator
- `crackle` type — controlled via `density`

### Additive Synthesis
- `partials([magnitudes])` — harmonic magnitudes relative to fundamental
- `phases([phases])` — phase of each harmonic
- `sound("user")` — custom waveform from partials

### Vibrato
- `vib`/`vibrato`/`v` — frequency (Hz). Mini-notation: `"freq:depth"`
- `vibmod`/`vmod` — depth in semitones. Mini-notation: `"depth:freq"`

### FM Synthesis
- `fm` — modulation index
- `fmh` — harmonicity ratio (integer=harmonic, decimal=metallic)
- `fmattack`/`fmatt`, `fmdecay`/`fmdec`, `fmsustain`/`fmsus`, `fmenv`/`fme`
- Per-operator: `fmh2`, `fmatt5`, `fmdec6`, etc. (up to 8 operators)

### Wavetable Synthesis
Samples prefixed with `wt_` auto-loop as wavetables. Use `loopBegin`/`loopEnd` to scan.

### ZZFX (Zuper Zmall Zound Zynth)
20-parameter synth for game-style sounds:
```js
note("c2 eb2 f2 g2")
  .s("{z_sawtooth z_tan z_noise z_sine z_square}%4")
  .curve(1).slide(0).zmod(0).zcrush(0).zdelay(0)
  .pitchJump(0).pitchJumpTime(0).lfo(0).tremolo(0.5)
```

## Samples

### Default Sounds
Built-in: `insect`, `wind`, `jazz`, `metal`, `east`, `crow`, `casio`, `space`, `numbers`
VCSL instruments loaded by default.

### Drum Machines
Banks: `RolandTR808`, `RolandTR909`, `RolandTR707`, `RolandTR505`, `AkaiLinn`, `RhythmAce`, `ViscoSpaceDrum`, `RolandCompurhythm1000`
```js
s("bd sd,hh*8").bank("RolandTR909")
```

### Loading Custom Samples

From URLs:
```js
samples({ name: 'path/to/file.wav' }, 'https://base-url/')
```

From strudel.json:
```js
samples('https://url/to/strudel.json')
```

GitHub shortcut:
```js
samples('github:user/repo')
```

From disk (Import Sounds folder or @strudel/sampler CLI).

### Pitch-mapped Samples
```js
samples({ 'moog': { 'g3': 'moog/G3.wav', 'g4': 'moog/G4.wav' } }, 'base-url')
note("g3 bb3 c4").s("moog").clip(1)
```

### Shabda (freesound.org integration)
```js
samples('shabda:bass:4,hihat:4,rimshot:2')
samples('shabda/speech:hello,world')
```

### Sampler Effects
- `begin(0-1)` / `end(0-1)` — sample start/end point
- `loop(1)` — loop the sample
- `loopBegin`/`loopb` / `loopEnd`/`loope` — loop points
- `cut(group)` — cut group (hi-hat choke)
- `clip(factor)` / `legato` — duration multiplier
- `loopAt(cycles)` — fit sample to N cycles
- `fit()` — fit to event duration
- `chop(n)` — granular: cut into n parts
- `striate(n)` — progressive portions per loop
- `slice(n, pattern)` — chop and trigger by index
- `splice(n, pattern)` — like slice, adjusts speed
- `scrub(position)` — tape-style scrubbing
- `speed(n)` — playback speed (negative = reverse)

### Custom Aliases
```js
soundAlias('RolandTR808_bd', 'kick')
```

## MIDI Output

### Basic
```js
note("c a f e").midi('IAC Driver')
```

### Options
```js
.midi('IAC Driver', {
  isController: false,  // true = no note messages
  latencyMs: 34,        // align with audio
  midichannel: 1,       // 1-16
  velocity: 0.9,        // default velocity
  midimap: 'default'    // CC mapping name
})
```

### MIDI Functions
- `midiport(device)` — select output device
- `midichan(n)` — select channel (1-16)
- `midicmd("clock|start|stop|continue")` — transport control
- `ccn(n)` / `ccv(value)` — control change number/value
- `control([ccn, ccv])` — combined CC
- `progNum(n)` — program change (0-127)
- `sysex(id, data)` / `sysexid(id)` / `sysexdata(data)` — system exclusive
- `midibend(value)` — pitch bend (-1 to 1)
- `miditouch(value)` — aftertouch (0 to 1)

### MIDI Input
```js
const cc = await midin('Device Name')
note("c a f e").lpf(cc(0).range(0, 1000))

const kb = await midikeys('Device Name')
kb().s("tri").lpf(80)
```

### MIDI Maps
```js
midimaps({ mymap: { lpf: 74 } })
defaultmidimap({ lpf: 74 })
```

### OSC
```js
Pattern.osc()  // send haps as OSC messages
```

### MQTT
```js
Pattern.mqtt('broker-url', 'topic')
```
