# Euclidean Rhythms 欧几里得节奏

欧几里得节奏 `(beats,segments,offset)` 将指定数量的打击均匀分布在指定数量的步进中，产生世界各地的传统节奏型。

## Cuban tresillo 古巴 tresillo
```js
sound("bd(3,8)")
```

## Multiple euclidean layers 多层欧几里得
```js
sound("bd(3,8), hh(5,8), sd(2,8)")
```

## With rotation 带旋转偏移
```js
sound("bd(3,8,0), hh(5,8,2)")
```

## Afro-Cuban bell pattern 非洲-古巴铃铛
```js
sound("cb(5,8)")
```

## Samba percussion 桑巴打击乐
```js
sound("bd(3,16), sd(2,16,4), hh(5,16)")
```

## West African timeline 西非时间线
```js
sound("bell(3,4,1)")
```

## Aksak rhythm 不规则节奏
```js
sound("bd(5,8)")
```

## Cuban clave 古巴 clave
```js
sound("clave(3,8,2)")
```

## Layered euclidean with different rotations 多层旋转欧几里得
```js
sound("bd(5,16,0), sd(5,16,4), hh(5,16,8), cp(5,16,12)")
```

## Euclidean with melody 欧几里得 + 旋律
```js
n(irand(12)).scale("C4:minor:pentatonic").sound("gm_kalimba")
  .degradeBy(0.3).room(.6).gain(.3)
$: sound("bd(3,8)").bank("RolandTR707").gain(.4)
$: n("0 ~ 4 ~").scale("C2:minor").sound("gm_acoustic_bass").lpf(400)
```
