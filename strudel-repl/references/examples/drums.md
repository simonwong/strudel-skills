# Drum Patterns 鼓 Pattern

从最简单的四拍到复杂的 breakbeat，覆盖常见的鼓 pattern 类型。

## Simple beat 基础节拍
```js
sound("bd hh sd hh")
```

## Rock beat 摇滚节拍
```js
setcpm(100/4)
sound("[bd sd]*2, hh*8").bank("RolandTR505")
```

## Classic house 经典 House
```js
sound("bd*4, [- cp]*2, [- hh]*4").bank("RolandTR909")
```

## We Will Rock You
```js
setcpm(81/2)
sound("bd*2 cp").bank("RolandTR707")
```

## TR-808 pattern
```js
setcpm(88/4)
sound(`
[-  -  -  - ] [-  -  -  - ] [-  -  -  - ] [-  -  oh:1 - ],
[hh hh hh hh] [hh hh hh hh] [hh hh hh hh] [hh hh -  - ],
[-  -  -  - ] [cp -  -  - ] [-  -  -  - ] [~  cp -  - ],
[bd bd -  - ] [-  -  bd - ] [bd bd - bd ] [-  -  -  - ]
`).bank("RolandTR808")
```

## 16-step sequencer style 16 步音序器
```js
setcpm(90/4)
sound(`
[-  -  oh - ] [-  -  -  - ] [-  -  -  - ] [-  -  -  - ],
[hh hh -  - ] [hh -  hh - ] [hh -  hh - ] [hh -  hh - ],
[-  -  -  - ] [cp -  -  - ] [-  -  -  - ] [cp -  -  - ],
[bd -  -  - ] [-  -  -  bd] [-  -  bd - ] [-  -  -  bd]
`)
```

## Non-standard percussion 非常规打击乐
```js
setcpm(100/2)
s(`jazz*2,
insect [crow metal] - -,
- space:4 - space:1,
- wind`)
```

## Syncopated funk beat 切分 Funk
```js
setcpm(110/4)
sound("bd [~ bd] [~ bd] bd, ~ ~ ~ cp, hh*16").bank("RolandTR909")
```

## Reggae one-drop 雷鬼 one-drop
```js
setcpm(80/4)
sound("bd ~ ~ ~, ~ ~ cp ~, hh ~ hh ~").bank("RolandTR707")
```

## Breakbeat 碎拍
```js
setcpm(130/4)
sound("bd*2 [~ sd] bd [~ sd], hh*8").bank("RolandTR909")
```

## Multi-layer beat 多层鼓组

See `parallel.md` for multi-layer and drum+bass+chords examples.
