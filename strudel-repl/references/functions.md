# Strudel Functions Complete Reference

## Pattern Creation (Factories)

### `cat` (synonyms: `slowcat`)
Concatenates items, each taking one cycle.
```js
cat("e5", "b4", ["d5", "c5"]).note()  // "<e5 b4 [d5 c5]>"
```

### `seq` (synonyms: `fastcat`)
Like `cat` but items crammed into one cycle.
```js
seq("e5", "b4", ["d5", "c5"]).note()  // "e5 b4 [d5 c5]"
```

### `stack` (synonyms: `polyrhythm`, `pr`)
Play items simultaneously.
```js
stack("g3", "b3", ["e4", "d4"]).note()  // "g3,b3,[e4 d4]"
```

### `stepcat` (synonyms: `timeCat`, `timecat`)
Concatenate proportional to step counts.
```js
stepcat([3,"e3"],[1, "g3"]).note()  // "e3@3 g3"
```

### `arrange`
Arrange patterns across cycles: `[cycles, pattern]` pairs.
```js
arrange([4, "<c a f e>(3,8)"], [2, "<g a>(5,8)"]).note()
```

### `polymeter` (synonyms: `pm`)
Align steps creating polymeters (lowest common multiple).
```js
polymeter("c eb g", "c2 g2").note()  // "{c eb g, c2 g2}"
```

### `silence`
Empty pattern. Equivalent to `"~"`.

### `run`
Numbers 0 to n-1.
```js
n(run(4)).scale("C4:pentatonic")  // "0 1 2 3"
```

### `binary` / `binaryN`
Create binary pattern from number.
```js
"hh".s().struct(binary(5))  // "1 0 1"
"hh".s().struct(binaryN(55532, 16))  // 16-bit pattern
```

---

## Time Modifiers

### `slow(n)` (synonyms: `sparsity`)
Slow down by factor. Equivalent to `/` in mini-notation.

### `fast(n)` (synonyms: `density`)
Speed up by factor. Equivalent to `*` in mini-notation.

### `early(n)` / `late(n)`
Nudge pattern earlier/later by cycles.

### `clip(n)` (synonyms: `legato`)
Multiply event duration; cut samples exceeding it.

### `euclid(pulses, steps)`
Euclidean rhythm.
```js
note("c3").euclid(3,8)  // Cuban tresillo
```

### `euclidRot(pulses, steps, rotation)`
Euclidean rhythm with rotation offset.
```js
note("c3").euclidRot(3,16,14)  // Samba necklace
```

### `euclidLegato(pulses, steps)`
Euclidean with legato (no gaps between pulses).

### `rev`
Reverse all cycles.

### `palindrome`
Alternate forward/backward each cycle.

### `iter(n)` / `iterBack(n)`
Rotate through subdivisions each cycle.

### `ply(n)`
Repeat each event n times within its time span.

### `segment(n)` (synonyms: `seg`)
Sample pattern at n events per cycle. Essential for continuous modulation:
```js
s("supersaw").seg(16).lpf(sine.range(100, 5000).slow(2))
```

### `compress(start, end)`
Compress cycle into given timespan.

### `zoom(start, end)`
Play portion of pattern.

### `linger(fraction)`
Select fraction and repeat to fill cycle.

### `fastGap(n)` (synonyms: `fastgap`)
Speed up but leave gaps instead of repeating.

### `inside(n, fn)` / `outside(n, fn)`
Apply operation inside/outside n cycles.

### `cpm(n)`
Play at given cycles per minute.

### `ribbon(offset, cycles)` (synonyms: `rib`)
Loop a portion of the pattern.

### `swing(subdivision)` / `swingBy(amount, subdivision)`
Add swing feel.
```js
s("hh*8").swing(4)  // shuffle
```

---

## Control Parameters

### Core Parameters
- `sound` / `s` — sound source name
- `note` — pitch by name (`c3`) or MIDI number (`48`)
- `n` — index (scale degree, sample number)
- `freq` — frequency in Hz

### Operators

#### `add(n)` / `sub(n)`
Add/subtract from pitch (works with notes and numbers).

#### `mul(n)` / `div(n)`
Multiply/divide values.

#### `round` / `floor` / `ceil`
Round numerical patterns.

#### `range(lo, hi)` / `rangex(lo, hi)` / `range2(lo, hi)`
Remap 0..1 (or -1..1 for range2) to given range. `rangex` uses exponential curve.

#### `ratio("1, 5:4, 3:2")`
Ratio notation for frequency ratios.

#### `as("param:param")`
Batch set properties: `"c:.5 a:1".as("note:clip")`

---

## Signals (Continuous Patterns)

