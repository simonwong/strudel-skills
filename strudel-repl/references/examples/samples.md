# Samples 采样

展示 Strudel 中采样的加载、操控和创意使用：鼓机音色库、颗粒化、切片、循环等。

## Load custom samples 加载自定义采样
```js
samples({ mydrum: 'path/to/file.wav' }, 'https://base-url/')
```

## GitHub shortcut GitHub 快捷加载
```js
samples('github:tidalcycles/dirt-samples')
```

## Drum machine banks 鼓机音色库
```js
s("bd sd,hh*8").bank("RolandTR909")
s("bd sd,hh*8").bank("RolandTR808")
s("bd sd,hh*8").bank("RolandTR707")
s("bd sd,hh*8").bank("RolandTR505")
```

## Sample selection 采样选择
```js
sound("hh:0 hh:1 hh:2 hh:3")
```

## Granular with chop 颗粒化
```js
s("rhodes").chop(4).rev().loopAt(2)
```

## Slicing 切片
```js
s("breaks165").slice(8, "0 1 2 3 4 5 6 7")
```

## Splice (with speed adjustment) 拼接（带速度调整）
```js
s("breaks165").splice(8, "0 1 2 3 4 5 6 7")
```

## Loop 循环
```js
s("casio").loop(1).loopBegin(0).loopEnd(.5)
```

## Loop at cycle length 按周期循环
```js
s("breaks165").loopAt(4)
```

## Scrub through sample 刷读采样
```js
s("rhodes").scrub(sine.range(0, 1).slow(4))
```

## Speed manipulation 速度操控
```js
s("bd").speed("<1 2 0.5 -1>")
```

## Begin and end 起止点
```js
s("rhodes").begin(0.25).end(0.75)
```

## Cut group (hi-hat choke) 切断组（踩镲互斥）
```js
s("[oh hh]*4").cut(1)
```

## Fit to cycle 适配周期
```js
s("breaks165").fit()
```

## Striate 条纹化
```js
s("breaks165").striate(8)
```

## Pitch-mapped samples 音高映射采样
```js
samples({ 'moog': { 'g3': 'moog/G3.wav', 'g4': 'moog/G4.wav' } }, 'base-url')
note("g3 bb3 c4").s("moog").clip(1)
```

## Shabda (freesound) 在线音效库
```js
samples('shabda:bass:4,hihat:4,rimshot:2')
```

## Custom sample with envelope 自定义采样 + 包络
```js
s("mydrum").attack(0.01).decay(0.1).sustain(0).release(0.1)
```
