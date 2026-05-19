# Strudel Examples — From Simple to Complex

## Basic Drum Patterns

### Simple beat
```js
sound("bd hh sd hh")
```

### Rock beat
```js
setcpm(100/4)
sound("[bd sd]*2, hh*8").bank("RolandTR505")
```

### Classic house
```js
sound("bd*4, [- cp]*2, [- hh]*4").bank("RolandTR909")
```

### We Will Rock You
```js
setcpm(81/2)
sound("bd*2 cp").bank("RolandTR707")
```

### TR-808 pattern
```js
setcpm(88/4)
sound(`
[-  -  -  - ] [-  -  -  - ] [-  -  -  - ] [-  -  oh:1 - ],
[hh hh hh hh] [hh hh hh hh] [hh hh hh hh] [hh hh -  - ],
[-  -  -  - ] [cp -  -  - ] [-  -  -  - ] [~  cp -  - ],
[bd bd -  - ] [-  -  bd - ] [bd bd - bd ] [-  -  -  - ]
`).bank("RolandTR808")
```

### 16-step sequencer style
```js
setcpm(90/4)
sound(`
[-  -  oh - ] [-  -  -  - ] [-  -  -  - ] [-  -  -  - ],
[hh hh -  - ] [hh -  hh - ] [hh -  hh - ] [hh -  hh - ],
[-  -  -  - ] [cp -  -  - ] [-  -  -  - ] [cp -  -  - ],
[bd -  -  - ] [-  -  -  bd] [-  -  bd - ] [-  -  -  bd]
`)
```

### Non-standard percussion
```js
setcpm(100/2)
s(`jazz*2,
insect [crow metal] - -,
- space:4 - space:1,
- wind`)
```

### Syncopated funk beat
```js
setcpm(110/4)
sound("bd [~ bd] [~ bd] bd, ~ ~ ~ cp, hh*16").bank("RolandTR909")
```

### Reggae one-drop
```js
setcpm(80/4)
sound("bd ~ ~ ~, ~ ~ cp ~, hh ~ hh ~").bank("RolandTR707")
```

### Breakbeat
```js
setcpm(130/4)
sound("bd*2 [~ sd] bd [~ sd], hh*8").bank("RolandTR909")
```

## Euclidean Rhythms

```js
// Cuban tresillo
sound("bd(3,8)")

// Multiple euclidean layers
sound("bd(3,8), hh(5,8), sd(2,8)")

// With rotation
sound("bd(3,8,0), hh(5,8,2)")

// Afro-Cuban bell pattern
sound("cb(5,8)")

// Samba percussion
sound("bd(3,16), sd(2,16,4), hh(5,16)")

// West African timeline (standard pattern)
sound("bell(3,4,1)")

// Aksak rhythm
sound("bd(5,8)")

// Cuban clave
sound("clave(3,8,2)")

// Layered euclidean with different rotations
sound("bd(5,16,0), sd(5,16,4), hh(5,16,8), cp(5,16,12)")
```

## Melodies & Basslines

### Simple melody with letters
```js
note("c e g b").sound("piano")
```

### Using scale degrees
```js
n("0 2 4 <[6,8] [7,9]>").scale("C:minor").sound("piano")
```

### Classy bassline
```js
note("<[c2 c3]*4 [bb1 bb2]*4 [f2 f3]*4 [eb2 eb3]*4>")
  .sound("gm_synth_bass_1").lpf(800)
```

### Classy melody
```js
n(`<
[~ 0] 2 [0 2] [~ 2]
[~ 0] 1 [0 1] [~ 1]
[~ 0] 3 [0 3] [~ 3]
[~ 0] 2 [0 2] [~ 2]
>*4`).scale("C4:minor").sound("gm_synth_strings_1")
```

### Shuffle groove with @
```js
setcpm(60)
n("<[4@2 4] [5@2 5] [6@2 6] [5@2 5]>*2")
  .scale("<C2:mixolydian F2:mixolydian>/4")
  .sound("gm_acoustic_bass")
```

### Arpeggiated pattern
```js
n("0 2 4 6 4 2").scale("C4:minor").sound("piano").fast(2)
```

