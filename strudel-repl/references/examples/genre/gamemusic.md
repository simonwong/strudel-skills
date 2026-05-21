# 游戏音乐 Game Music

## 简介 Introduction

游戏音乐从 8-bit 芯片音色进化到现代管弦乐配乐，但 chiptune 的魅力从未褪色。
NES 时代的限制——方波、三角波、噪声通道——造就了最具辨识度的音乐风格。
马里奥的跳跃感、塞尔达的冒险感、洛克人的战斗感，都源于简洁有力的旋律设计。

## 风格特征 Style Characteristics

- **节奏 Rhythm**: 120-180 BPM，节奏鲜明，常有快速音符
- **和声 Harmony**: 简单调式，大调/小调，五声音阶
- **音色 Timbre**: 方波（主旋律）、三角波（贝斯）、噪声（鼓）
- **特色 Features**: 快速琶音、循环段落、能量感递进

---

## 基础模式 Basic Patterns

### 8-bit 方波旋律 8-Bit Square Melody
```js
// NES 风格方波旋律
setcpm(140/4)
n("0 4 7 12 7 4 0 ~").scale("C4:major").sound("square").gain(.3)
```

### 三角波贝斯 Triangle Bass
```js
// 三角波：8-bit 贝斯的标准音色
setcpm(140/4)
note("<c2 g2 bb1 f2>").sound("triangle").lpf(800)
```

### 噪声鼓 Noise Drums
```js
// 用噪声模拟 NES 的打击乐通道
setcpm(140/4)
sound("bd*4, [~ sd]*2, [hh ~]*4").crush(4).gain(.4)
```

---

## 进阶示例 Advanced Examples

### 平台跳跃 Platformer Theme
```js
// 马里奥风格：跳跃感旋律 + 强力鼓点
setcpm(160/4)
$: n("0 4 7 12 ~ 7 4 0 ~ 2 5 7 12 ~ 5 2 0").scale("C4:major")
  .sound("square").gain(.25)
$: note("<c2 ~ g2 ~ bb1 ~ f2 ~>").sound("triangle").lpf(600)
$: sound("bd ~ sd ~, [hh ~]*4").crush(4).gain(.35)
```

### 快速琶音 Fast Arpeggios
```js
// 洛克人风格：快速琶音 + 高能量
setcpm(170/4)
$: n("0 4 7 12 7 4").scale("C4:minor").sound("square").fast(2).gain(.2)
$: n("0 ~ 0 ~ 3 ~ 5 ~").scale("C3:minor").sound("triangle").lpf(700)
$: sound("bd*4, sd*2, [hh hh]*4").crush(4).gain(.35)
```

### RPG 冒险主题 RPG Overworld
```js
// 塞尔达风格：开阔感旋律 + 行进低音
setcpm(130/4)
$: n("0 ~ 2 ~ 4 ~ 7 ~ 12 ~ 7 ~ 4 ~ 2").scale("C4:major")
  .sound("square").gain(.2).room(.3)
$: n("0 ~ ~ ~ 4 ~ ~ ~ 5 ~ ~ ~ 7 ~ ~ ~").scale("C2:major")
  .sound("triangle").lpf(500)
$: sound("bd ~ ~ sd ~ ~ bd ~, [hh ~]*4").crush(4).gain(.3)
```

### Boss 战斗曲 Boss Battle
```js
// 紧张感：小调 + 快速节奏 + 低音驱动
setcpm(180/4)
$: n("5 4 2 0 2 4 5 7").scale("C4:minor").sound("square").fast(2).gain(.2)
$: note("<c2 c2 eb2 f2 g2 f2 eb2 c2>").sound("triangle")
  .lpf(600).fast(2)
$: sound("[bd bd]*4, [sd ~]*4, [hh hh]*8").crush(4).gain(.35)
```

