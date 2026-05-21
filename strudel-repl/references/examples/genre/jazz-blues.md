# 爵士 / 蓝调 / Jazz & Blues

> 爵士和声的复杂色彩、行走贝斯的流动感、摇摆节奏的律动。
> 从 12 小节蓝调到 Coltrane 的 Giant Steps，爵士的核心是「对话与即兴」。

## 风格特征 / Style Characteristics

- **节奏 / Rhythm**: 120-180 BPM，摇摆八分音符，三连音律动
- **和声 / Harmony**: 七和弦、九和弦、十三和弦、变化和弦、ii-V-I 进行
- **音色 / Timbre**: 钢琴、原声贝斯、爵士鼓刷、空心吉他
- **律动 / Feel**: 摇摆感强，强调「走在」节拍上

---

## 基础模式 / Basic Patterns

### ii-V-I 进行 / ii-V-I Progression

```js
// 经典爵士 ii-V-I
setcpm(120/4)

$: chord("<Dm7 G7 Cmaj7>")
  .voicings('lefthand')
  .sound("gm_electric_piano:1")
  .gain(0.35)
  .room(0.3).size(2)
  .lpf(2500)
```

### 行走贝斯 / Walking Bass

```js
// 行走贝斯 — 四分音符流动
$: n("0 2 4 5 7 5 4 2")
  .set(chord("<Dm7 G7 Cmaj7>*2"))
  .mode("root:c2").voicing()
  .sound("gm_acoustic_bass")
  .gain(0.45)
  .lpf(800)
  .room(0.2).size(1.5)
```

---

## 进阶示例 / Advanced Examples

### 爵士三重奏 / Jazz Trio

```js
// 钢琴 + 贝斯 + 鼓，经典三重奏
setcpm(130/4)

$: chord("<Dm7 G7 Cmaj7 A7>*2")
  .voicings('lefthand')
  .sound("gm_electric_piano:1")
  .struct("x ~ x ~ x ~ x ~")
  .gain(0.3)
  .room(0.3).size(2)
  .lpf(2200)
  .delay(0.1).delaytime(1/6).delayfeedback(0.2)

$: n("0 ~ 2 ~ 4 ~ 5 ~")
  .set(chord("<Dm7 G7 Cmaj7 A7>*2"))
  .mode("root:c2").voicing()
  .sound("gm_acoustic_bass")
  .gain(0.45)
  .lpf(700)
  .room(0.2).size(1.5)
  .clip(0.8)

$: stack(
    sound("bd ~ ~ ~ bd ~ ~ ~").gain(0.3),
    sound("~ ~ sn ~ ~ ~ sn ~").gain(0.2),
    sound("hh ~ hh ~ hh ~ hh ~").gain(0.08).lpf(8000)
  ).bank("RolandTR707")
   .swing(4)
   .room(0.15).size(1)
```

### 12 小节蓝调 / 12-Bar Blues

```js
// 经典 12 小节蓝调：I-I-I-I / IV-IV-I-I / V-IV-I-V
setcpm(110/4)

$: chord("<E7!4 A7!2 E7!2 B7 A7 E7 B7>")
  .voicings('lefthand')
  .sound("gm_electric_piano:1")
  .struct("x ~ x ~ x ~ x ~")
  .gain(0.3)
  .room(0.25).size(2)
  .lpf(2000)

$: n("~ 0 ~ 2 ~ 4 ~ 5")
  .set(chord("<E7!4 A7!2 E7!2 B7 A7 E7 B7>"))
  .mode("root:c2").voicing()
  .sound("gm_acoustic_bass")
  .gain(0.45)
  .lpf(700)
  .room(0.2).size(1.5)
  .clip(0.7)

// 蓝调吉他 — 推弦 licks
$: n("3 ~ 5 ~ b7 ~ 5 ~")
  .set(chord("<E7!4 A7!2 E7!2 B7 A7 E7 B7>"))
  .scale("E3:minor:pentatonic")
  .sound("gm_overdrive_guitar")
  .gain(0.2)
  .lpf(1800)
  .vib("0.6:6")
  .room(0.4).size(2.5)
  .delay(0.2).delaytime(1/6).delayfeedback(0.3)
```

### Giant Steps 风格 / Coltrane Changes

