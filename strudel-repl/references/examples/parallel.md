# Parallel Patterns with `$:` 并行 Pattern

使用 `$:` 同时运行多个独立的 pattern 层，构建完整的音乐编排。

## Basic parallel layers 基础并行层
```js
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
$: note("<c2 bb1 f2 eb2>").sound("gm_synth_bass_1").lpf(800)
$: n("0 2 4 <6 7>").scale("C4:minor").sound("piano")

// _$ 静音某一层
_$: note("<c2 bb1>").sound("gm_synth_bass_1")
```

## Multi-layer beat 多层鼓组
```js
$: sound("bd*4").bank("RolandTR909")
$: sound("[~ sd]*2").bank("RolandTR909")
$: sound("hh*8").bank("RolandTR909").gain("[.25 1]*4")
```

## Drum + bass + chords 鼓 + 贝斯 + 和弦
```js
$: sound("bd*4, [~ sd]*2, hh*8").bank("RolandTR909")
$: note("<c2 g2 bb1 f2>").sound("gm_synth_bass_1").lpf(600)
$: chord("<Cm7 Fm7 Bb7 Eb^7>").voicing().s("gm_electric_piano:1").room(.5)
```

## Ambient layers 氛围层
```js
$: note("<c3 e3 g3>").sound("pad").slow(4).room(.8)
$: note("<c2 ~ ~ g2>").sound("bass").lpf(400)
$: sound("rim ~ ~ ~").room(.6).gain(.3)
```
