# 世界音乐 World Music

## 简介 Introduction

世界音乐涵盖全球各文化的传统与现代音乐风格。
非洲鼓乐以复杂的多层欧几里得节奏为核心；拉丁音乐融合切分与摇摆；
印度音乐以持续低音（drone）和塔布拉鼓为特色；日本五声音阶清雅空灵；
凯尔特音乐以 jig 和 reel 的舞曲节奏为标志；甘美兰以金属质感的交织音色闻名。

## 风格特征 Style Characteristics

- **节奏 Rhythm**: 欧几里得节奏、复节奏、不对称拍号
- **和声 Harmony**: 五声音阶、调式音阶、drone 持续音
- **音色 Timbre**: kalimba、taiko、agogo、steel drums、koto
- **特色 Features**: 交错节奏、呼应模式、循环往复

---

## 基础节拍 Basic Patterns

### 欧几里得非洲鼓 Euclidean African Drum
```js
// 三连音模式：非洲音乐的基础节奏单元
sound("bd(3,8), hh(5,8), sd(2,8)")
```

### 特雷索尔节奏 Tresillo Pattern
```js
// 古巴 tresillo：3+3+2 的经典划分
sound("bd(3,8), cb(5,8)")
```

### 五声音阶旋律 Pentatonic Melody
```js
// 东亚五声音阶，简洁空灵
n("0 2 4 6 0 4 2 0").scale("A4:minor:pentatonic").sound("gm_kalimba")
```

---

## 进阶示例 Advanced Examples

### 西非复节奏 West African Polyrhythm
```js
// 多层欧几里得节奏叠加，形成复节奏织体
setcpm(100/4)
$: sound("bell(5,8)").gain(.6)
$: sound("bd(3,8,0)").gain(.7)
$: sound("sd(2,8,4)").gain(.6)
$: sound("hh(5,16)").gain(.3)
```

### Bossa Nova 节奏 Bossa Nova Rhythm
```js
// bossa nova 的标志性节奏型：切分 + 摇摆
setcpm(120/4)
$: chord("<Dm7 G7 C^7 F^7>").struct("[x ~ x ~] [~ x ~ x]")
  .voicing().s("piano").room(.4).gain(.4)
$: n("0 ~ 1 ~ 2 ~ 1 ~").set(chord("<Dm7 G7 C^7 F^7>"))
  .mode("root:c2").voicing().s("gm_acoustic_bass").clip(.8)
```

### 印度 Drone + 塔布拉 Indian Drone & Tabla
```js
// 持续低音 drone + 循环节奏
setcpm(110/4)
$: note("c2").sound("sawtooth").lpf(400).gain(.2).room(1)
$: sound("bd(5,16), sd(2,16,4)").gain(.5)
$: n("0 2 4 5 7 5 4 2").scale("C4:major:pentatonic")
  .sound("gm_flute").room(.6).gain(.4)
```

### 日本五声音阶 Japanese Pentatonic
```js
// in scale：日本传统音阶，空灵而忧伤
setcpm(80/4)
$: n("0 ~ 2 ~ 4 ~ 6 ~").scale("A4:minor:pentatonic")
  .sound("gm_kalimba").room(.8).gain(.4)
$: note("a2").sound("triangle").gain(.15).room(1)
```

### 凯尔特 Jig 舞曲 Celtic Jig
```js
// 6/8 拍 jig：凯尔特舞曲的典型节奏
setcpm(140/3)
$: n("0 2 4 5 4 2 0 ~ 2 4 5 7").scale("G4:major").sound("gm_flute").gain(.5)
$: n("0 ~ ~ 0 ~ ~ 2 ~ ~ 0 ~ ~").scale("G2:major")
  .sound("gm_acoustic_bass").clip(.7)
$: sound("bd ~ ~ sd ~ ~, hh ~ hh ~ hh ~").gain(.4)
```

### 甘美兰交织 Gamelan Interlocking
```js
// 两个声部交错，模拟甘美兰的金属音色
setcpm(90/4)
$: n("0 ~ 4 ~ 2 ~ 6 ~").scale("C5:minor:pentatonic")
  .sound("triangle").gain(.3).room(.8)
$: n("~ 2 ~ 6 ~ 4 ~ 0").scale("C5:minor:pentatonic")
  .sound("triangle").gain(.3).room(.8).slow(2)
```

---

## 完整编曲示例 Full Compositions

### 非洲日出 African Sunrise
```js
setcpm(100/4)

// 铃铛：时间线模式，五拍循环
$: sound("bell(5,8)").gain(.5)

// 底鼓：三连音
$: sound("bd(3,8)").gain(.7)

// 军鼓：两拍偏移
$: sound("sd(2,8,4)").gain(.5)

// 卡林巴旋律：五声音阶
$: n("0 2 4 6 7 6 4 2").scale("A4:minor:pentatonic")
  .sound("gm_kalimba").room(.6).gain(.4)

// 低音呼应
$: n("0 ~ 4 ~ 2 ~ 6 ~").scale("A2:minor:pentatonic")
  .sound("gm_acoustic_bass").lpf(600).gain(.3)
```

### 拉萨黄昏 Lhasa Dusk
```js
setcpm(80/4)

// Drone 持续音：空灵背景
$: note("c2").sound("sawtooth").lpf(300).gain(.15).room(1).size(8)

// 长笛旋律：五声音阶 + 呼应
$: n("0 ~ 2 ~ 4 ~ 5 ~ 7 ~ 5 ~ 4 ~ 2").scale("C4:major:pentatonic")
  .sound("gm_flute").room(.8).gain(.35)

// 轻柔打击
$: sound("~ ~ rim ~ ~ ~ ~ rim").gain(.2).room(.6)

// 卡林巴点缀
$: n("7 ~ ~ 5 ~ ~ 4 ~").scale("C5:major:pentatonic")
  .sound("gm_kalimba").room(.7).gain(.25)
```

### 热带海岸 Tropical Coast
```js
setcpm(110/4)

// 钢鼓旋律
$: n("0 4 7 4 2 4 7 12").scale("C4:major:pentatonic")
  .sound("gm_steel_drums").room(.5).gain(.4)

// Bossa 和弦
$: chord("<Am7 Dm7 G7 C^7>").struct("[x ~ x ~] [~ x ~ x]")
  .voicing().s("piano").room(.4).gain(.3)

// 低音
$: n("0 ~ 1 ~ 2 ~ 1 ~").set(chord("<Am7 Dm7 G7 C^7>"))
  .mode("root:c2").voicing().s("gm_acoustic_bass").clip(.8)

// 沙锤 + agogo
$: sound("[~ shaker]*4, agogo(3,8)").gain(.3)
```

---

## 技巧 Tips

- **欧几里得节奏**: `sound("bd(3,8)")` 中 (hits,steps) 是核心参数，试不同的组合
- **旋转偏移**: `(3,8,2)` 第三个参数是旋转，改变重音位置
- **五声音阶**: `scale("C:major:pentatonic")` 或 `scale("A:minor:pentatonic")` 适合多种世界音乐
- **Drone 持续音**: 用单长音 + 高混响模拟印度/中东 drone 质感
- **交织模式**: 两个声部用互补的节奏位置，模拟甘美兰的 interlocking
- **Jig 节奏**: 用 `setcpm(bpm/3)` 配合三连音模式实现 6/8 拍
- **调式音阶**: 试试 `dorian`、`mixolydian` 等调式，适合凯尔特和中东风格
- **金属质感**: `triangle` 波形 + `.room(.8)` 模拟甘美兰的金属泛音
