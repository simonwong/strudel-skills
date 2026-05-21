# Hip-Hop / Lo-Fi 嘻哈与低保真

## 简介 Introduction

Lo-Fi Hip-Hop 以柔和的鼓组、爵士和弦采样和磁带噪声为特征，营造慵懒放松的氛围。
Boom bap 节拍是经典嘻哈的根基，强调反拍军鼓和摇摆的hi-hat。
J Dilla 式的"human feel"让节拍听起来像是微醺的鼓手在演奏。

## 风格特征 Style Characteristics

- **节奏 Rhythm**: 85-95 BPM，boom bap 摇摆感，hi-hat 带 swing
- **和声 Harmony**: 爵士七和弦、九和弦，常用 ii-V-I 进行
- **音色 Timbre**: 电钢琴、upright bass、采样 vinyl 噪声
- **效果 Effects**: bit crush、磁带 wow/flutter、低通滤波、混响

---

## 基础节拍 Basic Patterns

### 经典 Boom Bap 节拍 Classic Boom Bap
```js
// 经典 boom bap：底鼓+军鼓+hi-hat
setcpm(90/4)
sound("bd [~ bd] ~ bd, ~ ~ sd ~, [hh ~]*4").bank("RolandTR909")
```

### Lo-Fi Hi-Hat 摇摆 Lofi Swing Hats
```js
// 摇摆感 hi-hat，力度变化营造人性
setcpm(88/4)
sound("hh*8").gain(".3 1 .5 1 .3 1 .5 1").swing(4)
```

### 低保真鼓组 Lofi Drum Kit
```js
// 带 bit crush 的鼓组，模拟老式采样器
setcpm(85/4)
sound("bd ~ sd ~, hh*8").crush(12).gain(.7)
```

---

## 进阶示例 Advanced Examples

### 爵士嘻哈和弦 Jazz Hop Chords
```js
// 爵士七和弦 + 电钢琴，慵懒氛围
setcpm(88/4)
chord("<Dm7 G7 C^7 F^7>").voicings('lefthand').note()
  .s("gm_electric_piano:1").room(.6).gain(.4)
```

### Dilla 式摇摆节拍 Dilla Swing
```js
// 微量时间偏移模拟 human feel
setcpm(86/4)
sound("bd ~ [~ bd] ~, ~ sd ~ sd, hh*8").bank("RolandTR909")
  .swing(4).speed(perlin.range(.95, 1.05))
```

### 采样切片 Sample Chopping
```js
// 切片 + 随机重组，模拟 MPC 采样工作流
setcpm(90/4)
s("rhodes").chop(8).slice(8, "0 2 4 6 1 3 5 7").room(.4)
```

### Vinyl 质感 Vinyl Texture
```js
// perlin 噪声模拟黑胶唱片的 wow & flutter
setcpm(88/4)
note("c4 e4 g4 bb4").sound("gm_electric_piano:1")
  .speed(perlin.range(.98, 1.02)).crush(14).room(.5)
```

---

## 完整编曲示例 Full Compositions

### 午夜咖啡 Midnight Coffee — Lo-Fi Study Beat
```js
setcpm(88/4)

// 底鼓+军鼓：经典 boom bap 骨架
$: sound("bd [~ bd] ~ bd, ~ ~ sd ~").bank("RolandTR909").crush(14)

// Hi-hat：带力度变化和摇摆
$: sound("[hh ~]*4").gain(".3 1 .5 1").swing(4).room(.2)

// 和弦：爵士电钢琴
$: chord("<Dm7 G7 C^7 Am7>").voicings('lefthand').note()
  .s("gm_electric_piano:1").room(.6).gain(.35)
  .speed(perlin.range(.99, 1.01)) // vinyl wow

// 贝斯：走根音，低通滤波
$: n("0 - - -").set(chord("<Dm7 G7 C^7 Am7>"))
  .mode("root:c2").voicing().s("gm_upright_bass").lpf(500).room(.3)
```

### 爵士弹跳 Jazz Bounce
```js
setcpm(92/4)

$: sound("bd ~ [~ bd] ~, ~ sd ~ sd, hh*8").bank("RolandTR808").crush(10)
$: chord("<Am7 Dm7 G7 C^7>").voicing().s("gm_electric_piano:1")
  .room(.5).struct("[~ x] [x ~] [~ x] [x ~]")
$: n("0 ~ 1 ~ 2 ~ 1 ~").set(chord("<Am7 Dm7 G7 C^7>"))
  .mode("root:c2").voicing().s("gm_upright_bass").lpf(600).clip(.8)
```

### Trap 808 模式 Trap 808 Pattern
```js
setcpm(140/4)

// 快速 hi-hat + 长 808 底鼓
$: sound("[hh hh]*8").gain(".3 1 .5 1 .3 1 .7 1").bank("RolandTR808")
$: sound("bd ~ ~ [~ bd] ~ bd ~ ~").bank("RolandTR808").gain(.9)
$: note("<c1 ~ ~ eb1 ~ f1 ~ g1 ~>").sound("sawtooth").lpf(300)
  .decay(.4).sustain(0)
```

---

## 技巧 Tips

- **Swing 是关键**: `.swing(4)` 给 hi-hat 加入摇摆感，这是 lo-fi 的灵魂
- **Bit Crush 模拟老设备**: `.crush(12-14)` 模拟 MPC/SP-404 的采样质感
- **Vinyl 效果**: `.speed(perlin.range(.98, 1.02))` 模拟黑胶唱片的 pitch wobble
- **低通滤波**: `.lpf(800-1500)` 切掉高频，营造温暖感
- **混响**: `.room(.4-.6)` 给乐器空间感，不要太干
- **爵士和弦**: 用 `voicings('lefthand')` 获得紧凑的爵士钢琴 voicing
- **力度变化**: hi-hat 用 `.gain(".3 1 .5 1")` 制造强弱交替
- **Crush 适度**: crush 值 12-14 保留质感，太低会变成噪声
