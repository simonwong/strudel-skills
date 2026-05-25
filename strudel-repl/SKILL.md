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
| `"?0.3"` | Random removal (30%) | `sound("hh?0.3")` |
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
setBpm(120)      // 120 BPM directly (auto-adjusts for cycle length)
```

BPM formula: `setcpm(bpm / beatsPerCycle)` — or use `setBpm(bpm)` to skip the math.

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

### 日常帮助（调试、解释语法、快速 pattern）

1. **Understand intent** — Are they building a beat, writing a melody, exploring sounds, or learning syntax?
2. **Start simple** — Begin with a basic pattern and iterate. Don't write 20 lines of code upfront.
3. **Explain the why** — Strudel has non-obvious behaviors (e.g., adding notes speeds them up). Explain tradeoffs.
4. **Use mini-notation first** — `sound("bd*4, [~ sd]*2, hh*8")` is more idiomatic than `stack(s("bd").struct("x*4"), ...)`. Reserve JS functions for when mini-notation can't express the idea.
5. **Use `n().scale()` for melodies** — `n("0 2 4").scale("C:major")` is more flexible than `note("c3 e3 g3")` because transposing only requires changing one parameter.
6. **Only read relevant reference files** — Don't load all references. Pick the one file that matches the user's question (e.g., drums → `references/examples/drums.md`).
7. **Suggest `.log()` for debugging** — `.log()` shows event timing and parameter values.

### 完整创作（作曲、编曲、模仿、复刻）

当用户要求**创作、编曲、模仿、复刻某首歌**时，不要直接输出最终代码。遵循以下五步流程：

#### Step 1 — 理解需求

- 明确模式：**原创** / **模仿**（取其神韵） / **复刻**（还原原曲）
- 明确风格、情绪、参考歌曲、乐器偏好
- 如果有参考歌曲，进入 Step 2；否则跳到 Step 3

#### Step 2 — 研究参考歌曲

用 WebSearch 搜索歌曲的音乐特征。根据模式不同，研究深度不同：

**模仿（取其神韵）** — 搜索风格参数即可：

| 维度 | 说明 | 对应 Strudel 参数 |
|------|------|-------------------|
| 调性 Key | 大调/小调/调式 | `scale("Root:Type")` |
| 速度 BPM | 每分钟拍数 | `setcpm(bpm/4)` 或 `setBpm()` |
| 和弦进行 | 主歌/副歌的和弦走向 | `chord("<...>")` |
| 节奏型 | 鼓 pattern 特征 | `sound("bd sd hh...")` |
| 标志性音色 | 主奏乐器、特色音效 | `.sound()`, `.bank()` |
| 结构 | 前奏→主歌→副歌→桥段 | `arrange()` 或分层设计 |
| 情绪关键词 | 悲伤、温暖、暗黑等 | 影响混响、滤波、音色选择 |

将研究结果整理为"创作参数表"，展示给用户确认后再进入编曲。

**复刻（还原原曲）** — 需要更精确的音乐信息：

| 维度 | 说明 | 搜索方式 |
|------|------|----------|
| 精确和弦谱 | 具体的和弦标记（如 C#m7 - A - E - B） | 搜索"`歌名` chords"或"`歌名` 和弦" |
| 旋律音符 | 主旋律的具体音高和节奏 | 搜索"`歌名` melody notes"或"`歌名` sheet music" |
| 鼓 pattern | 每个乐器的精确节奏型 | 搜索"`歌名` drum pattern"或"`歌名` drum transcription" |
| 各层音色 | 每个乐器轨的具体音色 | 搜索"`歌名` instrumentation" |
| 段落编排 | 每个段落有哪些乐器进出 | 搜索"`歌名` arrangement" |
| 特殊技巧 | 滑音、泛音、效果器等 | 搜索"`歌名` guitar tab"`歌名` synth patch" |

复刻模式下，将研究结果逐层列出（旋律层、和弦层、贝斯层、鼓层、效果层），与用户确认每个层的准确性后再编曲。

#### Step 3 — 编曲

- 从简单骨架开始（1-2 层），逐步叠加
- 每加一层，检查是否符合 SKILL.md 的最佳实践（`n().scale()` > `note()`，mini-notation > JS 函数等）
- 复刻模式下，优先使用 `note()` 直接指定音高（精确还原），而非 `n().scale()`（灵活但不精确）

#### Step 4 — 自我 Review

输出代码前，对照 Common Pitfalls 逐项检查：

- `struct` 用法是否正确（二进制 `x`/`~`，而非数字索引）
- `n().scale()` vs `note()` 是否选对（模仿用 `n().scale()`，复刻用 `note()`）
- `setcpm()` / `setBpm()` 是否匹配目标 BPM
- 各层 `gain` 是否平衡（避免某层盖过其他层）
- Pad/弦乐类音色是否设了 `sustain`
- 复刻模式额外检查：和弦是否与原曲一致、旋律音高是否准确、段落结构是否匹配

如发现问题，修正后再输出。不需要设定固定的迭代次数——发现多少问题就修多少次，直到没有明显问题。

#### Step 5 — 输出 + 迭代提示

- 输出完整代码
- 主动询问用户是否需要调整，例如："需要我调整某个层的参数、增加/删除某个层、或者换一种风格方向吗？"

## Common Pitfalls

- `note("c e g")` without `.sound()` uses default triangle wave — always set a sound
- Adding more notes in a sequence speeds it up (they're squished into 1 cycle) — use `<>` or `/n` to prevent this
- `n` vs `note`: `n` indexes into scales/samples, `note` names specific pitches. For melodies, prefer `n("0 2 4").scale("C:major")` over `note("c3 e3 g3")` — it's more flexible and idiomatic
- Effects are single-use per event — duplicates override, not stack
- Parameters are sampled at note onset only — use `.seg(n)` for continuous modulation
- `setcpm(120)` is NOT 120 BPM — it's 120 cycles/min. For 120 BPM in 4/4: `setcpm(120/4)` or `setBpm(120)`
- `$:` layers are independent cycles — they sync automatically. Don't use `stack()` to "fix" `$:` timing (it's not a bug)
- `struct` 的参数是**二进制节奏模式**（`x`/`~`），不是音符索引。`struct("[~ 0] [1 ~]")` 中的 `0 1` 会被当作音符索引从 voicing 中选音，而非节奏门控。要控制节奏用 `struct("[~ x] [x ~]")`，要选音用 `n("0 1 2 3").set(chord("...")).voicing()`
- 弦乐/Pad 类音色注意 `sustain` 设置——只有 `attack` + `release` 会让音符很短，需加 `.sustain(0.5-1.0)` 延长

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
