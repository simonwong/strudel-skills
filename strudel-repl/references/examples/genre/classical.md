# 古典与当代作曲 Classical & Contemporary Composition

## 简介 Introduction

在 Strudel 中探索古典与当代作曲技法：从巴赫的赋格到 Steve Reich 的相位偏移，
从十二音序列到算法生成音乐。Strudel 的模式变换功能天然适合这些作曲技术。
循环、迭代、镜像、多节拍——这些概念在代码中变得直观。

## 风格特征 Style Characteristics

- **节奏 Rhythm**: 复节拍、相位偏移、自由节奏
- **和声 Harmony**: 对位法、十二音、序列主义
- **音色 Timbre**: 弦乐、钢琴、木管、管弦乐色彩
- **技法 Techniques**: 赋格、卡农、相位、极简主义、算法

---

## 基础模式 Basic Patterns

### 简单卡农 Simple Canon
```js
// 两个声部相差一拍，形成卡农
$: n("0 2 4 7 4 2").scale("C4:major").sound("gm_piano")
$: n("0 2 4 7 4 2").scale("C4:major").sound("gm_piano").late(1/4)
```

### 上行音阶 Ascending Scale
```js
// run() 生成连续音阶
n(run(8)).scale("C4:major").sound("gm_piano")
```

### 镜像旋律 Mirror Melody
```js
// palindrome：正序 + 倒序，形成拱形
n("0 2 4 7 12 7 4 2").scale("C4:major").palindrome().sound("gm_piano")
```

---

## 进阶示例 Advanced Examples

### 赋格风格层叠 Fugue-Style Layering
```js
// 三个声部依次进入，模拟赋格
setcpm(90/4)
$: n("0 2 4 7 4 2 0 ~").scale("C4:minor").sound("gm_piano").gain(.4)
$: n("0 2 4 7 4 2 0 ~").scale("C3:minor").sound("gm_piano").late(2).gain(.4)
$: n("0 2 4 7 4 2 0 ~").scale("C2:minor").sound("gm_piano").late(4).gain(.4)
```

### Steve Reich 相位偏移 Phasing
```js
// 两个相同旋律以微小速度差播放，逐渐产生相位偏移
setcpm(100/4)
$: n("0 2 4 5 7 5 4 2").scale("C4:major").sound("gm_piano").gain(.4)
$: n("0 2 4 5 7 5 4 2").scale("C4:major").sound("gm_piano")
  .fast(1.01).gain(.4) // 微小速度差
```

### 极简主义重复 Minimalism
```js
// 短动机不断重复，逐渐加入变化
setcpm(110/4)
$: n("0 2 4 2").scale("C4:major").sound("gm_piano")
  .every(4, x => x.add(7)) // 每4次移调
  .every(8, rev) // 每8次反转
```

### 十二音序列 Twelve-Tone Row
```js
// 十二音技法：使用完整的半音序列
setcpm(80/4)
$: n("0 7 3 10 5 1 8 4 11 6 2 9").scale("C4:chromatic")
  .sound("gm_piano").slow(3)
$: n("9 2 6 11 4 8 1 5 10 3 7 0").scale("C3:chromatic")
  .sound("gm_piano").slow(3) // 逆行
```

### 弦乐四重奏 String Quartet
```js
// 四个声部，不同节奏密度
setcpm(80/4)
$: n("0 ~ 2 ~ 4 ~ 2 ~").scale("C4:minor").sound("gm_string_ensemble_1").gain(.25)
$: n("4 ~ ~ ~ 7 ~ ~ ~").scale("C4:minor").sound("gm_string_ensemble_1").gain(.25)
$: n("0 ~ ~ 4 ~ ~ 7 ~").scale("C3:minor").sound("gm_string_ensemble_1").gain(.25)
$: n("0 ~ ~ ~ ~ ~ ~ ~").scale("C2:minor").sound("gm_string_ensemble_1").slow(2).gain(.25)
```

### 算法旋律生成 Algorithmic Melody
```js
// 用随机 + 约束生成旋律
setcpm(100/4)
n("0 | 2 | 4 | 5 | 7").scale("C4:major").sound("gm_flute")
  .sometimes(x => x.add(12))
  .sometimes(x => x.add(7))
  .degradeBy(0.2).room(.5)
```

---

## 完整编曲示例 Full Compositions

### 赋格 F小调 Fugue in F Minor
```js
setcpm(88/4)

// 主题：赋格主题
let theme = n("5 3 1 0 1 3 5 7").scale("F3:minor")

// 高音声部：主题
$: theme.sound("gm_piano").gain(.35).room(.4)

// 中音声部：答题（移高五度，延迟进入）
$: theme.scale("C4:minor").sound("gm_piano").late(2).gain(.35).room(.4)

// 低音声部：对题
$: n("0 4 7 12 7 4 0 ~").scale("F2:minor").sound("gm_piano")
  .slow(2).gain(.35).room(.4)
```

### 极简花园 Minimalist Garden
```js
setcpm(100/4)

// 动机不断重复，逐渐叠加变化
$: n("0 2 4 2").scale("C4:major").sound("gm_piano")
  .every(4, x => x.add(7))
  .every(8, rev)
  .gain(.3).room(.5)

// 相位偏移的相同旋律
$: n("0 2 4 2").scale("C4:major").sound("gm_piano")
  .fast(1.02).gain(.3).room(.5)

// 低音锚点
$: note("c2").sound("gm_piano").slow(4).gain(.2).room(.5)

// 弦乐长音
$: note("c4 g4").sound("gm_string_ensemble_1").slow(4).room(.8).gain(.15)
```

### 管弦序曲 Orchestral Overture
```js
setcpm(72/4)

// 弦乐主题
$: n("0 ~ 2 ~ 4 ~ 7 ~ 4 ~ 2 ~ 0 ~ ~ ~").scale("C4:minor")
  .sound("gm_string_ensemble_1").room(.8).gain(.25)

// 木管对位
$: n("~ ~ ~ ~ 7 ~ 4 ~ ~ ~ ~ ~ 2 ~ 4 ~").scale("C5:minor")
  .sound("gm_oboe").room(.6).gain(.3)

// 铜管和弦（每小节一个）
$: chord("<Cm Ab Fm G7>").voicing().s("gm_string_ensemble_1")
  .slow(4).room(1).gain(.2)

// 定音鼓
$: sound("bd ~ ~ ~ ~ ~ ~ ~").room(.4).gain(.5)
```

---

## 技巧 Tips

- **late() 延迟**: 用 `.late(n)` 实现声部延迟进入，模拟卡农/赋格
- **palindrome() 镜像**: 自动创建正序+倒序的拱形旋律
- **iter() 迭代**: `.iter(4)` 将模式的起始点每次偏移一位，产生变奏
- **every() 周期变化**: `.every(n, fn)` 每 n 次应用变换，极简主义的核心
- **run() 音阶**: `run(12)` 生成完整八度的半音序列，配合 scale 使用
- **chromatic 半音阶**: `scale("C:chromatic")` 用于十二音技法
- **slow() 拉伸**: 不同声部用不同 slow 值创造节奏对比
- **复节拍**: `polymeter()` 让不同声部以不同周期循环
- **弦乐泛音**: 高音区 + 高混响模拟弦乐泛音效果
