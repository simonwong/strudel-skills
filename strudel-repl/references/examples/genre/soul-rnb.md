# 灵魂乐 / R&B / Soul & R&B

> Rhodes 电钢琴的温暖音色、福音和声的丰富色彩、摇摆的 ghost note 节奏。
> 从 Motown 的经典律动到 D'Angelo 的 Neo-Soul，灵魂乐的核心是「律动与情感」。

## 风格特征 / Style Characteristics

- **节奏 / Rhythm**: 80-110 BPM，摇摆十六分音符，ghost note 丰富
- **和声 / Harmony**: 七和弦、九和弦、挂留和弦，福音色彩
- **音色 / Timbre**: Rhodes 电钢琴、无品贝斯、温暖人声
- **律动 / Feel**: 摇摆感强，留白多，强调「呼吸」

---

## 基础模式 / Basic Patterns

### 经典灵魂乐和弦 / Classic Soul Chords

```js
// 70 年代 Motown 和弦进行
setcpm(90/4)

$: chord("<Dm7 G7 Cmaj7 Fmaj7>")
  .voicings('lefthand')
  .sound("gm_electric_piano:1")
  .gain(0.35)
  .room(0.4).size(2)
  .lpf(2500)
```

### 摇摆鼓点 / Swing Drums

```js
// 灵魂乐鼓点 — rim 替代 snare，轻柔 hi-hat
$: sound("bd ~ rim ~, ~ hh ~ hh")
  .bank("RolandTR909")
  .gain("0.35 0 0.2 0, 0 0.12 0 0.12")
  .swing(4)
  .room(0.2).size(1.5)
```

---

## 进阶示例 / Advanced Examples

### Motown 经典律动 / Motown Groove

```js
// 经典 Motown — 贝斯先行，Rhodes 和弦点缀
setcpm(100/4)

$: n("~ 0 ~ 2 ~ 0 4 ~")
  .set(chord("<Am7 Dm7 E7 Am7>*2"))
  .mode("root:c2").voicing()
  .sound("gm_fretless_bass")
  .gain(0.45)
  .lpf(800)
  .room(0.2).size(1.5)
  .clip(0.8)

$: chord("<Am7 Dm7 E7 Am7>*2")
  .voicings('lefthand')
  .sound("gm_electric_piano:1")
  .struct("~ x ~ ~ ~ x ~ x")
  .gain(0.3)
  .room(0.35).size(2)
  .lpf(2200)
  .tremolosync(8).tremolodepth(0.2)

$: sound("bd ~ rim ~, ~ hh ~ hh")
  .bank("RolandTR909")
  .gain("0.35 0 0.22 0, 0 0.1 0 0.1")
  .room(0.15).size(1)
```

### Neo-Soul / D'Angelo 风格

```js
// Neo-Soul — 更复杂的和声，更松弛的律动
setcpm(88/4)

$: chord("<Dm9 Em7b5 A7b9 Gm9 C7b9 Fmaj7 Bm7b5 E7b9>")
  .voicings('lefthand')
  .superimpose(x => x.add(0.04))  // 轻微失谐，温暖感
  .sound("gm_electric_piano:1")
  .struct("x ~ ~ x ~ ~ x ~")
  .gain(0.28)
  .room(0.4).size(2.5)
  .delay(0.15).delaytime(1/6).delayfeedback(0.25)
  .lpf(2000)

$: n("~ 0 ~ 2 ~ 4 ~ ~")
  .set(chord("<Dm9 Em7b5 A7b9 Gm9 C7b9 Fmaj7 Bm7b5 E7b9>"))
  .mode("root:c2").voicing()
  .sound("gm_fretless_bass")
  .gain(0.4)
  .lpf(600)
  .room(0.25).size(1.5)
  .clip(1.2)

$: sound("bd ~ ~ rim, ~ hh ~ sh")
  .bank("RolandTR909")
  .gain("0.3 0 0 0.18, 0 0.1 0 0.08")
  .swing(6)
  .room(0.2).size(1.5)
  .speed(perlin.range(0.95, 1.0))
```

### 悲伤灵魂乐 / Sad Soul Ballad

