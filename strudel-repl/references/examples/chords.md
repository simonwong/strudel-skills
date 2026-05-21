# Chords & Voicings 和弦与编排

展示 Strudel 的和弦系统：自动 voicing、lefthand/righthand 编排、shell voicings、Bossa Nova 等。

## Simple chord progression 简单和弦进行
```js
chord("<Am C F G>").voicing().room(.5)
```

## Jazz voicings with bass 爵士 voicing + 贝斯
```js
"<C^7 A7b13 Dm7 G7>*2".layer(
  x => x.voicings('lefthand').struct("[~ x]*2").note(),
  x => x.rootNotes(2).note().s('sawtooth').cutoff(800)
)
```

## Jazz blues in F F 调爵士蓝调
```js
let chords = chord(`<
F7 Bb7 F7 [Cm7 F7]
Bb7 Bo F7 [Am7 D7]
Gm7 C7 [F7 D7] [Gm7 C7]
>`)

$: n("7 8 [10 9] 8").set(chords).voicing().dec(.2)
$: chords.struct("- x - x").voicing().room(.5)
$: n("0 - 1 -").set(chords).mode("root:g2").voicing()
```

## Chord melody 和弦旋律
```js
chord("<C Am F G>").voicing().s("piano").room(.4)
  .struct("[~ x] [x ~] [~ x] [x ~]")
```

## Piano voicings 钢琴 voicing
```js
chord("<Dm7 G7 C^7>").voicings('lefthand').note()
  .s("piano").room(.5)
```

## Shell voicings
```js
chord("<Dm7 G7 C^7>").voicing({ mode: 'below', anchor: 'c4' }).note()
  .s("piano")
```

## Right hand voicings 右手 voicing
```js
chord("<Dm7 G7 C^7>").voicings('righthand').note()
  .s("piano").room(.3)
```

## Rootless voicings 无根音 voicing
```js
chord("<Am7 Dm7 G7 C^7>").voicings('lefthand').note()
  .s("gm_electric_piano:1").room(.5)
```

## Chord + bass unison 和弦 + 贝斯齐奏
```js
$: chord("<F^7 E7b9 Am7 Abm7 Db7 C^7>").voicing().s("piano").room(.5)
$: n("0 - - -").set(chord("<F^7 E7b9 Am7 Abm7 Db7 C^7>"))
  .mode("root:c2").voicing().s("sawtooth").lpf(600)
```

## Bossa nova chords Bossa Nova 和弦
```js
chord("<Dm7 G7 C^7 F^7>").struct("[x ~ x ~] [~ x ~ x]")
  .voicing().s("piano").room(.4)
```
