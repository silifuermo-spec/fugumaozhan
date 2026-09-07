---
name: fugumaozhan
description: 基于内置角色参考图与固定中文风格提示词，生成同一视觉体系的全新手工定格动画人偶角色。适用于新职业、新动作、新年龄或新配色角色；不得用于无参考图的纯文本出图。
---

# 复古毛毡人偶

生成与内置样片属于同一“角色家族”、但主题和动作全新的手工定格动画人偶。调用本 Skill 即表示用户要求用参考图垫图；不得降级为纯提示词生成。

## 强制前置条件

1. 完整读取 [references/风格提示词.md](references/风格提示词.md)。其中“通用风格锁定”是每次提示词的不可删减基线；角色段落用于理解人物比例、职业动作、表情和穿搭的写法。
2. 阅读 [references/参考图索引.md](references/参考图索引.md)，并确认 `assets/references/06.png` 至 `10.png` 均存在且可读取。
3. 加载并遵循 `$imagegen` Skill，使用内置 `image_gen` 工具。当前任务是 `stylized-concept` 类型的“带参考图生成”，不是编辑任何一张原图。
4. 在调用 `image_gen` 时，必须通过 `referenced_image_paths` 传入 `assets/references/06.png`、`07.png`、`08.png`、`09.png`、`10.png` 的绝对路径；五张图的角色身份仅作风格家族参考，不得复制为新角色。
5. 禁止省略 `referenced_image_paths`，禁止用 `num_last_images_to_include` 代替本地参考资产，禁止仅凭文字生成。若风格 Markdown 或任一参考图缺失、损坏或无法传入，停止生成并明确说明缺失项。

## 生成流程

### 1. 提炼新角色

从用户请求中确定：年龄、性别表达、身份或职业、动作、表情、主色、服装与必要道具。用户只给出简短主题时，可补充支持该主题的姿态和服装细节，但不要新增人物、场景、文字、品牌或无关道具。

新角色必须满足：

- 身份与动作能一眼读懂；动作符合真实受力、持物和视线逻辑。
- 与五个样片的职业、配色和道具明显不同，避免把参考人物改色后复刻。
- 保留同系列的圆润大头、略修长四肢、陶土五官和亲切而略笨拙的手作气质。

### 2. 组装生成提示词

使用下面的短标签结构。将风格 Markdown 中“通用风格锁定”完整并入 `Style lock`；不要用同义改写削弱材质、背景、画幅和负面约束。

```text
Use case: stylized-concept
Asset type: full-body stop-motion character concept
Primary request: <用户要求的新角色与动作>
Input images: Images 1–5 are equal-weight style-family references only. Match their shared handcrafted visual language, proportions, material realism, studio setup, lighting, and finish. Do not copy any reference character's identity, occupation, clothing, prop, or pose.
Subject: <年龄、性别表达、身份、外貌>
Action/pose: <全身动作、重心、四肢、持物、视线>
Expression: <与动作一致的具体表情>
Wardrobe/palette: <服装层次、材质、主色和禁用主色>
Style lock: <逐字并入“通用风格锁定”>
Constraints: one character only; full body and both feet visible; coherent hands and limbs; only essential prop(s); no readable text, watermark, or logo; create a new character, not a copy of Images 1–5.
```

对动态动作，仍保持竖幅 3:4 与完整全身，但允许身体斜向构图；不得为了动作裁掉头顶、脚、球或必要道具。

### 3. 调用 ImageGen

- 先把五张本地参考图全部传给 `image_gen`，再提交组装后的提示词。
- 参考图角色均为“风格参考”，不是“编辑目标”或“身份参考”。
- 不要求模型输出拼图、角色设定表、文字说明或前后视图，除非用户明确提出。
- 项目交付图复制到当前工作区的稳定路径，避免覆盖已有文件；同时记录最终提示词。

### 4. 视觉验收与迭代

生成后必须打开成图，并按 [references/验收标准.md](references/验收标准.md) 与五张参考图对照。任一硬门槛不通过时，不得宣布完成；保持五张参考图不变，只针对最大偏差做一次单点修正并再次生成。每轮都重复风格锁定和全部不变量。

常见修正顺序：

1. 先修正媒介与材质：从“普通 3D 卡通”拉回可触摸的陶土、毛毡、粗针织和缝线。
2. 再修正比例与构图：大头约 1:3、完整全身、双脚入画、竖幅 3:4。
3. 再修正背景与光：无缝暖浅蓝、柔和漫射光、极淡脚下投影。
4. 最后修正角色语义、动作、服装主色、手指和道具。

## 交付说明

最终回复必须包含：成图绝对路径、实际使用的五张参考图、最终提示词、使用的是内置 `image_gen` 模式，以及验收结果。若未生成图片，只能说明阻塞原因，不得提供一个声称等价的纯文本生成方案。
