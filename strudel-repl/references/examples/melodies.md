# Melodies & Basslines 旋律与贝斯线

从简单的音名旋律到复杂的 walking bass，展示 Strudel 中旋律写作的各种技巧。

## Simple melody with letters 简单音名旋律
```js
note("c e g b").sound("piano")
```

## Using scale degrees 音阶级进
```js
n("0 2 4 <[6,8] [7,9]>").scale("C:minor").sound("piano")
```

## Classy bassline 经典贝斯线
```js
note("<[c2 c3]*4 [bb1 bb2]*4 [f2 f3]*4 [eb2 eb3]*4>")
  .sound("gm_synth_bass_1").lpf(800)
```

## Classy melody 经典旋律
```js
n(`<
[~ 0] 2 [0 2] [~ 2]
[~ 0] 1 [0 1] [~ 1]
[~ 0] 3 [0 3] [~ 3]
[~ 0] 2 [0 2] [~ 2]
>*4`).scale("C4:minor").sound("gm_synth_strings_1")
```

## Shuffle groove with @ 用 @ 实现 shuffle 律动
```js
setcpm(60)
n("<[4@2 4] [5@2 5] [6@2 6] [5@2 5]>*2")
  .scale("<C2:mixolydian F2:mixolydian>/4")
  .sound("gm_acoustic_bass")
```

## Arpeggiated pattern 琶音
```js
n("0 2 4 6 4 2").scale("C4:minor").sound("piano").fast(2)
```

## Melody with rests 带休止的旋律
```js
n("0 ~ 2 ~ 4 ~ 6 ~").scale("C4:major").sound("gm_flute")
```

## Walking bass 行走贝斯
```js
n("<0 1 2 3 4 3 2 1>").scale("C2:major:pentatonic")
  .sound("gm_acoustic_bass").clip(0.8)
```

## Ambient pad with long notes 氛围长音 Pad
```js
n("0 4 7 12").scale("C3:minor").sound("gm_pad_new_age")
  .slow(4).room(0.8).size(4)
```

## Pentatonic melody 五声音阶旋律
```js
n("0 2 4 0 2 4 6 4").scale("A4:minor:pentatonic")
  .sound("gm_kalimba")
```

## Melody with octave jumps 八度跳跃旋律
```js
n("0 2 4 7 12 7 4 2").scale("C4:major").sound("piano")
  .sometimes(x => x.add(12))
```

## Call and response 呼应
```js
$: n("<0 2 4 2> ~ ~ ~").scale("C4:major").sound("piano")
$: n("~ ~ ~ <4 2 0 ~>").scale("C4:major").sound("piano")
```

## Simple bass pattern 简单贝斯
```js
note("<c2 ~ e2 ~ g2 ~ e2 ~>").sound("gm_synth_bass_1").lpf(600)
```

## Ascending/descending scale 上行/下行音阶
```js
n("0 1 2 3 4 5 6 7 6 5 4 3 2 1 0").scale("C4:major").sound("piano")
```
