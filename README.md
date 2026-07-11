# Prompt Craft — 提示词设计与优化 Skill

> 一个 Claude / Claude Code **skill**：把模糊的意图变成清晰、可复用、拿来就能用的 prompt。
>
> A Claude / Claude Code **skill** that turns vague intent into clear, reusable, ready-to-run prompts.

---

## 是什么 / What it is

**中文**

Prompt Craft 是一套经过实践验证的提示词方法论，核心是 **四要素框架**：

- **目标 Goal** — 要产出什么、给谁看
- **上下文 Context** — 只加会改变结果的信息
- **输出 Output** — 结构、长度、格式
- **边界 Boundaries** — 什么不能动、什么要先批准

一条好 prompt 不需要技术语法或固定套路，只在有帮助时才补充要素——不是每项都要填。

**English**

Prompt Craft is a battle-tested methodology for writing and optimizing prompts, built around a **four-element framework**: **Goal** (what to produce, for whom), **Context** (only what changes the result), **Output** (structure, length, format), and **Boundaries** (what must not change, what needs approval). A good prompt needs no special syntax—you add elements only when they help, not by rote.

---

## 适用场景 / When to use

| 类型 Type | 特征 Traits | 做法 Approach |
|-----------|-------------|---------------|
| 日常型 Everyday | 提问、找点子、草稿、比较 | 短 prompt，1–3 句 |
| 交付型 Deliverable | 多来源/多步骤、产出文件、给他人看 | 完整四要素 + 终检 |
| 代码型 Code | 修 bug、写测试、重构 | 行为 + 复现/定位 + 约束 + 验证方式 |
| Agent/系统型 Agent | 系统提示词、自动化、定时任务 | 四要素 + 审批边界 + 失败处理 |

触发方式：只要你请 Claude **"写一个 prompt"、"优化提示词"、"帮我改 prompt"、"review 这个 prompt"**，或把一个模糊需求变成可复用 prompt，这个 skill 就会介入。

Trigger it by asking Claude to *write*, *optimize*, *review*, or *restructure* a prompt (in any language).

---

## 安装 / Install

这是一个标准的 Claude Code skill，目录结构为 `skills/prompt-craft/SKILL.md`。

```bash
# 1. 克隆仓库 / Clone
git clone https://github.com/<your-name>/claude-prompt-craft-skill.git

# 2. 把 skill 放进 Claude 的 skills 目录 / Copy into your skills dir
#    Windows:  %USERPROFILE%\.claude\skills\
#    macOS/Linux: ~/.claude/skills/
cp -r claude-prompt-craft-skill/skills/prompt-craft ~/.claude/skills/
```

放好后，在 Claude / Claude Code 里正常对话即可自动触发（skill 靠描述里的关键词匹配）。

Once it's in your skills directory, Claude picks it up automatically based on the description keywords—no extra config needed.

---

## 怎么用 / Usage

直接用自然语言描述你的需求即可，例如：

```
帮我写一个交付型 prompt：为周一管理层会议准备一页纸项目状态通报。
```
```
优化这个提示词，让它输出更聚焦、别把每一步都写死。
```
```
Review this system prompt for my customer-support agent and tell me what's missing.
```

Skill 会先判断任务类型，最多问你一个最关键的问题，然后把最终 prompt 放进代码块方便复制，并附上 2–4 句"为什么这样组织 / 哪里可按需删改"的说明。

---

## 方法论概览 / Methodology at a glance

- **从结果说起，不从步骤说起** — 描述要产出什么、给谁看，给模型留出调整空间。
- **上下文只加会改变结果的** — 每个来源说清该取什么，别把文件整个丢过去。
- **边界防的是"真麻烦"** — 盯住 1–2 条最要紧的：改错就报废的细节、影响他人前该先过目的动作。
- **说清用途，模型才能选对形态** — 受众和用途决定长度、详细度、组织方式。
- **重要任务要终检** — 收尾前让模型自查一次（每个行动项有负责人和截止日期、标出无法核实的信息）。
- **第一版不必完美，靠追问收敛** — 审第一版 → 说出具体改动 → 不用从头再来。

完整方法论、场景模板与交付检查清单见 [`skills/prompt-craft/SKILL.md`](skills/prompt-craft/SKILL.md)。

Full templates and the delivery checklist live in [`skills/prompt-craft/SKILL.md`](skills/prompt-craft/SKILL.md).

---

## 目录结构 / Structure

```
claude-prompt-craft-skill/
├── README.md
├── LICENSE
└── skills/
    └── prompt-craft/
        └── SKILL.md      # 方法论本体 / the skill itself
```

---

## 致谢 / Credits

方法论来自实践验证的四要素框架（目标 / 上下文 / 输出 / 边界）。欢迎提 issue / PR 补充场景模板。

Methodology based on the field-tested four-element framework (Goal / Context / Output / Boundaries). Issues and PRs welcome.

## License

[MIT](LICENSE)
