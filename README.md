# 复古毛毡人偶（fugumaozhan）

一个面向 ChatGPT 与 Codex 的图像生成 Skill。它使用仓库内置的 5 张角色样片作为等权重风格参考，生成同一视觉家族中主题、身份、动作和配色全新的手工定格动画人偶。

![参考角色样片](assets/references/06.png)

## 特点

- 固定使用 5 张本地参考图，不降级为无参考图的纯文本生成。
- 锁定陶土、羊毛毡、粗针织、灯芯绒、棉麻与旧皮革的手作质感。
- 约束为单个完整全身角色、3:4 竖幅、暖浅蓝无缝棚拍背景。
- 内置硬门槛与 16 分视觉验收规则；未达标时按最大偏差进行单点迭代。
- 支持新职业、新动作、新年龄、不同性别表达和新配色。

## 目录结构

```text
fugumaozhan/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── assets/
│   └── references/
│       ├── 06.png
│       ├── 07.png
│       ├── 08.png
│       ├── 09.png
│       └── 10.png
└── references/
    ├── 参考图索引.md
    ├── 风格提示词.md
    └── 验收标准.md
```

## 安装

可以在 Codex 中调用内置的 Skill Installer，并提供本仓库地址：

```text
$skill-installer 从 https://github.com/silifuermo-spec/fugumaozhan 安装 fugumaozhan Skill
```

也可以手动克隆到个人 Skill 目录：

```bash
git clone https://github.com/silifuermo-spec/fugumaozhan.git "$HOME/.agents/skills/fugumaozhan"
```

安装后，若 Skill 未立即出现在选择器中，请重启 Codex。

## 使用

在提示中显式调用 `$fugumaozhan`，并描述新角色需要具备的职业、动作、年龄、性别表达或配色。例如：

```text
$fugumaozhan 生成一位 26 岁的女性陶艺修复师，正小心托起一只修补后的陶杯，主色为低饱和靛青。
```

本 Skill 依赖内置的 `$imagegen` Skill 与 `image_gen` 工具。具体生成约束、提示词组装方式和验收规则请查看 [SKILL.md](SKILL.md)。

## 素材与许可

仓库当前未附开源许可证。除 GitHub 正常浏览本仓库所必需的权限外，提示词、文档与参考图片不因此被授予复制、再分发、修改或商业使用许可。公开使用前，请确保你对输出内容及参考素材拥有所需权利。