### Melody with rests
```js
n("0 ~ 2 ~ 4 ~ 6 ~").scale("C4:major").sound("gm_flute")
```

### Walking bass
```js
n("<0 1 2 3 4 3 2 1>").scale("C2:major:pentatonic")
  .sound("gm_acoustic_bass").clip(0.8)
```

### Ambient pad with long notes
```js
n("0 4 7 12").scale("C3:minor").sound("gm_pad_new_age")
  .slow(4).room(0.8).size(4)
```

### Pentatonic melody
```js
n("0 2 4 0 2 4 6 4").scale("A4:minor:pentatonic")
  .sound("gm_kalimba")
```

### Melody with octave jumps
```js
n("0 2 4 7 12 7 4 2").scale("C4:major").sound("piano")
  .sometimes(x => x.add(12))
```

### Call and response
```js
$: n("<0 2 4 2> ~ ~ ~").scale("C4:major").sound("piano")
$: n("~ ~ ~ <4 2 0 ~>").scale("C4:major").sound("piano")
```

### Simple bass pattern
```js
note("<c2 ~ e2 ~ g2 ~ e2 ~>").sound("gm_synth_bass_1").lpf(600)
```

### Ascending/descending scale
```js
n("0 1 2 3 4 5 6 7 6 5 4 3 2 1 0").scale("C4:major").sound("piano")
```

## Chords & Voicings

### Simple chord progression
```js
chord("<Am C F G>").voicing().room(.5)
```

### Jazz voicings with bass
```js
"<C^7 A7b13 Dm7 G7>*2".layer(
  x => x.voicings('lefthand').struct("[~ x]*2").note(),
  x => x.rootNotes(2).note().s('sawtooth').cutoff(800)
)
```

### Jazz blues in F
```js
let chords = chord(`<
F7 Bb7 F7 [Cm7 F7]
Bb7 Bo F7 [Am7 D7]
Gm7 C7 [F7 D7] [Gm7 C7]
>`)

$: n("7 8 [10 9] 8").set(chords).voicing().dec(.2)
$: chords.struct("- x - x").voicing().room(.5)
$: n("0 - 1 -").set(chords).mode("root:g2").voicing()
```

### Chord melody
```js
chord("<C Am F G>").voicing().s("piano").room(.4)
  .struct("[~ x] [x ~] [~ x] [x ~]")
```

### Piano voicings
```js
chord("<Dm7 G7 C^7>").voicings('lefthand').note()
  .s("piano").room(.5)
```

### Shell voicings
```js
chord("<Dm7 G7 C^7>").voicing({ mode: 'below', anchor: 'c4' }).note()
  .s("piano")
```

### Right hand voicings
```js
chord("<Dm7 G7 C^7>").voicings('righthand').note()
  .s("piano").room(.3)
```

### Rootless voicings
```js
chord("<Am7 Dm7 G7 C^7>").voicings('lefthand').note()
  .s("gm_electric_piano:1").room(.5)
```

### Chord + bass unison
```js
$: chord("<F^7 E7b9 Am7 Abm7 Db7 C^7>").voicing().s("piano").room(.5)
$: n("0 - - -").set(chord("<F^7 E7b9 Am7 Abm7 Db7 C^7>"))
  .mode("root:c2").voicing().s("sawtooth").lpf(600)
```

### Bossa nova chords
```js
chord("<Dm7 G7 C^7 F^7>").struct("[x ~ x ~] [~ x ~ x]")
  .voicing().s("piano").room(.4)
```

## Effects Showcase

### Filter sweep
```js
note("<[c2 c3]*4 [bb1 bb2]*4 [f2 f3]*4 [eb2 eb3]*4>")
  .sound("sawtooth").lpf("200 1000 200 1000")
```

### Vowel formants
```js
note("<[c3,g3,e4] [bb2,f3,d4] [a2,f3,c4] [bb2,g3,eb4]>")
  .sound("sawtooth").vowel("<a e i o>")
```

### Dynamic hihats with gain
```js
sound("hh*16").gain("[.25 1]*4")
```

### Delay and reverb
```js
sound("bd rim bd cp").delay(.5).room(.5)
```

### Stereo panning
```js
sound("numbers:1 numbers:2 numbers:3 numbers:4")
  .pan("0 0.3 .6 1")
```

