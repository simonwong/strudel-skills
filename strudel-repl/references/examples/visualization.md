# Visualization 可视化

在 Strudel REPL 中实时可视化音频信号和 pattern。

## Waveform scope 波形示波器
```js
note("c3 e3 g3").sound("sawtooth")._scope()
```

## Pitch wheel 音高轮
```js
n("0 2 4 6 4 2 0").scale("C4:minor").sound("piano")._pitchwheel()
```

## Piano roll (punchcard) 钢琴卷帘
```js
n("0 2 4 6 4 2").scale("C4:minor").sound("piano").punchcard()
```

## Scope on all layers 所有层可视化
```js
$: sound("bd*4, hh*8")._scope()
$: note("<c2 g2>").sound("bass").lpf(600)._scope()
$: chord("<Cm7 Fm7>").voicing().s("piano")._scope()
```
