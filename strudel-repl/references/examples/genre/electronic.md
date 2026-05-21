# 电子 / Electronic

> 从底特律 Techno 的冰冷机械感到 Ambient 的无限空间，电子音乐的核心是「音色设计」。
> 用合成器波形、滤波器扫描、侧链压缩构建声音景观。

## 风格特征 / Style Characteristics

- **节奏 / Rhythm**: 120-180 BPM（Techno/House），160-180 BPM（DnB），多变（Ambient）
- **和声 / Harmony**: 简单和弦或无调性，强调音色变化
- **音色 / Timbre**: 合成器锯齿波/方波、TR-909/808 鼓机、采样处理
- **律动 / Feel**: 机械精确或有机流动，取决于子风格

---

## 基础模式 / Basic Patterns

### 四四拍底鼓 / Four-on-the-Floor

```js
// House/Techno 基础底鼓
setcpm(128/4)

$: sound("bd bd bd bd")
  .bank("RolandTR909")
  .gain(0.5)
```

### 酸性贝斯 / Acid Bassline

```js
// 经典 303 酸性贝斯线条
$: note("<c2 c3 eb2 c2 f2 g2 bb2 c3>")
  .sound("sawtooth")
  .lpf(sine.range(200, 2000).slow(4))
  .lpq(8)
  .gain(0.4)
  .distort(0.3)
```

---

## 进阶示例 / Advanced Examples

### Minimal Techno / 极简Techno

```js
// 极简 Techno — 循环、渐变、催眠
setcpm(128/4)

$: sound("bd ~ ~ ~ bd ~ ~ ~")
  .bank("RolandTR909")
  .gain(0.5)
  .lpf(100)

$: sound("~ ~ ~ ~ ~ ~ ~ oh")
  .bank("RolandTR909")
  .gain(0.15)
  .room(0.3).size(2)

$: note("c2 ~ ~ c2 ~ ~ c2 ~")
  .sound("sawtooth")
  .lpf(sine.range(300, 1500).slow(8))
  .lpq(6)
  .gain(0.3)
  .distort(0.2)

// 滤波器扫描 — 催眠的核心
$: note("c3")
  .sound("square")
  .lpf(sine.range(200, 4000).slow(16))
  .lpq(4)
  .gain(0.08)
  .delay(0.3).delaytime(1/8).delayfeedback(0.4)
```

### Dub / 回响音乐

```js
// Dub — 重混响、回声、空间感
setcpm(136/4)

$: sound("bd ~ ~ ~ ~ ~ bd ~")
  .bank("RolandTR909")
  .gain(0.4)
  .room(0.5).size(3)

$: sound("~ sn ~ ~ ~ ~ ~ ~")
  .bank("RolandTR909")
  .gain(0.25)
  .delay(0.6).delaytime(3/8).delayfeedback(0.6)
  .room(0.7).size(4)

$: note("<c2 ~ bb1 ~ f2 ~ g2 ~>")
  .sound("sawtooth")
  .lpf(400)
  .gain(0.3)
  .delay(0.5).delaytime(1/4).delayfeedback(0.5)
  .room(0.6).size(3.5)

// Dub 钢琴 — 回声处理
$: chord("<Cm7 Fm7>")
  .voicing()
  .sound("gm_electric_piano:1")
  .struct("x ~ ~ ~ ~ ~ ~ ~")
  .gain(0.15)
  .echo(3, 1/4, 0.6)
  .room(0.8).size(5)
  .lpf(2000)
```

### Ambient / 氛围音乐

```js
// Ambient — 无限空间、缓慢变化、漂浮感
setcpm(60/8)

$: chord("<Am9 Em11>")
  .voicing()
  .sound("gm_electric_piano:1")
  .gain(0.2)
  .room(0.9).size(6)
  .attack(0.8).release(2)
  .delay(0.4).delaytime(1).delayfeedback(0.6)
  .lpf(1500)

$: note("<a1 ~ e1 ~>")
  .sound("sawtooth")
  .lpf(sine.range(100, 800).slow(16))
  .gain(0.1)
  .room(0.95).size(8)
  .attack(1).release(3)

// 噪音纹理 — 模拟风声
$: sound("noise")
  .gain(sine.range(0.01, 0.04).slow(12))
  .hpf(2000)
  .lpf(4000)
  .room(0.95).size(10)

// 偶尔的钟声
$: sound("wind")
  .gain(0.05)
  .room(0.9).size(8)
  .delay(0.3).delaytime(2).delayfeedback(0.5)
```

### Drum & Bass / 鼓打贝斯