| Signal | Range | Type |
|--------|-------|------|
| `sine` | 0-1 | Sine wave |
| `cosine` | 0-1 | Cosine wave |
| `saw` | 0-1 | Sawtooth wave |
| `tri` | 0-1 | Triangle wave |
| `square` | 0-1 | Square wave |
| `rand` | 0-1 | Random float |
| `perlin` | 0-1 | Perlin noise |
| `irand(n)` | 0 to n-1 | Random integer |
| `brand` | 0 or 1 | Binary random |
| `brandBy(p)` | 0 or 1 | Binary with probability |
| `mouseX` / `mouseY` | 0-1 | Mouse position |

Bipolar variants (-1 to 1): `sine2`, `cosine2`, `saw2`, `tri2`, `square2`, `rand2`

Common companion methods: `.range()`, `.segment()`, `.slow()`

---

## Random Modifiers

### `choose(xs...)` / `wchoose([val, weight]...)`
Random selection from list.

### `chooseCycles` (synonyms: `randcat`) / `wchooseCycles` (synonyms: `wrandcat`)
One random choice per cycle. Mini-notation: `"a | b | c"`.

### `degradeBy(amount)` / `degrade`
Random removal. `degrade` = `degradeBy(0.5)`. Mini-notation: `"x?"` / `"x?0.3"`.

### `undegradeBy(amount)` / `undegrade`
Inverse of degrade — keeps what degrade removes.

### `sometimesBy(prob, fn)` / `sometimes(fn)`
Apply function with given (or 50%) probability.

### Shorthand probabilities
`never` (0), `almostNever` (0.1), `rarely` (0.25), `sometimes` (0.5), `often` (0.75), `almostAlways` (0.9), `always` (1)

### `someCyclesBy(prob, fn)` / `someCycles(fn)`
Apply per-cycle with given (or 50%) probability.

---

## Conditional Modifiers

### `firstOf(n, fn)` / `lastOf(n, fn)`
Apply function every n cycles (starting from first/last).

### `when(binaryPattern, fn)`
Apply function when pattern is true.

### `chunk(n, fn)` / `chunkBack(n, fn)` / `fastChunk(n, fn)`
Divide into n parts, apply fn to each part in turn.

### `arp(indices)` / `arpWith(fn)`
Select indices from stacked notes.

### `struct(binaryPattern)`
Apply rhythm structure. Use `x` for hit, `~` for silence.

### `mask(binaryPattern)`
Mute where mask is 0 or `~`.

### `reset(pattern)` / `restart(pattern)`
Reset/restart pattern on trigger.

### `hush`
Silence a pattern.

### `invert` (synonyms: `inv`)
Swap 1s and 0s in binary pattern.

### `pick(pattern, lookup)` / `pickmod` / `pickF` / `pickRestart` / `pickReset`
Select from list by index or name. `pick` preserves structure; `inhabit` compresses to fit.

### `squeeze(pattern, list)`
Pick and compress to match selecting event duration.

---

## Accumulation Modifiers

### `superimpose(fn...)`
Overlay transformed copy on original.

### `layer(fn...)`
Replace with transformed versions (original not kept).

### `off(time, fn)`
Overlay with time delay.
```js
"c3 eb3 g3".off(1/8, x=>x.add(7)).note()
```

### `echo(times, time, feedback)`
Repeated echoes with decreasing velocity.

### `echoWith(times, time, fn)`
Echoes with custom function per iteration.

---

## Tonal Functions

### `scale(name)`
Transform numbers to scale degrees. Format: `"Root:Type"` e.g. `"C:major"`, `"A2:minor:pentatonic"`.

Negative values wrap backwards. Sharps/flats can produce out-of-scale notes.

### `transpose(semitones)`
Transpose by semitones. Supports scientific notation.

### `scaleTranspose(steps)`
Transpose within the current scale.

### `chord(symbol)` + `voicing()`
Automated chord voicing with smooth voice leading.
```js
chord("<Am C F G>").voicing()
```

Control params: `chord`, `dict`, `anchor`, `mode` (below/above/duck/root), `offset`, `n`.

### `rootNotes(octave)`
Extract root notes from chord symbols.

### `addVoicings(name, dictionary)`
Register custom voicing dictionary.

Default chord symbols: `2 5 6 7 9 11 13 69 add9 o h sus ^ - ^7 -7 7sus h7 o7 ^9 ^13` and many more.

---

## Stepwise Functions (Experimental)

Work with steps instead of cycles.

### `pace(n)` — fit n steps per cycle
### `stepcat` — concatenate proportional to steps
### `stepalt` — alternate with list elements
### `expand(n)` / `contract(n)` — modify step size
### `extend(n)` — increase density + step count
### `take(n)` / `drop(n)` — take/drop steps
### `shrink(n)` / `grow(n)` — progressively shrink/grow
### `tour(...)` / `zip(...)` — insert/zip patterns
