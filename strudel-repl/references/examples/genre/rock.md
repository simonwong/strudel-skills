# 摇滚 / Rock

> 从 Chuck Berry 的原始能量到 Post-Rock 的壮丽声墙，摇滚的核心是「力量与态度」。
> 失真吉他、驱动鼓点、简单有力的和声进行。

## 风格特征 / Style Characteristics

- **节奏 / Rhythm**: 100-180 BPM，强力四拍，强调反拍
- **和声 / Harmony**: 大调/小调三和弦，强力和弦（五度），偶尔七和弦
- **音色 / Timbre**: 过载/失真吉他、有力的鼓组、贝斯驱动
- **律动 / Feel**: 直接、有力、能量感强

---

## 基础模式 / Basic Patterns

### 强力和弦 / Power Chords

```js
// 经典摇滚强力和弦 — 只用根音和五度
setcpm(120/4)

$: note("<c3 g3 c3 g3>")
  .sound("gm_overdrive_guitar")
  .struct("x x x x")
  .gain(0.35)
  .distort(0.4)
  .lpf(3000)
```

### 驱动鼓点 / Driving Drums

```js
// 摇滚基础鼓点 — 底鼓 + 军鼓 + 开帽
$: sound("bd ~ sn ~ bd ~ sn ~")
  .bank("RolandTR909")
  .gain("0.4 0 0.35 0 0.4 0 0.35 0")

$: sound("~ oh ~ oh")
  .bank("RolandTR909")
  .gain(0.12)
```

---

## 进阶示例 / Advanced Examples

### 经典摇滚 / Classic Rock

```js
// 经典摇滚 — 吉他 riff + 强力鼓点
setcpm(110/4)

// 吉他 riff — 五度进行
$: note("<c3 ~ g3 ~ bb2 ~ f3 ~>")
  .sound("gm_overdrive_guitar")
  .struct("x ~ x ~ x ~ x ~")
  .gain(0.3)
  .distort(0.35)
  .lpf(2500)
  .room(0.2).size(1.5)

// 鼓 — 经典摇滚节奏
$: stack(
    sound("bd ~ sn ~ bd ~ sn ~").gain(0.4),
    sound("~ hh ~ hh ~ hh ~ hh").gain(0.08).lpf(8000),
    sound("~ ~ ~ ~ ~ ~ oh ~").gain(0.1)
  ).bank("RolandTR909")

// 贝斯 — 根音驱动
$: note("<c2 ~ g2 ~ bb1 ~ f2 ~>")
  .sound("gm_synth_bass_1")
  .gain(0.45)
  .lpf(600)
  .clip(0.7)
```

### 朋克 / Punk

```js
// 朋克 — 快速、简单、原始能量
setcpm(180/4)

// 朋克和弦 — 快速强力和弦
$: note("<c3 c3 c3 c3>")
  .sound("gm_distortion_guitar")
  .struct("x x x x")
  .gain(0.35)
  .distort(0.6)
  .lpf(2000)
  .room(0.1).size(1)

// 鼓 — 快速四拍
$: stack(
    sound("bd bd bd bd").gain(0.45),
    sound("sn sn sn sn").gain(0.35),
    sound("hh hh hh hh").gain(0.08).lpf(9000)
  ).bank("RolandTR909")
   .speed(perlin.range(0.98, 1.02))

// 贝斯 — 快速八分音符
$: note("<c2 c2 c2 c2>")
  .sound("gm_synth_bass_1")
  .struct("x x x x")
  .gain(0.45)
  .lpf(500)
  .clip(0.5)
```

### 硬摇滚 / Hard Rock

```js
// 硬摇滚 — 更重的失真，更复杂的节奏
setcpm(105/4)

// 吉他 — 重度失真 riffs
$: note("<a2 ~ c3 ~ d3 ~ e3 ~>")
  .sound("gm_distortion_guitar")
  .struct("x ~ x ~ x ~ x ~")
  .gain(0.3)
  .distort(0.5)
  .lpf(2200)
  .room(0.15).size(1.5)

// 鼓 — 更重的底鼓
$: stack(
    sound("bd ~ ~ bd ~ ~ bd ~").gain(0.5),
    sound("~ ~ sn ~ ~ ~ sn ~").gain(0.35),
    sound("hh ~ hh ~ hh ~ hh ~").gain(0.06).lpf(7000)
  ).bank("RolandTR909")

// 贝斯 — 跟随吉他 riff
$: note("<a1 ~ c2 ~ d2 ~ e2 ~>")
  .sound("gm_synth_bass_1")
  .gain(0.45)
  .lpf(500)
  .distort(0.2)
  .clip(0.8)
```

### Post-Rock / 后摇