### Reverse and jux
```js
n("0 1 [4 3] 2 0 2 [~ 3] 4").sound("jazz").jux(rev)
```

### Delay with feedback
```js
sound("bd rim").delay(.5).delaytime(1/4).delayfeedback(.6)
```

### Phaser
```js
note("c3").sound("sawtooth").phaser(2).phaserdepth(.8)
```

### Tremolo
```js
note("c3").sound("triangle").tremolosync(4).tremolodepth(.8)
```

### Bit crush
```js
sound("bd sd").crush("<16 8 4 2>")
```

### Distortion
```js
note("e3").sound("sawtooth").distort(2).lpf(2000)
```

### Resonant filter
```js
note("c3").sound("sawtooth").lpf(800).lpq(20)
```

### Compressor
```js
sound("bd*4, sd*2, hh*8").compressor("-20:10:5:.002:.05")
```

### Combining effects
```js
note("c3 e3 g3").sound("sawtooth")
  .lpf(1000).room(.5).delay(.3).pan("0 .5 1")
```

### Filter type switching
```js
note("c3").sound("sawtooth").lpf(800).ftype("<0 1 2>")
```

### Heavy reverb
```js
sound("bd ~ ~ ~").room(1).size(10).roomlp(3000)
```

### Sidechain ducking
```js
$: sound("bd*4").duckorbit(2)
$: note("c3").sound("sawtooth").orbit(2).duckdepth(.8)
```

### Auto-pan with jux
```js
s("hh*8").jux(rev).juxBy(0.5, x => x.speed(2))
```

## Pattern Transforms

### Offset with add
```js
n("0 [4 <3 2>] <2 3> [~ 1]")
  .off(1/16, x=>x.add(4))
  .scale("C:minor").sound("piano")
```

### Echo
```js
s("bd sd").echo(3, 1/6, .8)
```

### Iteration
```js
note("0 1 2 3".scale('A minor')).iter(4)
```

### Sometimes
```js
s("hh*8").sometimes(x=>x.speed("0.5"))
```

### Chunk processing
```js
"0 1 2 3".chunk(4, x=>x.add(7)).scale("A:minor").note()
```

### Every
```js
n("0 1 2 3").scale("C:minor").every(4, rev).sound("piano")
```

### Fast and slow
```js
sound("bd sd hh cp").fast(2) // double speed
sound("bd sd hh cp").slow(2) // half speed
```

### Superimpose
```js
n("0 2 4").scale("C4:minor").superimpose(x => x.add(7)).sound("piano")
```

### Palindrome
```js
n("0 1 2 3 4").scale("C4:minor").palindrome().sound("piano")
```

### Off with rev
```js
sound("bd sd").off(1/8, rev)
```

### Echo with decay
```js
note("c3").sound("triangle").echo(4, 1/8, 0.7)
```

### Jux with filter
```js
s("hh*8").jux(x => x.lpf(1000))
```

### Layer multiple transforms
```js
n("0 2 4 6").scale("C4:minor").sound("piano")
  .layer(
    x => x.add(7),
    x => x.add(12)
  )
```

### Degrade
```js
s("hh*16").degradeBy(0.3)
```

### Sometimes with add
```js
n("0 1 2 3 4 5 6 7").scale("C4:major").sound("piano")
  .sometimes(x => x.add(12))
```

### Rarely with speed
```js
s("hh*8").rarely(x => x.speed(0.5))
```

### Struct
```js
note("c3 e3 g3").struct("x ~ x ~ x ~ ~ x")
```

### Mask
```js
n("0 1 2 3 4 5 6 7").scale("C4:major").sound("piano")
  .mask("<1 0 1 0>")
```

### Chunk with add
```js
n("0 1 2 3 4 5 6 7").scale("C4:major").sound("piano")
  .chunk(4, x => x.add(7))
```

## Continuous Modulation

### LFO on filter
```js
s("hh*16").lpf(sine.range(200, 4000).slow(4))
```

### Perlin noise on cutoff
```js
s("bd*4,hh*8").cutoff(perlin.range(500, 8000))
```

### Random pan
```js
s("hh*10").pan(brand)
```

