# Effects Showcase 音效展示

展示 Strudel 中各种音效的使用：滤波器、延迟、混响、失真、压缩等。

## Filter sweep 滤波器扫描
```js
note("<[c2 c3]*4 [bb1 bb2]*4 [f2 f3]*4 [eb2 eb3]*4>")
  .sound("sawtooth").lpf("200 1000 200 1000")
```

## Vowel formants 元音共振峰
```js
note("<[c3,g3,e4] [bb2,f3,d4] [a2,f3,c4] [bb2,g3,eb4]>")
  .sound("sawtooth").vowel("<a e i o>")
```

## Dynamic hihats with gain 动态踩镲
```js
sound("hh*16").gain("[.25 1]*4")
```

## Delay and reverb 延迟 + 混响
```js
sound("bd rim bd cp").delay(.5).room(.5)
```

## Stereo panning 立体声声像
```js
sound("numbers:1 numbers:2 numbers:3 numbers:4")
  .pan("0 0.3 .6 1")
```

## Reverse and jux 反转 + 立体声分离
```js
n("0 1 [4 3] 2 0 2 [~ 3] 4").sound("jazz").jux(rev)
```

## Delay with feedback 带反馈的延迟
```js
sound("bd rim").delay(.5).delaytime(1/4).delayfeedback(.6)
```

## Phaser 相位器
```js
note("c3").sound("sawtooth").phaser(2).phaserdepth(.8)
```

## Tremolo 颤音
```js
note("c3").sound("triangle").tremolosync(4).tremolodepth(.8)
```

## Bit crush 位压缩
```js
sound("bd sd").crush("<16 8 4 2>")
```

## Distortion 失真
```js
note("e3").sound("sawtooth").distort(2).lpf(2000)
```

## Resonant filter 共振滤波器
```js
note("c3").sound("sawtooth").lpf(800).lpq(20)
```

## Compressor 压缩器
```js
sound("bd*4, sd*2, hh*8").compressor("-20:10:5:.002:.05")
```

## Combining effects 组合音效
```js
note("c3 e3 g3").sound("sawtooth")
  .lpf(1000).room(.5).delay(.3).pan("0 .5 1")
```

## Filter type switching 滤波器类型切换
```js
note("c3").sound("sawtooth").lpf(800).ftype("<0 1 2>")
```

## Heavy reverb 重混响
```js
sound("bd ~ ~ ~").room(1).size(10).roomlp(3000)
```

## Sidechain ducking 侧链闪避
```js
$: sound("bd*4").duckorbit(2)
$: note("c3").sound("sawtooth").orbit(2).duckdepth(.8)
```

## Auto-pan with jux jux 自动声像
```js
s("hh*8").jux(rev).juxBy(0.5, x => x.speed(2))
```
