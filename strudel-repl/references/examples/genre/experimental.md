# 实验与前卫 Experimental & Avant-garde

## 简介 Introduction

实验音乐打破常规，探索声音的边界。从 John Cage 的偶然音乐到 Merzbow 的噪声墙，
从 La Monte Young 的持续音到 Autechre 的算法节拍。
Strudel 的随机函数、时间变换和声音处理工具，让实验作曲变得触手可及。

## 风格特征 Style Characteristics

- **节奏 Rhythm**: 非传统节拍、随机节奏、时间拉伸
- **和声 Harmony**: 无调性、微分音、纯噪声
- **音色 Timbre**: 噪声源、bit crush、颗粒化、glitch
- **技法 Techniques**: 随机生成、drone、时间操控、degradation

---

## 基础模式 Basic Patterns

### 白噪声纹理 White Noise Texture
```js
// 最简单的噪声：白噪声 + 滤波
sound("white").gain(.1).lpf(sine.range(200, 4000).slow(8))
```

### 随机音符 Random Notes
```js
// irand 生成随机音高，配合 scale 保持调性
n(irand(8)).scale("C4:minor").sound("piano").degradeBy(0.3)
```

### Bit Crush 碎片 Crushed Fragments
```js
// crush + degrade 制造 glitch 质感
sound("bd sd").crush(4).degradeBy(0.5)
```

---

## 进阶示例 Advanced Examples

### 生成式氛围 Generative Ambient
```js
// 随机选择 + 滤波变化 = 每次不同的氛围
setcpm(60/4)
$: n("0 | 2 | 4 | 7 | 9").scale("C4:major:pentatonic")
  .sound("gm_pad_new_age").room(1).size(6)
  .lpf(sine.range(500, 3000).slow(6)).gain(.25)
$: note("c2").sound("triangle").gain(.1).lpf(200).room(1)
```

### 噪声墙壁 Noise Wall
```js
// 多层噪声叠加，滤波器塑形
setcpm(60/4)
$: sound("white").gain(.04).lpf(800)
$: sound("pink").gain(.05).hpf(200).lpf(2000)
$: sound("brown").gain(.06).lpf(400)
```

### Glitch 节拍 Glitch Beats
```js
// crush + degrade + 随机速度 = glitch 美学
setcpm(120/4)
sound("bd ~ sd ~, [hh ~]*4")
  .crush(rand.range(2, 8))
  .degradeBy(0.3)
  .speed(perlin.range(0.5, 2))
```

### 时间拉伸实验 Time-Stretch Experiment
```js
// 用 scrub 和 loop 实现极端时间拉伸
setcpm(60/4)
s("rhodes").scrub(sine.range(0, 1).slow(8)).room(1)
```

### Drone 持续音 Drone
```js
// 单音持续 + 调制，探索泛音
setcpm(60/4)
note("c2").sound("sawtooth").lpf(sine.range(100, 2000).slow(10))
  .room(1).size(10).gain(.2)
```

### 随机切片 Random Slicing
```js
// 随机切片重组采样
setcpm(100/4)
s("breaks165").slice(16, irand(16)).degradeBy(0.4)
  .crush(rand.range(4, 12)).room(.3)
```

---

## 完整编曲示例 Full Compositions

### 电子迷雾 Electric Fog
```js
setcpm(60/4)

// 底层：粉色噪声
$: sound("pink").gain(.03).lpf(600).room(1)

// 中层：随机音符飘浮
$: n("0 | 2 | 4 | 7 | 9").scale("C4:major:pentatonic")
  .sound("sine").degradeBy(0.5).room(1).size(8).gain(.15)

// 上层：glitch 打击
$: sound("~ ~ bd ~").crush(rand.range(2, 8)).degradeBy(0.6)
  .room(.5).gain(.2)

// 调制层：滤波器扫描
$: sound("white").gain(.015).lpf(sine.range(100, 5000).slow(12))
```

### 碎片记忆 Fragmented Memory
```js
setcpm(90/4)

// 切碎的采样
$: s("rhodes").chop(16).slice(16, "0 4 8 12 2 6 10 14")
  .degradeBy(0.3).crush(8).room(.4)

// 失真的贝斯
$: note("c2").sound("sawtooth").lpf(400).distort(3).gain(.2)

// 随机噪声打击
$: sound("white").gain(.05).decay(.02).sustain(0)
  .degradeBy(0.7).crush(2)

// 漂移的和弦
$: chord("<Am7 ~ Dm7 ~>").voicing().s("piano")
  .room(1).size(10).gain(.15).speed(perlin.range(.97, 1.03))
```

### 熵之花园 Entropy Garden
```js
setcpm(70/4)

// 生成式旋律：每次播放都不同
$: n("0 | 2 | 4 | 5 | 7 | 9 | 11").scale("C4:dorian")
  .sound("gm_kalimba").degradeBy(0.4).room(.8).gain(.2)

// 随机节奏的打击
$: sound("bd").struct("x ~ ~ x ~ ~ ~ x").degradeBy(0.5)
  .crush(rand.range(4, 16)).gain(.3)

// Drone 底座
$: note("c2").sound("triangle").lpf(sine.range(100, 800).slow(15))
  .gain(.12).room(1).size(10)

// 随机噪声脉冲
$: sound("white").gain(.02).decay(.05).sustain(0).degradeBy(.8)
  .lpf(rand.range(200, 8000))
```

### 延迟的钟声 Delayed Bells
```js
setcpm(60/4)

// 钟声 + 长延迟
$: n("0 | 7 | 12").scale("C5:major:pentatonic")
  .sound("triangle").echo(6, 1/3, .6).room(1).gain(.2)

// 低频 drone
$: note("c1").sound("sawtooth").lpf(150).gain(.1)

// 随机金属声
$: sound("white").decay(.01).sustain(0).gain(.03)
  .crush(2).degradeBy(.9).hpf(4000)
```

---

## 技巧 Tips

- **degradeBy() 随机移除**: `.degradeBy(0.3)` 移除 30% 的事件，制造稀疏感
- **rand vs perlin**: `rand` 完全随机跳跃，`perlin` 平滑渐变，选择取决于风格
- **crush 极端化**: `.crush(2)` 产生最极端的数字化质感
- **噪声源选择**: `white`（亮）、`pink`（平衡）、`brown`（暗），各有特色
- **room + size 大空间**: `.room(1).size(10)` 制造巨大的空间感
- **scrub 时间操控**: `.scrub(sine.range(0,1).slow(8))` 缓慢扫过采样
- **echo 长反馈**: `.echo(6, 1/3, .6)` 制造密集的延迟尾巴
- **distort 失真**: `.distort(2-3)` 给任何声音加入失真边缘
- **组合多种随机**: `degradeBy` + `rand.range` + `perlin` 叠加使用效果更丰富