```js
// DnB — 快速 breakbeat + 深沉 sub bass
setcpm(174/4)

// Breakbeat 鼓点
$: stack(
    sound("bd ~ ~ bd ~ ~ ~ bd").gain(0.5),
    sound("~ ~ sn ~ ~ ~ sn ~").gain(0.3),
    sound("hh hh hh hh hh hh hh hh").gain(0.06).lpf(8000)
  ).bank("RolandTR909")
   .speed(perlin.range(0.98, 1.02))

// Sub bass — 深沉低音
$: note("<c1 ~ ~ c1 ~ eb1 ~ c1>")
  .sound("sawtooth")
  .lpf(150)
  .gain(0.5)
  .clip(0.8)

// 旋律层 — 锯齿波
$: n("0 4 7 12 7 4 0 ~")
  .scale("C3:minor")
  .sound("square")
  .lpf(sine.range(500, 3000).slow(4))
  .gain(0.12)
  .delay(0.2).delaytime(3/16).delayfeedback(0.3)
```

### Trance / 出神音乐

```js
// Trance — Supersaw 和弦 + 快速底鼓
setcpm(140/4)

// 底鼓 — 每拍
$: sound("bd bd bd bd")
  .bank("RolandTR909")
  .gain(0.5)

// Supersaw 和弦 — 层叠失谐
$: chord("<Am F C G>")
  .voicing()
  .sound("sawtooth")
  .superimpose(x => x.add(0.05))  // 失谐层
  .superimpose(x => x.add(-0.05)) // 另一层失谐
  .gain(0.15)
  .lpf(sine.range(1000, 4000).slow(8))
  .room(0.4).size(2.5)

// 开合帽
$: sound("~ oh ~ oh")
  .bank("RolandTR909")
  .gain(0.15)

// 酸性 arpeggio
$: n("0 4 7 12 7 4 0 4")
  .scale("A3:minor")
  .sound("square")
  .lpf(sine.range(200, 2000).slow(4))
  .lpq(8)
  .gain(0.12)
  .delay(0.2).delaytime(1/8).delayfeedback(0.4)
```

---

## 完整编曲 / Full Composition — 深夜 Techno

```js
// Midnight Techno — 深夜 Techno
// 催眠、渐变、空间感的多层编曲
setcpm(128/4)

stack(
  // 底鼓 — 每拍稳定
  sound("bd ~ bd ~ bd ~ bd ~")
    .bank("RolandTR909")
    .gain(0.5)
    .lpf(100),

  // 闭合帽 — 十六分音符
  sound("~ hh ~ hh ~ hh ~ hh")
    .bank("RolandTR909")
    .gain(0.08)
    .lpf(8000)
    .speed(perlin.range(0.98, 1.02)),

  // 酸性贝斯 — 滤波器扫描
  note("<c2 ~ c3 ~ bb1 ~ f2 ~>")
    .sound("sawtooth")
    .lpf(sine.range(200, 2000).slow(8))
    .lpq(6)
    .gain(0.35)
    .distort(0.2),

  // 合成器 pad — 氛围层
  chord("<Am7 Fmaj7>")
    .voicing()
    .sound("sawtooth")
    .gain(0.06)
    .lpf(sine.range(500, 2000).slow(12))
    .room(0.7).size(4)
    .attack(0.5).release(1),

  // 开合帽 — 偶尔点缀
  sound("~ ~ ~ ~ ~ oh ~ ~")
    .bank("RolandTR909")
    .gain(0.12)
    .room(0.3).size(2),

  // 噪音纹理 — 空间感
  sound("noise")
    .gain(sine.range(0.01, 0.03).slow(16))
    .hpf(3000)
    .room(0.9).size(8),

  // 偶尔的 clap
  sound("~ ~ ~ ~ ~ ~ ~ clap")
    .bank("RolandTR909")
    .gain(0.15)
    .room(0.4).size(2.5)
    .echo(2, 1/4, 0.4)
)
```

---

## 技巧提示 / Tips

- **滤波器扫描**: `.lpf(sine.range(200, 4000).slow(4))` 是电子音乐的灵魂
- **侧链压缩**: `.duckorbit()` 模拟 sidechain pumping 效果
- **bitcrush**: `.crush(4)` 制造 lo-fi 数字感
- **失谐叠加**: `.superimpose(x => x.add(0.05))` 制造宽广的 supersaw
- **TR-909/808**: `.bank("RolandTR909")` 和 `.bank("RolandTR808")` 是标准鼓机音色
- **延迟反馈**: `.delayfeedback(0.6)` 以上制造 dub echo 效果
- **噪音层**: `sound("noise")` + 滤波器 + 混响 = 有机纹理
- **速度变化**: `.speed(perlin.range(0.98, 1.02))` 添加微妙的有机感
