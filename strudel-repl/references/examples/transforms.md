# Pattern Transforms Pattern 变换

展示 Strudel 的核心 pattern 变换函数：偏移、回声、迭代、随机、结构等。

## Offset with add 偏移 + 音高叠加
```js
n("0 [4 <3 2>] <2 3> [~ 1]")
  .off(1/16, x=>x.add(4))
  .scale("C:minor").sound("piano")
```

## Echo 回声
```js
s("bd sd").echo(3, 1/6, .8)
```

## Iteration 迭代旋转
```js
note("0 1 2 3".scale('A minor')).iter(4)
```

## Sometimes 随机应用
```js
s("hh*8").sometimes(x=>x.speed("0.5"))
```

## Chunk processing 分块处理
```js
"0 1 2 3".chunk(4, x=>x.add(7)).scale("A:minor").note()
```

## Every 每 N 周期应用
```js
n("0 1 2 3").scale("C:minor").every(4, rev).sound("piano")
```

## Fast and slow 加速与减速
```js
sound("bd sd hh cp").fast(2) // 加倍速度
sound("bd sd hh cp").slow(2) // 减半速度
```

## Superimpose 叠加变换
```js
n("0 2 4").scale("C4:minor").superimpose(x => x.add(7)).sound("piano")
```

## Palindrome 前后交替
```js
n("0 1 2 3 4").scale("C4:minor").palindrome().sound("piano")
```

## Off with rev 偏移 + 反转
```js
sound("bd sd").off(1/8, rev)
```

## Echo with decay 衰减回声
```js
note("c3").sound("triangle").echo(4, 1/8, 0.7)
```

## Jux with filter jux + 滤波器
```js
s("hh*8").jux(x => x.lpf(1000))
```

## Layer multiple transforms 多层变换
```js
n("0 2 4 6").scale("C4:minor").sound("piano")
  .layer(
    x => x.add(7),
    x => x.add(12)
  )
```

## Degrade 随机删除
```js
s("hh*16").degradeBy(0.3)
```

## Sometimes with add 随机八度
```js
n("0 1 2 3 4 5 6 7").scale("C4:major").sound("piano")
  .sometimes(x => x.add(12))
```

## Rarely with speed 偶尔变速
```js
s("hh*8").rarely(x => x.speed(0.5))
```

## Struct 结构化节奏
```js
note("c3 e3 g3").struct("x ~ x ~ x ~ ~ x")
```

## Mask 遮罩
```js
n("0 1 2 3 4 5 6 7").scale("C4:major").sound("piano")
  .mask("<1 0 1 0>")
```

## Chunk with add 分块音高偏移
```js
n("0 1 2 3 4 5 6 7").scale("C4:major").sound("piano")
  .chunk(4, x => x.add(7))
```
