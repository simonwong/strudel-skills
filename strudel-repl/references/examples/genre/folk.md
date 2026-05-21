# 民谣 / Folk

> 木吉他指弹、五声音阶、质朴叙事。从 Bob Dylan 的公路叙事到凯尔特舞曲，再到中国民歌，
> 民谣的核心是「简单而动人」——用最少的音说最多的话。

## 风格特征 / Style Characteristics

- **节奏 / Rhythm**: 中速 90-120 BPM，轻柔的刷弦节奏，凯尔特用 6/8 拍
- **和声 / Harmony**: 大小调五声音阶、简单三和弦、偶尔挂留和弦
- **音色 / Timbre**: 原声吉他为主，长笛/卡林巴点缀，轻柔打击乐
- **律动 / Feel**: 自由、呼吸感强、留白多

---

## 基础模式 / Basic Patterns

### 指弹吉他 / Fingerpicking

```js
// 简单的民谣指弹，五度圈进行
setcpm(100/4)

$: note("<Am Em F C>").struct("x ~ x ~ x ~ x ~")
  .sound("gm_acoustic_guitar")
  .gain(0.5)
  .room(0.3).size(2)
  .lpf(3000)
```

### 五声旋律 / Pentatonic Melody

```js
// C 大调五声音阶旋律，卡林巴音色
$: n("0 2 4 ~ 5 4 2 ~")
  .scale("C4:major:pentatonic")
  .sound("gm_kalimba")
  .gain(0.4)
  .room(0.4).size(2)
  .delay(0.2).delaytime(1/4).delayfeedback(0.3)
```

---

## 进阶示例 / Advanced Examples

### Bob Dylan 叙事民谣 / Narrative Folk

```js
// Dm 和弦循环，口琴般的旋律，公路感
setcpm(96/4)

$: chord("<Dm Gm Am Dm>*2")
  .voicing()
  .sound("gm_acoustic_guitar")
  .struct("x ~ x ~ x ~ x ~")
  .gain(0.45)
  .room(0.25).size(1.5)
  .lpf(2800)

$: n("5 ~ 3 ~ 0 ~ 2 ~")
  .scale("D4:minor:pentatonic")
  .sound("gm_harmonica")
  .gain(0.25)
  .room(0.4).size(2)
  .delay(0.15).delaytime(1/3).delayfeedback(0.2)
  .vib("0.3:5")

$: sound("rim ~ ~ sh ~ ~ sh ~")
  .gain("0.2 0 0 0 0.12 0 0.12 0")
  .room(0.2)
```

### 凯尔特舞曲 / Celtic Jig

```js
// 6/8 拍凯尔特吉格，D 大调
setcpm(120/3)

// 吉他 — 6/8 拍刷弦
$: chord("<D G A D>").voicing()
  .sound("gm_acoustic_guitar")
  .struct("x ~ x x ~ x")
  .gain(0.4)
  .room(0.3).size(2)

// 长笛旋律 — 五声音阶跳跃
$: n("0 2 4 5 7 5 4 2")
  .scale("D4:major:pentatonic")
  .sound("gm_flute")
  .gain(0.3)
  .room(0.5).size(2.5)
  .delay(0.15).delaytime(3/8).delayfeedback(0.25)

// 贝斯 — 根音跳动
$: n("0 ~ ~ 0 ~ ~")
  .set(chord("<D G A D>"))
  .mode("root:c2").voicing()
  .sound("gm_acoustic_bass")
  .gain(0.45)
  .lpf(800)

// 打击 — bodhran 风格
$: sound("bd ~ ~ rim ~ rim")
  .gain("0.3 0 0 0.15 0 0.15")
  .room(0.15)
```

### 中国五声民歌 / Chinese Pentatonic Folk

```js
// 宫调式，古筝 + 笛子，空灵意境
setcpm(88/4)

$: n("0 4 5 7 9 7 5 4")
  .scale("C4:major:pentatonic")
  .sound("gm_kalimba")
  .gain(0.35)
  .room(0.6).size(3)
  .delay(0.2).delaytime(1/3).delayfeedback(0.35)
  .lpf(4000)

$: n("9 ~ 7 ~ 5 ~ 4 ~")
  .scale("C4:major:pentatonic")
  .sound("gm_flute")
  .gain(0.25)
  .room(0.7).size(3.5)
  .vib("0.5:4")
  .attack(0.2).release(0.8)

$: n("0 ~ ~ ~ 4 ~ ~ ~")
  .scale("C3:major:pentatonic")
  .sound("gm_acoustic_bass")
  .gain(0.4)
  .lpf(600)
  .room(0.3).size(2)
```

---

## 完整编曲 / Full Composition — 公路民谣

```js
// Road Folk — 公路民谣
// 开阔、自由、有呼吸感的多层编曲
setcpm(96/4)

stack(
  // 吉他 — 指弹和弦，轻柔刷奏
  chord("<Am F C G>*2")
    .voicing()
    .sound("gm_acoustic_guitar")
    .struct("x ~ x ~ x ~ x ~")
    .gain(0.4)
    .room(0.25).size(1.5)
    .lpf(3200),

  // 旋律 — 五声音阶，卡林巴点缀
  n("0 ~ 2 ~ 4 ~ 5 ~ 7 ~ 5 ~ 4 ~ 2 ~")
    .scale("A4:minor:pentatonic")
    .sound("gm_kalimba")
    .gain(0.3)
    .room(0.4).size(2)
    .delay(0.15).delaytime(1/4).delayfeedback(0.3),

  // 贝斯 — 根音呼吸
  n("~ 0 ~ ~ ~ 0 ~ ~")
    .set(chord("<Am F C G>*2"))
    .mode("root:c2").voicing()
    .sound("gm_acoustic_bass")
    .gain(0.45)
    .lpf(700)
    .room(0.2).size(1.5),

  // 打击 — rim + shaker，极简
  sound("rim ~ ~ sh ~ ~ sh ~")
    .gain("0.2 0 0 0 0.1 0 0.1 0")
    .room(0.15)
    .lpf(3000),

  // 长笛间奏 — 偶尔出现
  n("~ ~ ~ ~ 5 ~ ~ ~")
    .scale("A4:minor:pentatonic")
    .sound("gm_flute")
    .gain(0.15)
    .room(0.6).size(3)
    .vib("0.4:5")
    .attack(0.3).release(0.6)
)
```

---

## 技巧提示 / Tips

- **留白是关键**: 民谣的美在于「不弹的音」，多用 `~` 留出呼吸空间
- **五声音阶**: `minor:pentatonic` 和 `major:pentatonic` 是民谣最安全的选择
- **混响要适度**: `room(0.2-0.4)` 即可，模拟木吉他的自然共鸣
- **节奏自由**: 民谣不追求精确节拍，可以用 `perlin.range()` 添加微妙的速度变化
- **音量层次**: 旋律 `gain(0.3)` > 和弦 `gain(0.4)` > 贝斯 `gain(0.45)`，保持平衡
- **凯尔特特殊**: 用 `setcpm(120/3)` 设置 6/8 拍，吉格舞曲的典型节奏