### Sine wave modulation
```js
note("c3").sound("sawtooth").lpf(sine.range(200, 4000).slow(2))
```

### Triangle LFO on gain
```js
s("hh*16").gain(tri.range(0.2, 1).slow(2))
```

### Perlin on speed
```js
s("hh*8").speed(perlin.range(0.8, 1.2))
```

### Random cutoff
```js
s("bd*4").lpf(rand.range(200, 4000))
```

### Saw LFO on pan
```js
s("hh*8").pan(saw.range(0, 1).slow(2))
```

### Multi-parameter modulation
```js
note("c3").sound("sawtooth")
  .lpf(sine.range(200, 4000).slow(4))
  .pan(cosine.range(0, 1).slow(3))
  .gain(tri.range(0.3, 0.8).slow(2))
```

### Segment for continuous control
```js
s("supersaw").seg(16).lpf(sine.range(100, 5000).slow(2))
```

### Perlin on resonance
```js
note("c3").sound("sawtooth").lpf(1000).lpq(perlin.range(0, 20))
```

### Square wave modulation
```js
s("bd*4").gain(square.range(0.3, 1).slow(1))
```

## Synths

### Basic waveforms
```js
note("c3 e3 g3").sound("sine")
note("c3 e3 g3").sound("triangle")
note("c3 e3 g3").sound("sawtooth")
note("c3 e3 g3").sound("square")
```

### Noise
```js
sound("white").gain(0.2)
sound("pink").gain(0.2)
sound("brown").gain(0.2)
```

### FM synthesis
```js
note("c3 e3 g3").sound("sawtooth").fm(4).fmh("<1 2 3>")
```

### FM with envelope
```js
note("c3 e3 g3").fm(4).fmattack(0).fmdecay(.2).fmsustain(.5)
```

### FM harmonicity
```js
note("c3").fm(4).fmh("<1 1.5 2 3>").sound("sawtooth")
```

### Additive synthesis
```js
note("c3").sound("sawtooth").partials("1 0.5 0.25 0.125")
```

### Custom waveform
```js
note("c3").sound("user").partials("1 .5 .3 .2 .1")
```

### Vibrato
```js
note("c3").sound("sine").vib(4).vibmod(0.5)
```

### Vibrato with mini-notation
```js
note("c3").vib("<.5 1 2 4>:12")
```

### ADSR envelope
```js
note("c3 e3 g3").sound("sawtooth")
  .attack(0).decay(.1).sustain(.5).release(.2)
```

### ADSR shorthand
```js
note("c3 e3 g3").sound("sawtooth").adsr("0:.1:.5:.2")
```

### Filter envelope
```js
note("c3 e3 g3").sound("sawtooth").lpf(300)
  .lpa(.5).lpd(.3).lps(.2).lpr(.1).lpenv(4)
```

### Pitch envelope
```js
note("c").sound("sine")
  .penv(12).pdec(.5).pcurve(1)
```

### Pitch envelope down
```js
note("c3").sound("sine")
  .penv(-12).pdec(.3).pcurve(1).panchor(1)
```

### Wavetable
```js
note("c3").s("wt_square").loopBegin(0.1).loopEnd(0.5)
```

### ZZFX synth
```js
note("c2 eb2 f2 g2")
  .s("{z_sawtooth z_tan z_noise z_sine z_square}%4")
```

### SuperSaw
```js
note("c3").sound("supersaw").lpf(2000).gain(0.3)
```

### Synth with effects
```js
note("c3 e3 g3").sound("sawtooth")
  .lpf(1000).room(.5).delay(.3)
  .attack(0).decay(.1).sustain(.6).release(.3)
```

## Samples

### Load custom samples
```js
samples({ mydrum: 'path/to/file.wav' }, 'https://base-url/')
```

### GitHub shortcut
```js
samples('github:tidalcycles/dirt-samples')
```

### Drum machine banks
```js
s("bd sd,hh*8").bank("RolandTR909")
s("bd sd,hh*8").bank("RolandTR808")
s("bd sd,hh*8").bank("RolandTR707")
s("bd sd,hh*8").bank("RolandTR505")
```

### Sample selection
```js
sound("hh:0 hh:1 hh:2 hh:3")
```