```js
// Coltrane 变化 — 大三度循环和声
setcpm(160/4)

$: chord("<Bmaj7 D7 Gmaj7 Bb7 Ebmaj7 Am7 D7 Gmaj7 Bb7 Ebmaj7 F#7 Bmaj7>")
  .voicings('lefthand')
  .sound("gm_electric_piano:1")
  .gain(0.3)
  .room(0.3).size(2)
  .lpf(2200)

$: n("0 ~ 2 ~ 4 ~ 5 ~")
  .set(chord("<Bmaj7 D7 Gmaj7 Bb7 Ebmaj7 Am7 D7 Gmaj7 Bb7 Ebmaj7 F#7 Bmaj7>"))
  .mode("root:c2").voicing()
  .sound("gm_acoustic_bass")
  .gain(0.45)
  .lpf(700)
  .room(0.15).size(1)
  .clip(0.6)
```

### Bossa Nova / 波萨诺瓦

```js
// Bossa Nova — 巴西爵士，轻柔的切分节奏
setcpm(120/4)

$: chord("<Dm9 G7 Cmaj7 Fmaj7 Bm7b5 E7 Am7 D7>")
  .voicings('lefthand')
  .sound("gm_jazz_guitar")
  .struct("x ~ x x ~ x ~ x")
  .gain(0.3)
  .room(0.25).size(2)
  .lpf(3000)

$: n("0 ~ ~ 2 ~ 4 ~ ~")
  .set(chord("<Dm9 G7 Cmaj7 Fmaj7 Bm7b5 E7 Am7 D7>"))
  .mode("root:c2").voicing()
  .sound("gm_acoustic_bass")
  .gain(0.4)
  .lpf(600)
  .room(0.2).size(1.5)
  .clip(1.0)

// Bossa 鼓点 — 轻柔的刷奏
$: sound("bd ~ sh ~, ~ ~ sn ~")
  .gain("0.25 0 0.1 0, 0 0 0.15 0")
  .room(0.2).size(1.5)
```

---

## 完整编曲 / Full Composition — 深夜爵士

```js
// Midnight Jazz — 深夜爵士俱乐部
// 温暖、私密、摇摆的多层编曲
setcpm(120/4)

stack(
  // 钢琴 — 和弦 comping
  chord("<Dm7 G7 Cmaj7 A7>*2")
    .voicings('lefthand')
    .sound("gm_electric_piano:1")
    .struct("~ x ~ x ~ x ~ x")
    .gain(0.3)
    .room(0.35).size(2.5)
    .lpf(2200)
    .delay(0.1).delaytime(1/6).delayfeedback(0.2),

  // 行走贝斯
  n("0 ~ 2 ~ 4 ~ 5 ~")
    .set(chord("<Dm7 G7 Cmaj7 A7>*2"))
    .mode("root:c2").voicing()
    .sound("gm_acoustic_bass")
    .gain(0.45)
    .lpf(700)
    .room(0.2).size(1.5)
    .clip(0.8),

  // 鼓 — 摇摆节奏
  stack(
    sound("bd ~ ~ ~ bd ~ ~ ~").gain(0.3),
    sound("~ ~ sn ~ ~ ~ sn ~").gain(0.2),
    sound("~ hh ~ hh ~ hh ~ hh").gain(0.06).lpf(9000)
  ).bank("RolandTR707")
   .swing(4)
   .room(0.15).size(1),

  // 贝斯独奏 — 偶尔的旋律线
  n("7 ~ 5 ~ 4 ~ 2 ~")
    .set(chord("<Dm7 G7 Cmaj7 A7>*2"))
    .scale("C4:major")
    .sound("gm_acoustic_bass")
    .gain(0.15)
    .lpf(1200)
    .room(0.3).size(2)
    .delay(0.15).delaytime(1/4).delayfeedback(0.25)
    .off(1/8, x => x.add(12)),  // 高八度叠加

  // 吉他点缀 — 和弦 hits
  chord("<Dm7 G7 Cmaj7 A7>")
    .voicing()
    .sound("gm_jazz_guitar")
    .struct("~ ~ ~ ~ x ~ ~ ~")
    .gain(0.08)
    .room(0.5).size(2.5)
    .lpf(3500)
)
```

---

## 技巧提示 / Tips

- **voicings('lefthand')** vs **voicings('righthand')**: 左手是和弦基础，右手是旋律层
- **swing(4)**: 四分音符摇摆，爵士的典型感觉
- **rootNotes()**: 提取根音用于行走贝斯
- **ii-V-I**: 爵士最常用的和声进行，`<Dm7 G7 Cmaj7>`
- **12-Bar Blues**: `<I!4 IV!2 I!2 V IV I V>` 的经典结构
- **变化和弦**: `7b9`, `7#9`, `7alt` 等增加色彩
- **Bossa Nova**: 切分节奏 `"x ~ x x ~ x ~ x"` 制造巴西律动
- **Coltrane Changes**: 大三度循环 `Bmaj7 → D7 → Gmaj7 → Bb7 → Ebmaj7`
