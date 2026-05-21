# Synths 合成器

展示 Strudel 的各种合成引擎：基础波形、FM 合成、加法合成、波表、ZZFX 等。

## Basic waveforms 基础波形
```js
note("c3 e3 g3").sound("sine")
note("c3 e3 g3").sound("triangle")
note("c3 e3 g3").sound("sawtooth")
note("c3 e3 g3").sound("square")
```

## Noise 噪声源
```js
sound("white").gain(0.2)
sound("pink").gain(0.2)
sound("brown").gain(0.2)
```

## FM synthesis FM 合成
```js
note("c3 e3 g3").sound("sawtooth").fm(4).fmh("<1 2 3>")
```

## FM with envelope FM + 包络
```js
note("c3 e3 g3").fm(4).fmattack(0).fmdecay(.2).fmsustain(.5)
```

## FM harmonicity FM 谐波比
```js
note("c3").fm(4).fmh("<1 1.5 2 3>").sound("sawtooth")
```

## Additive synthesis 加法合成
```js
note("c3").sound("sawtooth").partials("1 0.5 0.25 0.125")
```

## Custom waveform 自定义波形
```js
note("c3").sound("user").partials("1 .5 .3 .2 .1")
```

## Vibrato 颤音
```js
note("c3").sound("sine").vib(4).vibmod(0.5)
```

## Vibrato with mini-notation 迷你标记颤音
```js
note("c3").vib("<.5 1 2 4>:12")
```

## ADSR envelope ADSR 包络
```js
note("c3 e3 g3").sound("sawtooth")
  .attack(0).decay(.1).sustain(.5).release(.2)
```

## ADSR shorthand ADSR 简写
```js
note("c3 e3 g3").sound("sawtooth").adsr("0:.1:.5:.2")
```

## Filter envelope 滤波器包络
```js
note("c3 e3 g3").sound("sawtooth").lpf(300)
  .lpa(.5).lpd(.3).lps(.2).lpr(.1).lpenv(4)
```

## Pitch envelope 音高包络
```js
note("c").sound("sine")
  .penv(12).pdec(.5).pcurve(1)
```

## Pitch envelope down 下行音高包络
```js
note("c3").sound("sine")
  .penv(-12).pdec(.3).pcurve(1).panchor(1)
```

## Wavetable 波表
```js
note("c3").s("wt_square").loopBegin(0.1).loopEnd(0.5)
```

## ZZFX synth ZZFX 合成器
```js
note("c2 eb2 f2 g2")
  .s("{z_sawtooth z_tan z_noise z_sine z_square}%4")
```

## SuperSaw 超级锯齿
```js
note("c3").sound("supersaw").lpf(2000).gain(0.3)
```

## Synth with effects 合成器 + 音效
```js
note("c3 e3 g3").sound("sawtooth")
  .lpf(1000).room(.5).delay(.3)
  .attack(0).decay(.1).sustain(.6).release(.3)
```
