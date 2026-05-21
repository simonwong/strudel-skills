# Continuous Modulation 连续调制

使用 LFO（低频振荡器）和随机信号对参数进行连续调制，创造动态变化的音色。

## LFO on filter 滤波器 LFO
```js
s("hh*16").lpf(sine.range(200, 4000).slow(4))
```

## Perlin noise on cutoff 柏林噪声调制截止频率
```js
s("bd*4,hh*8").cutoff(perlin.range(500, 8000))
```

## Random pan 随机声像
```js
s("hh*10").pan(brand)
```

## Sine wave modulation 正弦波调制
```js
note("c3").sound("sawtooth").lpf(sine.range(200, 4000).slow(2))
```

## Triangle LFO on gain 三角波增益调制
```js
s("hh*16").gain(tri.range(0.2, 1).slow(2))
```

## Perlin on speed 柏林噪声速度调制
```js
s("hh*8").speed(perlin.range(0.8, 1.2))
```

## Random cutoff 随机截止频率
```js
s("bd*4").lpf(rand.range(200, 4000))
```

## Saw LFO on pan 锯齿波声像调制
```js
s("hh*8").pan(saw.range(0, 1).slow(2))
```

## Multi-parameter modulation 多参数调制
```js
note("c3").sound("sawtooth")
  .lpf(sine.range(200, 4000).slow(4))
  .pan(cosine.range(0, 1).slow(3))
  .gain(tri.range(0.3, 0.8).slow(2))
```

## Segment for continuous control 连续控制分段
```js
s("supersaw").seg(16).lpf(sine.range(100, 5000).slow(2))
```

## Perlin on resonance 柏林噪声共振调制
```js
note("c3").sound("sawtooth").lpf(1000).lpq(perlin.range(0, 20))
```

## Square wave modulation 方波调制
```js
s("bd*4").gain(square.range(0.3, 1).slow(1))
```