### Granular with chop
```js
s("rhodes").chop(4).rev().loopAt(2)
```

### Slicing
```js
s("breaks165").slice(8, "0 1 2 3 4 5 6 7")
```

### Splice (with speed adjustment)
```js
s("breaks165").splice(8, "0 1 2 3 4 5 6 7")
```

### Loop
```js
s("casio").loop(1).loopBegin(0).loopEnd(.5)
```

### Loop at cycle length
```js
s("breaks165").loopAt(4)
```

### Scrub through sample
```js
s("rhodes").scrub(sine.range(0, 1).slow(4))
```

### Speed manipulation
```js
s("bd").speed("<1 2 0.5 -1>")
```

### Begin and end
```js
s("rhodes").begin(0.25).end(0.75)
```

### Cut group (hi-hat choke)
```js
s("[oh hh]*4").cut(1)
```

### Fit to cycle
```js
s("breaks165").fit()
```

### Striate
```js
s("breaks165").striate(8)
```

### Pitch-mapped samples
```js
samples({ 'moog': { 'g3': 'moog/G3.wav', 'g4': 'moog/G4.wav' } }, 'base-url')
note("g3 bb3 c4").s("moog").clip(1)
```

### Shabda (freesound)
```js
samples('shabda:bass:4,hihat:4,rimshot:2')
```

### Custom sample with envelope
```js
s("mydrum").attack(0.01).decay(0.1).sustain(0).release(0.1)
```

## MIDI Output

### Basic MIDI
```js
note("c a f e").midi('IAC Driver')
```

### MIDI with options
```js
note("c a f e").midi('IAC Driver', {
  midichannel: 1,
  velocity: 0.9
})
```

### MIDI channel selection
```js
note("c a f e").midi('IAC Driver').midichan(2)
```

### MIDI control change
```js
note("c a f e").midi('IAC Driver').ccn(74).ccv(0.5)
```

### MIDI program change
```js
note("c a f e").midi('IAC Driver').progNum(40)
```

### MIDI pitch bend
```js
note("c3").midi('IAC Driver').midibend(sine.range(-0.1, 0.1))
```

### MIDI with chords
```js
chord("<C^7 Dm7 G7>").voicing().midi('IAC Driver')
```

## Parallel Patterns with `$:`

```js
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
$: note("<c2 bb1 f2 eb2>").sound("gm_synth_bass_1").lpf(800)
$: n("0 2 4 <6 7>").scale("C4:minor").sound("piano")

// Mute with _$
_$: note("<c2 bb1>").sound("gm_synth_bass_1")
```

### Multi-layer beat
```js
$: sound("bd*4").bank("RolandTR909")
$: sound("[~ sd]*2").bank("RolandTR909")
$: sound("hh*8").bank("RolandTR909").gain("[.25 1]*4")
```

### Drum + bass + chords
```js
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
$: note("<c2 g2 bb1 f2>").sound("gm_synth_bass_1").lpf(600)
$: chord("<Cm7 Fm7 Bb7 Eb^7>").voicing().s("gm_electric_piano:1").room(.5)
```

### Ambient layers
```js
$: note("<c3 e3 g3>").sound("pad").slow(4).room(.8)
$: note("<c2 ~ ~ g2>").sound("bass").lpf(400)
$: sound("rim ~ ~ ~").room(.6).gain(.3)
```

## Full Compositions

### Coastline (by eddyflux)
```js
samples('github:eddyflux/crate')
setcps(.75)

stack(
  // Drums
  s("bd sd, hh*8").room(.3),
  // Chords
  chord("<Bbm9 Fm9>/4").dict('ireal')
    .voicing().s("gm_electric_piano:2").room(.5),
  // Bass
  n("0").set(chord("<Bbm9 Fm9>/4").dict('ireal'))
    .mode("root:g2").voicing().s("sawtooth").lpf(600),
  // Lead
  n("0 2 4 6").set(chord("<Bbm9 Fm9>/4").dict('ireal'))
    .scale("D5:minor").sound("sawtooth")
    .delay(.5).room(.5).gain(.4)
)
```

