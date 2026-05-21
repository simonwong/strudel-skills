# MIDI Output MIDI 输出

将 Strudel 的 pattern 发送到外部 MIDI 设备或 DAW。

## Basic MIDI 基础 MIDI
```js
note("c a f e").midi('IAC Driver')
```

## MIDI with options MIDI 选项
```js
note("c a f e").midi('IAC Driver', {
  midichannel: 1,
  velocity: 0.9
})
```

## MIDI channel selection MIDI 通道选择
```js
note("c a f e").midi('IAC Driver').midichan(2)
```

## MIDI control change MIDI 控制变更
```js
note("c a f e").midi('IAC Driver').ccn(74).ccv(0.5)
```

## MIDI program change MIDI 音色变更
```js
note("c a f e").midi('IAC Driver').progNum(40)
```

## MIDI pitch bend MIDI 弯音
```js
note("c3").midi('IAC Driver').midibend(sine.range(-0.1, 0.1))
```

## MIDI with chords MIDI 和弦
```js
chord("<C^7 Dm7 G7>").voicing().midi('IAC Driver')
```
