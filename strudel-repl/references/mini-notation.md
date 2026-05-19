# Strudel Mini-Notation Complete Reference

Mini-notation is a custom language for writing rhythmic patterns compactly. It originates from TidalCycles.

## String Formats

- `"pattern"` — single-line mini-notation
- `` `pattern` `` — multi-line mini-notation (backticks)
- `'string'` — regular string, NOT parsed as mini-notation

## Sequences

Items separated by spaces play one after another within a cycle:

```js
note("c e g b")  // 4 notes, each 0.5s at default tempo
```

Adding more notes makes each shorter — everything is squished into 1 cycle.

## Sample Selection (`:n`)

```js
sound("hh:0 hh:1 hh:2 hh:3")
```

Omitting number is same as `:0`.

## Rests (`~` or `-`)

```js
sound("bd ~ sd ~")
sound("bd - sd -")
```

Both `~` and `-` mean silence.

## Alternation (`<>`)

One element per cycle, cycling through them:

```js
sound("<bd sd hh>")  // bd on cycle 1, sd on cycle 2, hh on cycle 3
```

Equivalent to `[bd sd hh]/3`. Adding/removing elements doesn't change tempo.

With multiplication for notes per cycle:
```js
note("<e5 b4 d5 c5 a4 c5>*8")  // 8 notes per cycle
```

## Sub-sequences (`[]`)

Nest patterns to create subdivisions:

```js
sound("bd [hh hh] sd [hh bd]")
```

Content inside `[]` is squished to the time of one outer event. Unlimited nesting depth:

```js
sound("bd [metal [jazz [sd cp]]]")
```

## Multiplication (`*`)

Speed up:

```js
sound("hh*8")           // 8 hihats per cycle
sound("[bd sd]*2")      // bd sd bd sd per cycle
sound("bd hh*2 rim hh*3") // individual element speed
```

Decimal values work: `sound("hh*2.75")`

## Division (`/`)

Slow down (requires brackets):

```js
note("[c e g b]/2")  // spread over 2 cycles
```

## Elongation (`@`)

Specify relative duration weight:

```js
note("c@3 e")  // c is 3x longer than e (c = 0.75 cycles, e = 0.25)
```

Default weight is 1. Multiple `@` symbols: `c @ @` = `c@3`

## Replication (`!`)

Repeat without speeding up:

```js
note("c!3 e")  // c c c e, each same duration
```

Compare: `c!3` = `c c c` (3 events, same total time as 1), `c*3` = `c c c` (3x faster)

## Parallel / Polyphony (`,`)

Play simultaneously:

```js
note("g3,b3,e4")           // chord
note("[g3,b3,e4]")         // same chord
sound("bd*4, hh*8")        // two parallel patterns
sound("hh hh hh, bd [bd,casio]")  // commas inside sub-sequences
```

Multi-line with backticks:
```js
sound(`bd*2, - cp,
- - - oh, hh*4,
[- casio]*2`)
```

## Random Removal (`?`)

50% chance of removal:

```js
note("[g3,b3,e4]*8?")       // 50% removal
note("[g3,b3,e4]*8?0.1")    // 10% removal
```

## Random Choice (`|`)

One chosen randomly per cycle:

```js
note("[g3,b3,e4] | [a3,c3,e4] | [b3,d3,f#4]")
```

## Euclidean Rhythms (`(beats, segments, offset)`)

Distribute beats evenly across segments:

```js
sound("bd(3,8)")       // 3 beats over 8 segments (Pop Clave)
sound("bd(3,8,0)")     // with offset
sound("bd(5,8)")       // 5 beats over 8 segments
sound("bd(3,8,3), hh cp")  // with offset, hear the shift
```

Parameters:
- `beats`: number of onsets
- `segments`: total steps
- `offset` (optional): starting position

## Foot/Period Notation (`.`)

Divides equal parts of a pattern (alternative to `[]`):

```js
sound("bd.sd.hh.sd")  // same as sound("bd sd hh sd") but with foot marking
```

## Polymeter (`{}`)

Historical syntax for polyrhythmic patterns:

```js
// {a b c, x y} is same as polymeter
note("{c eb g, c2 g2}")
// {a b c}%4 = <a b c>*4
```

## Complete Symbol Cheat Sheet

| Symbol | Meaning |
|--------|---------|
| `'` | marks start/end of strings (different from `"`) |
| `"` | marks start/end of single line patterns |
| `` ` `` | marks start/end of multi-line patterns |
| `[]` | sub-sequence; each item has same length |
| `<>` | alternates between items each cycle |
| `{}` | polymetric patterns |
| `@3` | elongates by factor 3 |
| `@` | elongates once (multiple `@` compound) |
| `_` | elongates once; also used before `$:` to mute |
| `.` | divides equal parts (foot) |
| `-` | silence |
| `~` | silence |
| `x` | not silence (for `struct`) |
| `b` | flat (decrease semitone) |
| `#` | sharp (increase semitone) |
| `*3` | play 3x speed (`fast(3)`) |
| `!3` | replicate 3 times |
| `/2` | play at half speed (`slow(2)`) |
| `?` | play sometimes (50% chance) |
| `?0.3` | play with 30% removal chance |
| `\|` | choose randomly per cycle |
| `,` | play all items at same time (`stack()`) |
| `:` | separates parameters (sample index, etc) |
| `$:` | start of line: defines stack member |
| `_$` | before stack name: mute (`hush()`) |
