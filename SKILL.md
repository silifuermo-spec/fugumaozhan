---
name: fugumaozhan
description: 基于五张内置动作版角色参考图，生成同一视觉家族、具有夸张且受力可信动作的复古手工毛毡定格动画人偶。适用于用户给出大致角色、职业或动作描述的单人全身角色图；禁止无参考图的纯文本生成。
---

# 夸张动作复古毛毡人偶

把用户的大致角色描述转化为一个主题全新、动作清楚、与内置样片同属一个角色家族的手工定格动画人偶。调用本 Skill 即表示必须使用五张参考图垫图；不得降级为纯提示词生成。

## 强制前置条件

1. 完整读取 [references/风格提示词.md](references/风格提示词.md)。其中“通用风格锁定”和“夸张动作锁定”必须逐字并入每次生成提示词。
2. 阅读 [references/参考图索引.md](references/参考图索引.md)，确认 `assets/references/01.png` 至 `05.png` 均存在且可读取。这五张图来自用户指定的“角色图片和提示词（动作版）”文件夹。
3. 加载并遵循 `$imagegen` Skill，使用内置 `image_gen` 工具。任务类型固定为 `stylized-concept` 的“带参考图生成”，不是编辑某一张原图。
4. 调用 `image_gen` 时，必须通过 `referenced_image_paths` 同时传入 `01.png`、`02.png`、`03.png`、`04.png`、`05.png` 的绝对路径。五张图是等权重的风格家族与动作语言参考，不是身份或姿势复制目标。
5. 禁止省略或减少参考图，禁止用 `num_last_images_to_include` 替代本地参考资产，禁止仅凭文字生成。若任一参考图或参考 Markdown 缺失、损坏或无法传入，停止生成并列出缺失项。

## 提炼新角色

从用户请求中确定年龄、性别表达、身份或职业、动作、表情、主色、服装和必要道具。若用户只给出“跳舞的女孩”这类简短描述，可补足有助于动作辨识和系列一致性的年龄、舞姿、服装层次与表情，但不得新增人物、场景、文字、品牌或无关道具。

若身份为职业、工种或社会角色，先建立“职业证据链”，再写造型：至少用 **专属工作道具、功能性服装细节、职业相关鞋履或足部装备** 中的两项共同说明身份；其中道具与鞋履不得只是泛用复古单品。根据动作和工作方式选择最合适的两到三项，不必机械塞满。职业本身合理携带包袋时，须明确它的工作用途、结构、材质和与动作的关系，例如邮差使用装有分格信件、可取信的帆布投递袋，而不是未说明用途的通用复古皮包。

新角色必须：

- 一眼读懂身份与动作；主轮廓和参考角色不同，不得把参考人物换色复刻。
- 职业角色的身份必须由至少两项可见职业证据共同支撑；鞋履应服务于该角色的工作环境、移动方式或安全需求，并在轮廓、闭合方式、材质、颜色或功能上与参考图的高辨识度鞋履明显不同。除非用户明确指定，不沿用参考图中相同的靴型、通用旧皮包、围巾组合或其近似配色。
- 具有夸张的停顿、折线、反向扭转、伸展或弹性，但至少一只脚可信承重；关节方向、重心、视线和持物逻辑合理。
- 保留圆润大头、略修长四肢、短小手塑手指、陶土五官和亲切而略笨拙的手工气质。
- 除非用户指定舞种，否则选择视觉上明确、适合单帧表达的复古律动舞姿；不要擅自写成特定舞种或复制参考图姿势。

## 组装提示词

使用以下结构。用户指定的信息优先；其余仅作必要补足。

```text
Use case: stylized-concept
Asset type: full-body stop-motion character concept
Primary request: <一个新原创角色及其夸张动作>
Input images: Images 1–5 are equal-weight style-family and movement-language references only. Match their shared handcrafted visual language, proportions, tactile material realism, dynamic silhouette, seamless studio setup, lighting, and finish. Do not copy any reference character's face, identity, occupation, clothing, prop, color scheme, or exact pose.
Subject: <年龄、性别表达、身份、外貌与约 1:3 大头身比例>
Occupation evidence: <若为职业角色，写出两至三项互相印证的职业证据：专属工作道具、功能性服装细节、职业相关鞋履/足部装备；说明每项的功能，且不复制参考图的高辨识度鞋包或服装组合>
Action/pose: <完整描述支撑脚、重心、躯干方向、四肢折角、手势、视线和必要道具；夸张但物理可信>
Expression: <与动作一致的具体表情>
Wardrobe/palette: <多层复古服装、材质、主色与禁用主色；明确鞋履的职业功能、鞋型、材质和颜色，并说明它与参考图鞋履的差异>
Style lock: <逐字并入“通用风格锁定”>
Movement lock: <逐字并入“夸张动作锁定”>
Composition: portrait 3:4; one character only; full body; crown, both hands, all fingers and both feet fully inside frame; reserve breathing room around extended limbs; mild eye-level camera.
Constraints: coherent anatomy and weight-bearing; clear negative space between limbs; essential props only and every prop must support the requested identity or action; no generic accessory substituted for a profession-specific tool; when the role needs a work bag, use a purpose-defined bag rather than an unspecified reference-like satchel; footwear must be newly designed for the role rather than copied from Images 1–5; no readable text, watermark, logo, extra character, extra limb, duplicated hand or foot, cropped body part, smooth plastic skin, glossy CGI, photorealistic human, motion blur, stage, dance floor, or environmental scene; create a new character, not a copy of Images 1–5.
```

动态动作允许斜向、侧向或下沉构图，但人物躯干应处在画面视觉中心附近，不能因动作幅度缩得过小，也不能裁掉头顶、手、脚或必要道具。

## 生成、保存与记录

- 将五张参考图作为 `referenced_image_paths` 一次性传给内置 `image_gen`。
- 生成后复制最终成图到当前项目的稳定路径，避免覆盖已有文件；同时以 Markdown 记录最终提示词。
- 若需要重试，五张参考图、两个锁定段落和已通过的不变量保持不变，只修正当前最大偏差。

## 视觉验收与迭代

生成后必须打开成图，并按 [references/验收标准.md](references/验收标准.md) 与五张参考图逐项对照。硬门槛任一失败，或总分低于阈值，不得宣布完成。

修正优先级：

1. 普通 3D 卡通感 → 拉回可触摸的陶土、毛毡、粗针织、灯芯绒和缝线。
2. 动作不够夸张或像普通站姿 → 强化轮廓、节奏断点、肩胯反向与肢体间负空间，同时保留可信承重。
3. 比例或裁切错误 → 恢复约 1:3 大头身、完整全身、双脚入画和竖幅 3:4。
4. 背景或光线漂移 → 恢复暖浅蓝无缝墙地、柔和漫射光与极淡落地阴影。
5. 最后修正角色语义、职业证据链、鞋履差异、服装主色、手指、道具和表情。职业不清晰时，优先替换泛用配饰为有功能的工作物件，或重设计鞋履；不要仅给参考样片的包袋或靴型换色。

## 交付要求

最终回复必须包含：成图绝对路径、实际使用的五张参考图绝对路径、最终提示词、内置 `image_gen` 模式说明，以及逐项验收结果。若生成被阻塞，只说明缺失项或工具失败；不得给出声称等价的纯文本出图方案。
