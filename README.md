# Claude Skills

Claude Code 的自定义 **Skill** 集合 — 7 个设计类知识包，含参考文档、脚本和提示词模板。

Skill 通过 `/skill-name` 在当前对话中加载，也可由 J.A.R.V.I.S. 根据需求自动加载。

---

## 目录

- [简介](#简介)
- [快速开始](#快速开始)
- [目录结构](#目录结构)
- [Skills 一览](#skills-一览)
  - [ui-ux-pro-max](#ui-ux-pro-max)
  - [ui-styling](#ui-styling)
  - [banner-design](#banner-design)
  - [brand](#brand)
  - [design](#design)
  - [design-system](#design-system)
  - [slides](#slides)
- [使用方式](#使用方式)
  - [方式一：命令行加载](#方式一命令行加载)
  - [方式二：J.A.R.V.I.S. 自动加载](#方式二jarvis-自动加载)
  - [方式三：Skill 工具加载](#方式三skill-工具加载)
- [为什么要用 Skill](#为什么要用-skill)
- [Skill vs Agent](#skill-vs-agent)
- [创建你自己的 Skill](#创建你自己的-skill)
- [最佳实践](#最佳实践)
- [许可证](#许可证)

---

## 简介

**Skill** 是 Claude Code 的一种知识包机制，用于将特定领域的专业知识、设计规范、参考文档和示例代码打包成一个可复用的单元。

与 Agent 不同：
- **Agent** = 独立执行任务的专家（子会话）
- **Skill** = 加载到当前对话的知识资源（当前会话）

Skill 的设计理念是"即插即用"——需要设计能力时加载，用完自动释放，不占用对话上下文。

---

## 快速开始

```bash
# 手动加载 — 直接敲 /skill-name
/ui-ux-pro-max 帮我设计一个现代登录页
/ui-styling 给这个按钮加上 Tailwind 样式
/banner-design 生成一张 Instagram 广告图
/slides 创建一个产品发布会演示文稿

# 或者让贾维斯自动加载
贾维斯，帮我设计一个品牌 Logo（会自动加载 design、brand）
贾维斯，做一份演示文稿（会自动加载 slides）
```

---

## 目录结构

```
~/.claude/skills/
├── banner-design/          # 👉 多平台 Banner 设计
│   ├── SKILL.md            #   Skill 入口
│   ├── references/         #   参考图片/模板
│   └── assets/             #   资源文件
├── brand/                  # 👉 品牌管理
│   ├── SKILL.md
│   └── references/
├── design/                 # 👉 Logo/CIP/图标生成
│   ├── SKILL.md
│   └── scripts/
├── design-system/          # 👉 设计 Token 与规范
│   ├── SKILL.md
│   └── references/
├── slides/                 # 👉 HTML 演示文稿
│   ├── SKILL.md
│   └── scripts/
├── ui-styling/             # 👉 UI 样式（shadcn/Tailwind）
│   ├── SKILL.md
│   └── references/
├── ui-ux-pro-max/          # 👉 UI/UX Pro Max 设计智能
│   ├── SKILL.md
│   └── references/
└── README.md               # 本文件
```

每个 Skill 目录包含：

| 文件/目录 | 用途 | 是否必需 |
|-----------|------|---------|
| `SKILL.md` | Skill 入口文件，定义角色、能力、输出规范 | ✅ |
| `scripts/` | 辅助脚本（如自动化生成工具） | ❌ |
| `references/` | 参考文档、色板、字体配对等知识库 | ❌ |
| `assets/` | 图片、模板等二进制资源 | ❌ |

---

## Skills 一览

### ui-ux-pro-max

> 全能 UI/UX 设计智能，50+ 风格、161 调色板、57 字体配对

| 项目 | 说明 |
|------|------|
| **加载方式** | `/ui-ux-pro-max` 或贾维斯自动 |
| **风格库** | glassmorphism, claymorphism, minimalism, brutalism, neumorphism, bento grid, skeuomorphism 等 50+ |
| **调色板** | 161 套预设色彩方案 |
| **字体配对** | 57 组经过验证的字体组合 |
| **UX 指南** | 99 条可用性设计原则 |
| **图表** | 25 种图表类型，支持 React/Next.js/Vue/Svelte/SwiftUI/Flutter |
| **技术栈** | React, Next.js, Vue, Svelte, SwiftUI, React Native, Flutter, Tailwind, shadcn/ui, HTML/CSS |
| **典型用法** | "设计一个 SaaS 仪表盘"、"评估这个页面 UI"、"优化登录页布局" |

### ui-styling

> shadcn/ui（Radix UI + Tailwind CSS）组件样式专家

| 项目 | 说明 |
|------|------|
| **加载方式** | `/ui-styling` 或贾维斯自动 |
| **组件库** | 对话框、下拉菜单、表单、表格、导航等 shadcn/ui 全部组件 |
| **核心能力** | Tailwind CSS 实用优先样式、响应式布局、暗色模式、无障碍组件 |
| **典型用法** | "帮我写一个响应式导航栏"、"给这个表单加样式" |

### banner-design

> 多平台广告 Banner 设计，22 种风格可选

| 平台 | 尺寸 |
|------|------|
| Facebook | 1200×628 |
| Twitter/X | 1200×675 |
| LinkedIn | 1200×627 |
| YouTube | 2560×1440 |
| Instagram | 1080×1080 / 1080×1350 |
| Google Display | 多种尺寸 |
| 网站 Hero | 自定义 |
| 印刷 | 自定义 |

| 风格 | 说明 |
|------|------|
| minimalism | 极简风格 |
| gradient | 渐变风格 |
| bold typography | 粗字体风格 |
| photo-based | 照片风格 |
| illustrated | 插画风格 |
| geometric | 几何风格 |
| retro | 复古风格 |
| glassmorphism | 毛玻璃风格 |
| 3D | 3D 风格 |
| neon | 霓虹风格 |
| duotone | 双色调风格 |
| collage | 拼贴风格 |
| 等 22 种 | |

**典型用法：** `/banner-design` 生成一个 Google Display 广告图

### brand

> 品牌识别系统管理

| 能力 | 说明 |
|------|------|
| **品牌声音** | 定义和管理品牌语调 |
| **视觉识别** | Logo、色板、排版规范 |
| **信息架构** | 品牌信息传递框架 |
| **资产管理** | 品牌素材管理指引 |
| **合规检查** | 品牌一致性审查 |

**典型用法：** `/brand` 帮我设计一个科技品牌的声音和色板

### design

> 综合设计 — Logo 生成、CIP、图标

| 能力 | 覆盖 |
|------|------|
| **Logo 生成** | 55 种风格，支持 Gemini AI |
| **CIP** | 50 项企业识别交付物 |
| **图标设计** | 15 种风格，SVG 格式，Gemini 3.1 Pro |
| **HTML 演示** | Chart.js 图表集成 |
| **社交图片** | HTML→截图，多平台输出 |

**典型用法：** `/design` 帮我生成一个科技公司的 Logo（几个选项供选择后生成完整 CIP）

### design-system

> 设计 Token 架构与组件规范

| 能力 | 说明 |
|------|------|
| **Token 架构** | 三层 Token：primitive → semantic → component |
| **CSS 变量** | 生成可直接使用的 CSS 自定义属性 |
| **间距/排版** | 比例尺度和字体层级系统 |
| **组件规格** | 组件的 Token 映射和使用规范 |
| **幻灯片** | 品牌合规的演示文稿生成 |

**典型用法：** `/design-system` 帮我建立一套设计 Token

### slides

> 交互式 HTML 演示文稿，支持 Chart.js

| 能力 | 说明 |
|------|------|
| **图表** | Chart.js 多类型图表 |
| **设计 Token** | 内建设计系统令牌 |
| **响应式** | 自动适配各种屏幕 |
| **文案框架** | 内置文案公式 |
| **上下文策略** | 每页的展示策略 |

**典型用法：** `/slides` 创建一个产品路线图演示

---

## 使用方式

### 方式一：命令行加载

直接在 Claude Code 中敲：

```bash
# 加载 Skill（必须在对话开始时或需要时手动敲）
/ui-ux-pro-max

# 加载并附带任务
/ui-ux-pro-max 帮我设计一个暗色主题的仪表盘

# 切换不同 Skill
/slides 帮我做一下季度汇报
/banner-design 生成一个 LinkedIn 封面图
```

加载成功后，Skill 的知识会在当前对话中生效，你可以继续对话。

### 方式二：J.A.R.V.I.S. 自动加载

提到贾维斯并描述设计类需求时，会自动加载对应的 Skill：

```bash
# 设计 UI
贾维斯，帮我设计一个现代化的登录页面
→ 自动加载 ui-ux-pro-max

# 做品牌
贾维斯，设计一个品牌 Logo
→ 自动加载 design + brand

# 做演示
贾维斯，帮我做一个产品发布会 PPT
→ 自动加载 slides

# UI 样式
贾维斯，帮我的 button 组件加样式
→ 自动加载 ui-styling

# Banner 广告
贾维斯，帮我做一张小红书封面图
→ 自动加载 banner-design
```

### 方式三：Skill 工具加载

在 Claude Code 对话中，无论主会话还是 Agent 子会话，只要配置了 `tools: [Skill]`，都可以直接调用：

```javascript
Skill({skill: "ui-ux-pro-max", args: "设计一个登录页"})
Skill({skill: "slides", args: "季度汇报演示"})
```

这是 J.A.R.V.I.S. 和高级 Agent 内部使用的加载方式。

---

## 为什么要用 Skill

### Skill 解决的核心问题

在实际 AI 辅助设计中，你会发现直接让 AI 做设计往往不够好：

```
❌ 直接说"给我设计一个 Banner" → 颜色、字体、布局都靠猜
✅ 先加载 Banner 设计 Skill → 有 22 种风格、平台尺寸规范、设计原则
```

Skill 提供了：

1. **上下文知识** — 不是让 AI 凭空想象，而是有一套完整的规则和参考
2. **风格一致性** — 同一 Skill 出来的设计风格统一
3. **输出规范** — 知道具体格式、尺寸、配色标准
4. **效率提升** — 不需要每次重新解释需求

### 什么时候需要 Skill

| 场景 | 用 Agent 还是 Skill？ |
|------|----------------------|
| 修复 bug、写代码 | Agent（直接执行） |
| 设计 UI 界面 | Skill（加载设计规范） |
| 生成 Logo | Skill（加载设计模板） |
| 做市场竞品分析 | Agent（搜索分析） |
| 做 PPT 演示 | Skill（加载图表模板） |
| 渗透测试 | Agent（专业操作） |
| 设计品牌系统 | Skill + Agent 配合 |
| 写文档 | Agent + Skill 配合 |

---

## Skill vs Agent

| 维度 | Skill | Agent |
|------|-------|-------|
| **本质** | 知识包（Knowledge Package） | 专家角色（Expert Role） |
| **文件形式** | 目录（含 SKILL.md + 参考资源） | 单个 `.md` 文件 |
| **加载方式** | `/skill-name`、`Skill()` 工具、J.A.R.V.I.S 自动 | 关键词路由、直接对话、J.A.R.V.I.S 路由 |
| **执行模型** | 加载到当前对话上下文 | 启动独立子会话 |
| **适用场景** | 设计、创作、知识密集型任务 | 开发、分析、搜索、执行类任务 |
| **状态** | 加载即生效，卸载消失 | 独立执行，返回结果 |
| **资源** | 可包含脚本、图片、参考文档 | 只有系统提示词 |
| **何时使用** | 需要专业知识储备时 | 需要独立执行任务时 |

### 可以一起用吗？

**可以！** 最佳效果往往是两者配合：

1. J.A.R.V.I.S. 分析任务 → 需要设计能力
2. 加载 Skill（如 ui-ux-pro-max） → 当前对话获得设计知识
3. 调用 Agent（如 Frontend Developer） → 执行具体的编码工作
4. Skill 提供设计规范，Agent 负责技术实现

---

## 创建你自己的 Skill

在 `~/.claude/skills/` 下新建一个目录并编写 `SKILL.md`：

```markdown
---
name: my-skill
description: 我的自定义 Skill
---

# My Skill

## Your Role

You are a [specific role] with expertise in [area].

## Capabilities

- Capability 1: detailed description
- Capability 2: detailed description

## Knowledge Base

### Topic 1
- Key point 1
- Key point 2
- Reference: [[link or note]]

### Topic 2
- ...

## Output Standards

When generating output, follow these conventions:
- Format: [expected format]
- Style: [expected style]
- Quality checks: [what to verify]

## Examples

### Example 1: [Scenario]
[Example input/output]
```

**可选资源目录：**

```bash
$ mkdir -p ~/.claude/skills/my-skill/{scripts,references,assets}
$ touch ~/.claude/skills/my-skill/SKILL.md
```

然后更新 `jarvis.md` 的路由表，添加新 Skill 的自动加载规则。

---

## 最佳实践

### 使用习惯

- **设计类任务先加载 Skill** — 效果远好于直接描述
- **Banner 设计指定平台** — 明确说是 Facebook、Instagram 还是其他
- **贾维斯帮你判断** — 不确定加载哪个 Skill 时，让贾维斯自动处理
- **复杂项目先用 Skill 后调 Agent** — Skill 提供知识，Agent 负责执行

### Skill 设计原则

- **SKILL.md 是第一入口** — 让 AI 在加载后先明白自己的角色和任务
- **提供具体示例** — 示例比抽象描述效果好得多
- **参考文件要精简** — 太多参考会占用对话上下文
- **保持独立** — 每个 Skill 聚焦一个领域，不要做大而全

### 已知 Skill 加载路由

当前 J.A.R.V.I.S. 配置的自动加载映射：

| 用户提及关键词 | 自动加载 Skill |
|---------------|---------------|
| UI/UX 设计、界面、风格、美观 | `ui-ux-pro-max` |
| UI 样式、组件、Tailwind | `ui-styling` |
| Banner、广告图、封面 | `banner-design` |
| 品牌、色板、品牌识别 | `brand` |
| Logo、图标、CIP、企业识别 | `design` |
| 设计系统、Token、规范 | `design-system` |
| 幻灯片、PPT、演示 | `slides` |

---

## 许可证

MIT

---

**相关资源：**
- [Agents 仓库](https://github.com/mjzappzz/claude-agents) — 100+ 领域专家 Agent
- [Claude Code 官方文档](https://docs.anthropic.com/en/docs/claude-code)
- [Anthropic 官方](https://anthropic.com)
