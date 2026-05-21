# Workflow Patterns 工作流 Pattern

实用的调试、节奏设定和编排技巧。

## Debug with log 用 log 调试
```js
n("0 2 4 6").scale("C4:minor").sound("piano").log()
```

## Set tempo 设定速度
```js
setcpm(120/4)  // 120 BPM in 4/4
setcps(0.5)    // 0.5 cycles per second (default)
```

## Arrange sections 段落编排
```js
arrange(
  [4, sound("bd*4, hh*8")],
  [4, sound("bd*4, hh*8, [~ sd]*2")],
  [2, sound("bd*2, hh*4")],
  [2, silence]
)
```

## Polymeter 复拍子
```js
polymeter(
  note("c3 e3 g3"),
  note("c2 g2")
).sound("piano")
```

## Swing 摇摆
```js
s("hh*8").swing(4)
```

## Choose randomly 随机选择
```js
n(irand(8)).scale("C4:minor").sound("piano")
```

## Random melody 随机旋律
```js
n("0 | 2 | 4 | 6 | 7").scale("C4:minor").sound("piano")
```