### Dub tune
```js
$: note("~ [< [d3,a3,f4]!2 [d3,bb3,g4]!2> ~])*2")
    .sound("gm_electric_guitar_muted").delay(.5)
$: sound("bd rim").bank("RolandTR707").delay(.5)
$: n("<4 [3@3 4] [<2 0> ~@16] ~>")
    .scale("D4:minor").sound("gm_accordion:2").room(2).gain(.4)
$: n("[0 [~ 0] 4 [3 2] [0 ~] [0 ~] <0 2> ~]/2")
    .scale("D2:minor").sound("sawtooth,triangle").lpf(800)
```

### Getting started demo
```js
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

### Minimal techno
```js
setcpm(125/4)

$: sound("bd*4").bank("RolandTR909")
$: sound("hh*16").gain("[.15 1]*8").bank("RolandTR909")
$: sound("~ ~ ~ cp").bank("RolandTR909").room(.4)
$: note("<c2 ~ eb2 ~ f2 ~ g2 ~>").sound("sawtooth")
  .lpf(sine.range(200, 2000).slow(8))
```

### Ambient soundscape
```js
setcpm(60/4)

$: note("<[c4,e4,g4] [a3,c4,e4] [f3,a3,c4] [g3,b3,d4]>/4")
  .sound("gm_pad_new_age").room(1).size(8).gain(.3)
$: n("0 ~ 2 ~ 4 ~ ~ ~").scale("C3:minor")
  .sound("gm_synth_bass_1").lpf(400).gain(.3)
$: sound("rim ~ ~ ~ ~ ~ ~ ~").room(.8).size(5).gain(.15)
```

### Acid bass
```js
setcpm(130/4)

$: note("<c2 eb2 f2 g2 bb2 c3>").sound("sawtooth")
  .lpf(sine.range(200, 4000).slow(2))
  .lpq(15).distort(1.5).gain(.5)
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
```

### Jazz trio
```js
setcpm(100/4)

$: chord("<Dm7 G7 C^7 A7>").voicing()
  .s("gm_electric_piano:1").room(.5).gain(.35)
$: n("0 - 1 - 2 - 1 -").set(chord("<Dm7 G7 C^7 A7>"))
  .mode("root:c2").voicing().s("gm_acoustic_bass").clip(.8)
$: sound("bd ~ sd ~, hh*4").bank("RhythmAce").gain(.3).room(.3)
```

### Reggae
```js
setcpm(75/4)

$: note("<[c4,e4,g4] ~ [bb3,d4,f4] ~>")
  .sound("gm_electric_guitar_muted").jux(rev)
  .delay(.5).room(.4)
$: sound("~ ~ sd ~, hh ~ hh ~").bank("RolandTR707")
$: note("<c2 ~ bb1 ~>").sound("gm_synth_bass_1").lpf(500)
```

## Visualization

### Waveform scope
```js
note("c3 e3 g3").sound("sawtooth")._scope()
```

### Pitch wheel
```js
n("0 2 4 6 4 2 0").scale("C4:minor").sound("piano")._pitchwheel()
```

### Piano roll (punchcard)
```js
n("0 2 4 6 4 2").scale("C4:minor").sound("piano").punchcard()
```

### Scope on all layers
```js
$: sound("bd*4, hh*8")._scope()
$: note("<c2 g2>").sound("bass").lpf(600)._scope()
$: chord("<Cm7 Fm7>").voicing().s("piano")._scope()
```

## Workflow Patterns

### Debug with log
```js
n("0 2 4 6").scale("C4:minor").sound("piano").log()
```

### Set tempo
```js
setcpm(120/4)  // 120 BPM in 4/4
setcps(0.5)    // 0.5 cycles per second (default)
```

### Arrange sections
```js
arrange(
  [4, sound("bd*4, hh*8")],
  [4, sound("bd*4, hh*8, [~ sd]*2")],
  [2, sound("bd*2, hh*4")],
  [2, silence]
)
```

### Polymeter
```js
polymeter(
  note("c3 e3 g3"),
  note("c2 g2")
).sound("piano")
```

### Swing
```js
s("hh*8").swing(4)
```

### Choose randomly
```js
n(irand(8)).scale("C4:minor").sound("piano")
```

### Random melody
```js
n("0 | 2 | 4 | 6 | 7").scale("C4:minor").sound("piano")
```