```js
// 慢板灵魂乐，大量留白，忧郁色彩
setcpm(72/4)

$: chord("<Dm9 Em7b5 Am7 Gm9>*2")
  .dict('ireal').voicing()
  .sound("gm_electric_piano:1")
  .room(0.7).size(3)
  .vowel("<u o ae>")
  .gain(0.28)
  .attack(0.08)
  .tremolosync(6).tremolodepth(0.3).tremoloskew(0.8)
  .lpf(1800)

$: n("~ 0 ~ ~ 1 ~ ~ ~")
  .set(chord("<Dm9 Em7b5 Am7 Gm9>*2"))
  .mode("root:c2").voicing()
  .sound("gm_fretless_bass")
  .gain(0.4)
  .lpf(500)
  .room(0.3).size(2)
  .clip(1.5)

$: sound("rim ~ ~ ~ ~ ~ ~ ~")
  .bank("RolandTR707")
  .gain(0.12)
  .room(0.6).size(3)

$: n("0 ~ 2 ~ ~ 4 ~ ~")
  .set(chord("<Dm9 Em7b5 Am7 Gm9>*2"))
  .scale("C4:minor")
  .sound("gm_voice_oohs")
  .slow(4)
  .room(0.8).size(4)
  .gain(0.12)
  .attack(0.5).release(0.8)
  .delay(0.3).delaytime(1/3).delayfeedback(0.35)
```

---

## 完整编曲 / Full Composition — 深夜灵魂

```js
// Midnight Soul — 深夜灵魂乐
// 温暖、慵懒、深情的多层编曲
setcpm(82/4)

stack(
  // Rhodes — 和弦铺底，颤音温暖
  chord("<Dm9 G7 Cmaj7 Am7>*2")
    .voicings('lefthand')
    .superimpose(x => x.add(0.03))
    .sound("gm_electric_piano:1")
    .struct("x ~ ~ x ~ ~ x ~")
    .gain(0.28)
    .room(0.4).size(2.5)
    .tremolosync(8).tremolodepth(0.25)
    .lpf(2200),

  // 无品贝斯 — 滑音律动
  n("~ 0 ~ 2 ~ 0 4 ~")
    .set(chord("<Dm9 G7 Cmaj7 Am7>*2"))
    .mode("root:c2").voicing()
    .sound("gm_fretless_bass")
    .gain(0.42)
    .lpf(700)
    .room(0.2).size(1.5)
    .clip(0.9),

  // 鼓 — 灵魂乐节拍，ghost note
  stack(
    sound("bd ~ ~ ~ bd ~ ~ ~").gain(0.35),
    sound("~ ~ rim ~ ~ rim ~ ~").gain(0.18),
    sound("~ hh ~ hh ~ hh ~ hh").gain(0.1).lpf(6000)
  ).bank("RolandTR909")
   .room(0.15).size(1)
   .swing(4),

  // 人声 — 长音漂浮
  n("0 ~ ~ 2 ~ ~ 4 ~")
    .set(chord("<Dm9 G7 Cmaj7 Am7>*2"))
    .scale("C4:minor")
    .sound("gm_voice_oohs")
    .slow(2)
    .gain(0.12)
    .room(0.7).size(3.5)
    .attack(0.3).release(0.6)
    .delay(0.2).delaytime(1/3).delayfeedback(0.3),

  // 吉他点缀 — 偶尔的和弦刷奏
  chord("<Dm9 G7 Cmaj7 Am7>")
    .voicing()
    .sound("gm_jazz_guitar")
    .struct("~ ~ ~ ~ x ~ ~ ~")
    .gain(0.1)
    .room(0.5).size(2.5)
    .lpf(3000)
)
```

---

## 技巧提示 / Tips

- **voicings('lefthand')**: 灵魂乐和声的灵魂，自动分配左手钢琴 voicing
- **superimpose 微失谐**: `.superimpose(x => x.add(0.03))` 制造温暖的合唱感
- **tremolosync**: 颤音同步到节拍，`(8)` 是八分音符，`(6)` 是三连音
- **ghost note**: 鼓 pattern 中用低 gain 的 rim/hi-hat 制造「幽灵音」
- **swing(4)**: 四分音符摇摆，灵魂乐的典型感觉
- **留白**: 灵魂乐的美在于「不弹」，多用 `~` 创造呼吸空间
- **vowel**: `.vowel("<u o>")` 模拟人声共鸣，增加温暖感
