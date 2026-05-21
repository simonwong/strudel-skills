# Strudel Compositions

Complete, multi-layer Strudel compositions demonstrating various techniques and genres.

---

## Official strudel.cc Examples (adapted)

Examples adapted from the official Strudel documentation, with Chinese+English technique annotations.

### Giant Steps

Giant Steps — John Coltrane 经典爵士曲
Techniques: chord voicings, scale transposition, multi-layer arrangement

```js
// Adapted from strudel.cc official "giantSteps" example
// 巨人的步伐 — John Coltrane 经典爵士曲
// 展示：chord voicings、scale transposition、多层编排
let chords = chord(`<
  [B^7 D7] [G^7 Bb7] [Eb^7 Am7 D7]
  [G^7 Bb7] [Eb^7 F#7] [B^7 Fm7 Bb7]
  [Eb^7 Am7] [D7] [G^7 C#7] [F#7 Fm7]
  [Bb7] [Eb^7 F#7] [B^7 Fm7] [Bb7 Eb^7] [Am7 D7]
>*2`).dict('ireal')

$: n("2 4 3 2 4 2 4 3 2 0 2 1 0").set(chords).voicing()
  .s("piano").room(.3).gain(.4)
$: chords.struct("[~ x]*2").voicing().s("piano").room(.4).gain(.25)
$: n("0 - 1 - 2 - 1 -").set(chords).mode("root:g2").voicing()
  .s("gm_acoustic_bass").clip(.8)
```

### Barry Harris Bebop

Barry Harris bebop 练习 — 展示 bebop 音阶线条
Techniques: bebop scale runs, fast note sequences

```js
// Barry Harris bebop 练习 — 展示 bebop 音阶线条
n("<0 2 4 5 6 4 2 0>").scale("C4:bebop major")
  .sound("piano").fast(2).room(.3)
```

### Belldub

Belldub — Dub 制作技巧：延迟反馈 + 共振滤波
Techniques: delay feedback, resonant filter sweeps, bell synthesis

```js
// Belldub — Dub 制作技巧：延迟反馈 + 共振滤波
$: note("c4 eb4 g4 bb4").sound("bell").delay(.5).delayfeedback(.6)
  .lpf(sine.range(500, 3000).slow(4)).lpq(12)
$: sound("bd rim").bank("RolandTR707").delay(.5)
$: note("<c2 eb2>").sound("sawtooth").lpf(600).room(.5)
```

### Caverave

Caverave — 多层电子舞曲
Techniques: four-on-the-floor kick, hi-hat gain pattern, filter sweep on bass

```js
// Caverave — 多层电子舞曲
setcpm(140/4)
$: sound("bd*4").bank("RolandTR909")
$: sound("hh*16").gain("[.15 1]*8").bank("RolandTR909")
$: note("<c2 eb2 f2 g2>").sound("sawtooth").lpf(sine.range(200, 3000).slow(2)).lpq(15)
$: chord("<Cm7 Fm7>").voicing().s("square").room(.4).gain(.2)
```

### Dinofunk

Dinofunk — Funk 编排：贝斯 + 和弦 + 旋律
Techniques: pentatonic bass line, chord voicings, delayed melody

```js
// Dinofunk — Funk 编排：贝斯 + 和弦 + 旋律
$: n("0 0 3 0 5 0 3 0").scale("C2:minor:pentatonic")
  .sound("gm_synth_bass_1").lpf(800).clip(.6)
$: chord("<Cm7 Fm7 Bb7 Eb^7>").struct("[~ x]*2")
  .voicing().s("gm_electric_piano:1").room(.4)
$: n("7 5 3 0 ~ 3 5 7").scale("C4:minor:pentatonic")
  .sound("sawtooth").lpf(2000).delay(.3).gain(.3)
```

### Amensister

Amensister — Amen break 操控 + 贝斯 + 和弦
Techniques: breakbeat slicing, random speed variation, sample loading from GitHub

```js
// Amensister — Amen break 操控 + 贝斯 + 和弦
samples('github:tidalcycles/dirt-samples')
$: s("breaks165").slice(8, "0 1 2 3 4 5 6 7").speed(rand.range(0.9, 1.1))
$: note("<c2 ~ g2 ~>").sound("sawtooth").lpf(600).gain(.5)
$: chord("<Cm7 ~ Fm7 ~>").voicing().s("piano").room(.5).gain(.3)
```

### Random Bells

Random bells — 欧几里得节奏 + 随机音高
Techniques: Euclidean rhythms, random note generation, degradeBy for sparse patterns

```js
// Random bells — 欧几里得节奏 + 随机音高
$: n(irand(12)).scale("C4:minor:pentatonic").sound("gm_kalimba")
  .degradeBy(0.3).room(.6).gain(.3)
$: sound("bd(3,8)").bank("RolandTR707").gain(.4)
$: n("0 ~ 4 ~").scale("C2:minor").sound("gm_acoustic_bass").lpf(400)
```

### SML1

Super Mario World 1-1 风格 — 8-bit chiptune
Techniques: chiptune square wave, fast ascending scale, simple drum pattern

```js
// Super Mario World 1-1 风格 — 8-bit chiptune
setcpm(180/4)
$: n("[0 2 4 5 7 9 11 12]*2").scale("C4:major")
  .sound("square").gain(.25).lpf(3000)
$: sound("bd*2, [~ sd]*2, hh*4").bank("RolandTR505").gain(.3)
```

---

## Community & Original Compositions

Original compositions from the Strudel community and custom demos.

### Coastline

Coastline (by eddyflux) — 海岸线
Techniques: custom sample loading, chord voicings with dict, bass root notes, delayed melody layer

```js
// Coastline (by eddyflux) — 海岸线
samples('github:eddyflux/crate')
setcps(.75)
stack(
  s("bd sd, hh*8").room(.3),
  chord("<Bbm9 Fm9>/4").dict('ireal')
    .voicing().s("gm_electric_piano:2").room(.5),
  n("0").set(chord("<Bbm9 Fm9>/4").dict('ireal'))
    .mode("root:g2").voicing().s("sawtooth").lpf(600),
  n("0 2 4 6").set(chord("<Bbm9 Fm9>/4").dict('ireal'))
    .scale("D5:minor").sound("sawtooth")
    .delay(.5).room(.5).gain(.4)
)
```

### Dub Tune

Dub tune — Dub 音乐
Techniques: muted guitar with delay, accordion melody, layered bass with sawtooth+triangle

```js
// Dub tune — Dub 音乐
$: note("~ [< [d3,a3,f4]!2 [d3,bb3,g4]!2> ~])*2")
    .sound("gm_electric_guitar_muted").delay(.5)
$: sound("bd rim").bank("RolandTR707").delay(.5)
$: n("<4 [3@3 4] [<2 0> ~@16] ~>")
    .scale("D4:minor").sound("gm_accordion:2").room(2).gain(.4)
$: n("[0 [~ 0] 4 [3 2] [0 ~] [0 ~] <0 2> ~]/2")
    .scale("D2:minor").sound("sawtooth,triangle").lpf(800)
```

### Minimal Techno

Minimal techno — 极简 Techno
Techniques: four-on-the-floor kick, gain-pattern hi-hats, clap on offbeats, LFO filter on bass

```js
// Minimal techno — 极简 Techno
setcpm(125/4)
$: sound("bd*4").bank("RolandTR909")
$: sound("hh*16").gain("[.15 1]*8").bank("RolandTR909")
$: sound("~ ~ ~ cp").bank("RolandTR909").room(.4)
$: note("<c2 ~ eb2 ~ f2 ~ g2 ~>").sound("sawtooth")
  .lpf(sine.range(200, 2000).slow(8))
```

### Ambient Soundscape

Ambient soundscape — 氛围音景
Techniques: slow pad chords with long reverb, sparse bass, rimshot as texture element

```js
// Ambient soundscape — 氛围音景
setcpm(60/4)
$: note("<[c4,e4,g4] [a3,c4,e4] [f3,a3,c4] [g3,b3,d4]>/4")
  .sound("gm_pad_new_age").room(1).size(8).gain(.3)
$: n("0 ~ 2 ~ 4 ~ ~ ~").scale("C3:minor")
  .sound("gm_synth_bass_1").lpf(400).gain(.3)
$: sound("rim ~ ~ ~ ~ ~ ~ ~").room(.8).size(5).gain(.15)
```

### Acid Bass

Acid bass — 酸性贝斯
Techniques: resonant filter sweep, distortion, TB-303 style bass line

```js
// Acid bass — 酸性贝斯
setcpm(130/4)
$: note("<c2 eb2 f2 g2 bb2 c3>").sound("sawtooth")
  .lpf(sine.range(200, 4000).slow(2))
  .lpq(15).distort(1.5).gain(.5)
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
```

### Jazz Trio

Jazz trio — 爵士三重奏
Techniques: ii-V-I progression, walking bass via voicing mode, swing feel drums

```js
// Jazz trio — 爵士三重奏
setcpm(100/4)
$: chord("<Dm7 G7 C^7 A7>").voicing()
  .s("gm_electric_piano:1").room(.5).gain(.35)
$: n("0 - 1 - 2 - 1 -").set(chord("<Dm7 G7 C^7 A7>"))
  .mode("root:c2").voicing().s("gm_acoustic_bass").clip(.8)
$: sound("bd ~ sd ~, hh*4").bank("RhythmAce").gain(.3).room(.3)
```

### Reggae

Reggae — 雷鬼
Techniques: jux(rev) for stereo guitar, offbeat rhythm, simple bass line

```js
// Reggae — 雷鬼
setcpm(75/4)
$: note("<[c4,e4,g4] ~ [bb3,d4,f4] ~>")
  .sound("gm_electric_guitar_muted").jux(rev)
  .delay(.5).room(.4)
$: sound("~ ~ sd ~, hh ~ hh ~").bank("RolandTR707")
$: note("<c2 ~ bb1 ~>").sound("gm_synth_bass_1").lpf(500)
```

### Getting Started Demo

Getting started demo — 入门演示
Techniques: custom sample map, perlin noise modulation, off-pattern with degradeBy, chord voicings with lefthand, superimpose for detune, cutoff LFO

```js
// Getting started demo — 入门演示
samples({
  bd: ['bd/BT0AADA.wav','bd/BT0AAD0.wav'],
  sd: ['sd/rytm-01-classic.wav','sd/rytm-00-hard.wav'],
  hh: ['hh27/000_hh27closedhh.wav'],
}, 'github:tidalcycles/dirt-samples')

stack(
  s("bd,[~ <sd!3 sd(3,4,2)>],hh*8")
    .speed(perlin.range(.7,.9)),
  "<a1 b1*2 a1(3,8) e2>"
    .off(1/8, x=>x.add(12).degradeBy(.5))
    .add(perlin.range(0,.5))
    .superimpose(add(.05))
    .note().decay(.15).sustain(0)
    .s('sawtooth').gain(.4)
    .cutoff(sine.slow(7).range(300,5000)),
  "<Am7!3 <Em7 E7b13 Em7 Ebm7b5>>"
    .voicings('lefthand')
    .superimpose(x=>x.add(.04))
    .add(perlin.range(0,.5))
    .note().s('sawtooth').gain(.16)
    .cutoff(500).attack(1)
).slow(3/2)
```
