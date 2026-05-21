# Strudel Examples Index 示例索引

按需加载指引：根据用户意图只加载相关模块，避免一次性加载所有内容。

## By Technique 按技术类别

| 文件 | 内容 | 何时加载 |
|------|------|---------|
| [drums.md](drums.md) | 鼓 pattern：基础节拍到 breakbeat | 用户要打鼓、做 beat |
| [euclidean.md](euclidean.md) | 欧几里得节奏：tresillo、clave 等 | 用户提到 euclidean、世界节奏 |
| [melodies.md](melodies.md) | 旋律与贝斯线 | 用户要写旋律、贝斯 |
| [chords.md](chords.md) | 和弦与 voicing 编排 | 用户要和弦、voicing |
| [effects.md](effects.md) | 音效：滤波器、延迟、混响、失真 | 用户要加效果 |
| [transforms.md](transforms.md) | Pattern 变换：off、echo、iter 等 | 用户要变换 pattern |
| [modulation.md](modulation.md) | 连续调制：LFO、柏林噪声 | 用户要 LFO、动态调制 |
| [synths.md](synths.md) | 合成器：FM、波表、加法合成 | 用户要合成器音色 |
| [samples.md](samples.md) | 采样：加载、切片、颗粒化 | 用户要加载采样、切片 |
| [midi.md](midi.md) | MIDI 输出 | 用户要连 MIDI 设备 |
| [parallel.md](parallel.md) | 并行 Pattern ($:) | 用户要多层编排 |
| [visualization.md](visualization.md) | 可视化：scope、punchcard | 用户要可视化 |
| [workflow.md](workflow.md) | 工作流：调试、速度、编排 | 用户要调试、设定速度 |

## By Music Genre 按音乐类型

| 文件 | 内容 | 何时加载 |
|------|------|---------|
| [genre/folk.md](genre/folk.md) | 民谣 / Folk：木吉他、五声音阶 | 用户说"民谣"、"folk" |
| [genre/soul-rnb.md](genre/soul-rnb.md) | Soul / R&B：Rhodes、福音和声 | 用户说"soul"、"R&B"、"灵魂乐" |
| [genre/jazz-blues.md](genre/jazz-blues.md) | Jazz / Blues：voicing、walking bass | 用户说"爵士"、"jazz"、"blues" |
| [genre/electronic.md](genre/electronic.md) | 电子：Techno/House/Dub/Ambient | 用户说"电子"、"techno"、"house" |
| [genre/rock.md](genre/rock.md) | 摇滚：power chord、失真吉他 | 用户说"摇滚"、"rock" |
| [genre/hiphop-lofi.md](genre/hiphop-lofi.md) | Hip-Hop / Lo-Fi：采样拼接 | 用户说"hip-hop"、"lo-fi"、"说唱" |
| [genre/world.md](genre/world.md) | 世界音乐：非洲/拉丁/亚洲 | 用户说"世界音乐"、"非洲鼓"、"拉丁" |
| [genre/classical.md](genre/classical.md) | 古典 / 当代作曲：算法、对位 | 用户说"古典"、"作曲"、"算法" |
| [genre/gamemusic.md](genre/gamemusic.md) | 游戏音乐：chiptune、8-bit | 用户说"游戏音乐"、"chiptune" |
| [genre/experimental.md](genre/experimental.md) | 实验 / 前卫：噪音、glitch | 用户说"实验"、"噪音"、"glitch" |

## Full Compositions 完整作品

| 文件 | 内容 | 何时加载 |
|------|------|---------|
| [compositions.md](compositions.md) | 多层完整作品（官方 + 社区） | 用户要完整示例、灵感参考 |

## Loading Strategy 加载策略

1. **用户问特定技术** → 加载对应技术文件
2. **用户说音乐类型** → 加载对应 genre 文件
3. **用户要灵感/参考** → 加载 compositions.md
4. **用户问题宽泛** → 先加载最相关的 1-2 个文件，不要一次全部加载
5. **用户要完整教程** → 按 drums → melodies → chords → effects 顺序逐步加载