```js
// Post-Rock — 壮丽声墙，渐进式构建
setcpm(90/4)

// 吉他 — 清音 arpeggio，逐渐失真
$: note("<a3 e4 c4 b3>")
  .sound("gm_overdrive_guitar")
  .struct("x ~ x ~ x ~ x ~")
  .gain(sine.range(0.15, 0.35).slow(16))
  .distort(sine.range(0.1, 0.4).slow(16))
  .lpf(sine.range(1500, 4000).slow(16))
  .room(0.7).size(4)
  .delay(0.3).delaytime(1/4).delayfeedback(0.5)

// 鼓 — 从轻柔到有力
$: stack(
    sound("bd ~ ~ ~ ~ ~ ~ ~").gain(sine.range(0.2, 0.4).slow(16)),
    sound("~ ~ ~ ~ sn ~ ~ ~").gain(sine.range(0.15, 0.3).slow(16)),
    sound("~ hh ~ hh ~ hh ~ hh").gain(0.05)
  ).bank("RolandTR909")
   .room(0.4).size(3)

// 贝斯 — 长音铺底
$: note("<a1 ~ ~ ~ ~ ~ ~ ~>")
  .sound("gm_synth_bass_1")
  .gain(0.35)
  .lpf(400)
  .room(0.5).size(3)
  .clip(3)
```

### 独立摇滚 / Indie

```js
// Indie — 清音吉他 arpeggios，温暖质感
setcpm(115/4)

// 吉他 — 清音 arpeggios
$: chord("<Am F C G>")
  .voicing()
  .sound("gm_acoustic_guitar")
  .struct("x ~ x ~ x ~ x ~")
  .gain(0.3)
  .room(0.3).size(2)
  .lpf(3500)

// 吉他点缀 — 高音旋律
$: n("9 ~ 7 ~ 5 ~ 4 ~")
  .scale("A4:minor")
  .sound("gm_acoustic_guitar")
  .gain(0.15)
  .room(0.4).size(2.5)
  .delay(0.15).delaytime(1/4).delayfeedback(0.3)

// 鼓 — 轻柔但有力
$: stack(
    sound("bd ~ ~ bd ~ ~ ~ ~").gain(0.35),
    sound("~ ~ sn ~ ~ ~ sn ~").gain(0.2),
    sound("~ sh ~ sh ~ sh ~ sh").gain(0.06)
  ).bank("RolandTR909")
   .room(0.2).size(1.5)

// 贝斯 — 简单根音
$: note("<a1 ~ f1 ~ c2 ~ g1 ~>")
  .sound("gm_acoustic_bass")
  .gain(0.4)
  .lpf(700)
  .room(0.2).size(1.5)
```

---

## 完整编曲 / Full Composition — 摇滚能量

```js
// Rock Energy — 摇滚能量
// 从清音 intro 到失真高潮的渐进式编曲
setcpm(120/4)

stack(
  // 吉他 — 强力和弦 riff
  note("<c3 ~ g3 ~ bb2 ~ f3 ~>")
    .sound("gm_overdrive_guitar")
    .struct("x ~ x ~ x ~ x ~")
    .gain(0.3)
    .distort(0.4)
    .lpf(2500)
    .room(0.2).size(1.5),

  // 吉他2 — 高音点缀
  n("7 ~ 5 ~ 3 ~ 0 ~")
    .scale("C4:minor")
    .sound("gm_overdrive_guitar")
    .gain(0.1)
    .distort(0.3)
    .lpf(3000)
    .delay(0.15).delaytime(1/4).delayfeedback(0.3)
    .room(0.4).size(2.5),

  // 鼓 — 经典摇滚节奏
  stack(
    sound("bd ~ sn ~ bd ~ sn ~").gain(0.4),
    sound("~ hh ~ hh ~ hh ~ hh").gain(0.07).lpf(8000),
    sound("~ ~ ~ ~ ~ ~ oh ~").gain(0.1)
  ).bank("RolandTR909"),

  // 贝斯 — 根音驱动
  note("<c2 ~ g2 ~ bb1 ~ f2 ~>")
    .sound("gm_synth_bass_1")
    .gain(0.45)
    .lpf(600)
    .clip(0.7),

  // 合成器 pad — 氛围层（可选）
  chord("<Cm Fm>")
    .voicing()
    .sound("sawtooth")
    .gain(0.04)
    .lpf(1200)
    .room(0.7).size(4)
    .attack(0.5).release(1)
)
```

---

## 技巧提示 / Tips

- **distort()**: `.distort(0.3-0.6)` 是摇滚吉他的灵魂，值越高越重
- **强力和弦**: 只用根音和五度，`note("<c3 g3>")` 制造厚重感
- **鼓机音色**: `.bank("RolandTR909")` 是摇滚的标准鼓机
- **节奏强调**: 摇滚强调反拍，在 `struct()` 中用 `~` 留出空间
- **渐进式构建**: Post-Rock 用 `sine.range().slow()` 逐渐增加能量
- **清音 vs 失真**: 同一 riff 可以通过调整 `distort()` 从清音到失真
- **房间感**: 摇滚混响要适度 `room(0.1-0.3)`，保持力量感
- **贝斯跟随**: 贝斯通常跟随吉他 riff 的根音