### 和平村庄 Peaceful Village
```js
// 温馨氛围：慢速 + 大调 + 柔和音色
setcpm(100/4)
$: n("0 ~ 2 ~ 4 ~ 2 ~ 0 ~ 4 ~ 7 ~ 4 ~").scale("C4:major")
  .sound("sine").gain(.25).room(.6)
$: note("c2 ~ g2 ~").sound("triangle").lpf(400).slow(2)
$: sound("bd ~ ~ ~ ~ ~ ~ ~").crush(6).gain(.2).room(.4)
```

### 8-bit 鼓机 8-Bit Drum Machine
```js
// 模拟 NES 噪声通道的打击乐
setcpm(140/4)
$: sound("bd*4").crush(4).gain(.4)
$: sound("~ sd ~ sd").crush(4).gain(.35)
$: sound("[hh ~]*8").crush(2).gain(.2)
$: sound("~ ~ ~ [~ rim]").crush(4).gain(.25)
```

---

## 完整编曲示例 Full Compositions

### 星际冒险 Star Adventure
```js
setcpm(150/4)

// 主旋律：方波，明亮欢快
$: n("0 4 7 12 ~ 7 4 0 ~ 2 5 9 12 ~ 9 5 2").scale("C4:major")
  .sound("square").gain(.22)

// 对位旋律：方波移高八度
$: n("~ ~ ~ ~ 12 ~ ~ ~ ~ ~ ~ ~ 12 ~ ~ ~").scale("C5:major")
  .sound("square").gain(.15)

// 贝斯：三角波行进
$: note("<c2 g2 bb1 f2>").sound("triangle").lpf(600)

// 鼓：噪声通道
$: sound("bd ~ [~ bd] ~, ~ sd ~ sd, [hh ~]*4").crush(4).gain(.3)
```

### 地下迷宫 Underground Maze
```js
setcpm(130/4)

// 阴暗旋律：小调 + 慢速琶音
$: n("0 3 5 7 5 3 0 ~").scale("C4:minor").sound("square").gain(.2)
$: n("7 5 3 0 ~ 3 5 7").scale("C4:minor").sound("square").late(1/2).gain(.15)

// 低音：沉重行进
$: note("<c2 ~ eb2 ~ f2 ~ g2 ~>").sound("triangle").lpf(500)

// 鼓：稀疏但有力
$: sound("bd ~ ~ ~ ~ sd ~ ~, [~ hh]*4").crush(4).gain(.35)

// 氛围噪声
$: sound("white").gain(.02).lpf(2000).room(1)
```

### 最终决战 Final Showdown
```js
setcpm(180/4)

// 高速旋律：紧迫感
$: n("7 5 4 2 0 2 4 5 7 9 12 9 7 5 4 2").scale("C4:minor")
  .sound("square").gain(.2)

// 低音音型：驱动力
$: note("<c2 c2 eb2 f2 g2 f2 eb2 c2>").sound("triangle").lpf(500).fast(2)

// 强力鼓点
$: sound("[bd bd]*4, sd*4, [hh hh]*8").crush(4).gain(.35)

// 第二方波：应答
$: n("~ 12 ~ 9 ~ 7 ~ 5 ~ 4 ~ 2 ~ 0 ~").scale("C5:minor")
  .sound("square").gain(.15)
```

---

## 技巧 Tips

- **方波是主角**: `sound("square")` 是 8-bit 音乐的灵魂，主旋律首选
- **三角波做贝斯**: `sound("triangle")` + `.lpf(500-800)` 模拟 NES 贝斯通道
- **Crush 模拟芯片**: `.crush(2-4)` 将任何音色变成 8-bit 质感
- **噪声做鼓**: 用 `sound("bd")` + `.crush(4)` 模拟 NES 噪声打击通道
- **快速琶音**: `.fast(2)` 或更快，是洛克人/魂斗罗风格的关键
- **简洁旋律**: 限制音符数量（4-8个），好的游戏旋律容易记住
- **循环段落**: 游戏音乐本质是循环，用简洁的模式反复
- **能量递进**: 通过叠加声部和加快节奏来制造战斗紧张感
- **Gain 控制**: 方波容易刺耳，`.gain(.2-.3)` 保持舒适
