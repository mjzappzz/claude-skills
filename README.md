# Claude Skills

Claude Code 的自定义 **Skill** 集合 — 26 个工程技能知识包，覆盖代码审查、调试、CI/CD、安全、性能优化等开发全流程。

每个 Skill 是一个独立目录，内含 `SKILL.md` 定义文件，通过 `/skill-name` 在当前对话中加载，也可由 J.A.R.V.I.S. 根据需求自动加载。

---

## 目录

- [简介](#简介)
- [快速开始](#快速开始)
- [目录结构](#目录结构)
- [Skills 一览](#skills-一览)
  - [工程基础](#工程基础)
  - [开发流程](#开发流程)
  - [质量与测试](#质量与测试)
  - [安全与运维](#安全与运维)
  - [设计与架构](#设计与架构)
  - [辅助工具](#辅助工具)
- [使用方式](#使用方式)
- [Skill 详解](#skill-详解)
- [技能组合推荐](#技能组合推荐)
- [创建你自己的 Skill](#创建你自己的-skill)
- [最佳实践](#最佳实践)
- [维护指南](#维护指南)
- [许可证](#许可证)

---

## 简介

**Skill** 是 Claude Code 的一种知识包机制，用于将特定领域的专业知识、检查清单、最佳实践和参考文档打包成一个可复用的单元。

与 Agent 不同：

- **Agent** = 独立执行任务的专家（子会话）
- **Skill** = 加载到当前对话的知识资源（当前会话）

Skill 的设计理念是"即插即用"——需要某个领域知识时加载，用完自动释放，不占用对话上下文。本仓库的 Skill 聚焦工程领域，是日常开发最常用的技能合集。

---

## 快速开始

```bash
# 手动加载 — 直接敲 /skill-name
/code-review-and-quality 帮我审查这段代码
/debugging-and-error-recovery 测试失败了，帮我调试
/security-and-hardening 检查这个接口的安全漏洞

# 或者让贾维斯自动加载
贾维斯，帮我审查一下这段代码（自动加载 code-review-and-quality）
贾维斯，我的构建失败了（自动加载 debugging-and-error-recovery）

# 查看所有可用技能
ls ~/.claude/skills/*/SKILL.md
```

---

## 目录结构

```
~/.claude/skills/
├── api-and-interface-design/      # 👉 API 与接口设计
├── browser-testing-with-devtools/ # 👉 浏览器测试
├── ci-cd-and-automation/          # 👉 CI/CD 自动化
├── code-review-and-quality/       # 👉 代码审查
├── code-simplification/           # 👉 代码简化
├── context-engineering/           # 👉 上下文工程
├── debugging-and-error-recovery/  # 👉 调试与错误恢复
├── deprecation-and-migration/     # 👉 废弃与迁移
├── documentation-and-adrs/        # 👉 文档与架构决策
├── doubt-driven-development/      # 👉 质疑驱动开发
├── frontend-ui-engineering/       # 👉 前端 UI 工程
├── git-workflow-and-versioning/   # 👉 Git 工作流
├── idea-refine/                   # 👉 创意提炼
├── incremental-implementation/    # 👉 增量实现
├── interview-me/                  # 👉 需求澄清
├── observability-and-instrumentation/ # 👉 可观测性
├── performance-optimization/      # 👉 性能优化
├── planning-and-task-breakdown/   # 👉 任务拆解
├── security-and-hardening/        # 👉 安全加固
├── shipping-and-launch/           # 👉 发布上线
├── source-driven-development/     # 👉 源码驱动开发
├── spec-driven-development/       # 👉 规范驱动开发
├── stress-report/                 # 👉 压力测试报告
├── test-driven-development/       # 👉 测试驱动开发
├── ui-ux-pro-max/                 # 👉 UI/UX 设计
├── using-agent-skills/            # 👉 技能路由指南
└── README.md                      # 本文件
```

每个 Skill 目录结构：

| 文件/目录 | 用途 | 必需 |
|-----------|------|------|
| `SKILL.md` | Skill 入口文件 — 角色定义、知识库、输出规范 | ✅ |
| `scripts/` | 辅助脚本（如自动化工具、模板生成） | ❌ |
| `references/` | 参考文档、示例代码 | ❌ |
| `assets/` | 静态资源、模板文件 | ❌ |

---

## Skills 一览

### 工程基础

| Skill | 用途 | 使用场景 |
|-------|------|---------|
| `code-review-and-quality` | 多维代码审查 — 正确性、可读性、架构、安全、性能 | 合入前审查任何代码变更 |
| `code-simplification` | 代码简化 — 降低复杂度、提升可维护性 | 代码过长、嵌套过深、重复逻辑 |
| `debugging-and-error-recovery` | 系统化调试 — Stop-the-Line 三阶段流程 | 测试失败、构建错误、运行时异常 |
| `performance-optimization` | 性能优化 — Profile → 定位 → 修复闭环 | 响应慢、CPU高、内存泄漏 |

### 开发流程

| Skill | 用途 | 使用场景 |
|-------|------|---------|
| `git-workflow-and-versioning` | Git 工作流与版本管理 | 分支策略、提交规范、版本发布 |
| `incremental-implementation` | 增量实现 — 小步快跑 | 多项变更按小步骤分次交付 |
| `planning-and-task-breakdown` | 任务拆解 — 将需求转化为有序任务 | 需求清晰后的执行规划 |
| `spec-driven-development` | 规范驱动开发 — 先写规范再实现 | 重要功能或 API 开发前 |
| `source-driven-development` | 源码驱动 — 基于官方来源做决策 | 使用新框架/库时的最佳实践 |
| `test-driven-development` | 测试驱动开发 — 测试先行 | 任何需要验证的行为变更 |
| `deprecation-and-migration` | 废弃与迁移计划 | 移除旧代码、升级依赖、数据迁移 |

### 质量与测试

| Skill | 用途 | 使用场景 |
|-------|------|---------|
| `ci-cd-and-automation` | CI/CD 质量门禁与自动化 | 设置流水线、自动化检查 |
| `browser-testing-with-devtools` | 浏览器行为验证 | 使用 Chrome DevTools 调试前端 |
| `stress-report` | 压力测试报告生成 | 服务器性能瓶颈分析 |
| `doubt-driven-development` | 质疑驱动 — 对抗性审查 | 对非平凡决策进行压力测试 |

### 安全与运维

| Skill | 用途 | 使用场景 |
|-------|------|---------|
| `security-and-hardening` | 安全加固 — 输入、认证、数据保护 | 涉及用户输入、认证、数据集成 |
| `observability-and-instrumentation` | 可观测性 — 日志、指标、链路、告警 | 添加监控、排查线上问题 |
| `shipping-and-launch` | 发布上线 — 部署、监控、回滚计划 | 准备生产发布 |

### 设计与架构

| Skill | 用途 | 使用场景 |
|-------|------|---------|
| `api-and-interface-design` | API 与接口设计 — 稳定、清晰的接口契约 | 定义模块边界、API 设计 |
| `frontend-ui-engineering` | 前端 UI 工程 — 高质量用户界面 | 构建或审查前端界面 |
| `ui-ux-pro-max` | UI/UX 设计指导 — 多技术栈 | 需要设计规范和最佳实践 |
| `documentation-and-adrs` | 文档与架构决策记录 | 记录架构决策、编写文档 |

### 辅助工具

| Skill | 用途 | 使用场景 |
|-------|------|---------|
| `context-engineering` | 上下文工程 — 管理项目上下文和 Agent 指令 | 优化 Agent 工作效果 |
| `interview-me` | 需求澄清 — 通过提问明确模糊需求 | 需求不清晰时 |
| `idea-refine` | 创意提炼 — 将模糊想法转化为可执行概念 | 从零开始构思功能 |
| `using-agent-skills` | 技能路由指南 — 发现和路由工作到合适的 Skill | 不确定该用哪个技能时 |

---

## 使用方式

### 在 Claude Code 中

直接在 Claude Code 对话中敲 `/skill-name` 加载对应技能：

```bash
# 加载 Skill（必须在对话开始时或需要时手动敲）
/code-review-and-quality

# 加载并附带任务
/debugging-and-error-recovery 我的 CI 构建失败了，帮我排查一下

# 切换不同 Skill
/security-and-hardening 检查这个 API 的安全漏洞
/performance-optimization 分析这个函数的性能
```

### 通过 J.A.R.V.I.S. 自动加载

提到贾维斯并描述工程需求时，会自动加载对应的 Skill：

```bash
# 代码审查
贾维斯，帮我审查这段代码
→ 自动加载 code-review-and-quality

# 调试
贾维斯，测试失败了
→ 自动加载 debugging-and-error-recovery

# 安全
贾维斯，检查这个接口的安全
→ 自动加载 security-and-hardening

# 性能
贾维斯，分析一下这个页面的性能
→ 自动加载 performance-optimization
```

### 通过 Skill 工具加载

在 Agent 子会话中通过 `Skill()` 工具调用：

```javascript
Skill({skill: "code-review-and-quality", args: "审查这个 PR 的变更"})
Skill({skill: "debugging-and-error-recovery", args: "调试 CI 构建失败"})
```

---

## Skill 详解

### code-review-and-quality

> 五轴代码审查 — 合入前的质量门禁

审查标准：

| 维度 | 检查项 |
|------|--------|
| **正确性** | 是否符合需求、边界条件、错误处理 |
| **可读性** | 命名、注释、代码结构是否清晰 |
| **架构** | 设计模式、模块边界、依赖是否合理 |
| **安全** | 输入验证、注入防护、敏感数据处理 |
| **性能** | 不必要的分配、循环效率、缓存机会 |

**原则：** 只要变更确实改进了整体代码健康度就批准，不需要代码完美。

### debugging-and-error-recovery

> Stop-the-Line 系统化调试流程

```
1. STOP — 停止添加功能或修改
2. PRESERVE — 保留证据（错误输出、日志、复现步骤）
3. DIAGNOSE — 用结构化的排查清单诊断
4. FIX — 修复根因
5. GUARD — 防止复发
```

**排查清单：**
- 最近改了什么？
- 假设是什么？（列出所有）
- 能稳定复现吗？
- 错误出现的时间和频率？
- 最小复现条件是什么？

### code-simplification

> 代码简化 — 降低复杂度、提升可维护性

评估标准：
- **圈复杂度** — 单个方法不要超过 10 条路径
- **认知负荷** — 阅读代码需要跟踪多少状态
- **嵌套深度** — 不要超过 3 层

**核心原则：** 先确保正确性，再简化。

### security-and-hardening

> 代码安全加固检查清单

| 检查项 | 说明 |
|--------|------|
| 输入验证 | 所有外部输入需校验类型、长度、范围 |
| SQL 注入 | 使用参数化查询，避免字符串拼接 |
| XSS | 输出编码，CSP 头 |
| 认证 | 会话管理、密码存储（bcrypt/argon2） |
| 授权 | 越权检查、最小权限原则 |
| 敏感数据 | 密钥管理、环境变量、不硬编码 |
| 依赖安全 | 已知漏洞扫描 |

### performance-optimization

> 性能优化三步走

```
1. Profile — 找到真正的瓶颈（不要猜）
2. 定位 — 确定问题类型（CPU/内存/IO/网络）
3. 修复 — 针对性优化（缓存/算法/并发/批处理）
```

**重要：** 先 Profile 再优化，90% 的性能猜测是错的。

### incremental-implementation

> 小步快跑，每个步骤都可验证

```
Step 1: 理解现状 → 分析当前代码结构
Step 2: 规划步骤 → 拆解为独立可验证的小步
Step 3-: 逐步骤实现 → 每步后运行验证
Final: 整体回归 → 全量测试
```

**每步标准：** 可独立验证、可回滚、不影响已有功能。

### doubt-driven-development

> 针对非平凡决策的对抗性审查

适用场景：
- 架构设计决策
- 第三方依赖选择
- 数据模型设计
- 安全方案
- 任何"感觉不对劲"的决定

**方法：** 列出决策背后的所有假设 → 逐一尝试证伪 → 记录剩余风险。

### planning-and-task-breakdown

> 将需求转化为可执行的任务

```
需求 → 功能拆解 → 任务列表 → 依赖排序 → 估算 → 排期
```

每个任务包含：
- 明确的目标
- 验收标准
- 涉及的代码/文件
- 依赖的前置任务

### documentation-and-adrs

> 架构决策记录（ADR）与项目文档

ADR 格式：

```markdown
# ADR-001: 选择 PostgreSQL 作为主数据库

## 状态
已接受 | 提议 | 废弃

## 上下文
为什么需要这个决策？当前存在的问题是什么？

## 决策
我们决定做什么？

## 后果
这样做带来的收益和成本是什么？

## 替代方案
考虑过的其他选项及放弃的原因
```

### stress-report

> 压力测试与性能报告生成

生成内容：
- 测试环境与配置
- 压测结果数据（QPS、延迟、错误率）
- 资源使用分析（CPU、内存、IO）
- 瓶颈定位
- 优化建议

---

## 技能组合推荐

| 场景 | 推荐技能组合 |
|------|-------------|
| **新功能开发** | `spec-driven-development` → `planning-and-task-breakdown` → `incremental-implementation` → `code-review-and-quality` |
| **Bug 修复** | `debugging-and-error-recovery` → `test-driven-development` → `code-review-and-quality` |
| **性能优化** | `performance-optimization` → 修复 → `code-review-and-quality` |
| **安全审查** | `security-and-hardening` → `doubt-driven-development` |
| **发布上线** | `ci-cd-and-automation` → `shipping-and-launch` → `observability-and-instrumentation` |
| **重构** | `code-simplification` → `test-driven-development` → `incremental-implementation` |
| **架构设计** | `api-and-interface-design` → `documentation-and-adrs` → `doubt-driven-development` |
| **需求不清晰** | `interview-me` → `idea-refine` → `planning-and-task-breakdown` |

---

## 创建你自己的 Skill

在 `~/.claude/skills/` 下新建目录并编写 `SKILL.md`：

```markdown
---
name: my-custom-skill
description: Short description of when to use this skill. Use when [触发条件].
---

# My Custom Skill

## Overview

简要描述这个技能是做什么的、为什么需要它。

## When to Use

- 场景 1: 什么时候用
- 场景 2: 什么时候用

## Core Principles

### 原则 1
详细说明...

### 原则 2
详细说明...

## Process / Checklist

清晰的步骤或检查清单...

## Examples

### 示例 1
输入 → 输出

### 示例 2
输入 → 输出
```

**可选资源目录：**

```bash
mkdir -p ~/.claude/skills/my-custom-skill/{scripts,references,assets}
```

---

## 最佳实践

### 使用建议

- **遇到问题先选对技能** — 调试用 `debugging-and-error-recovery`，审查用 `code-review-and-quality`
- **复杂任务多技能组合** — 例如：先 `planning` 拆解任务，然后 `incremental-implementation` 逐步实现
- **重要决策先 `doubt-driven-development`** — 对抗性审查能发现很多隐藏问题
- **准备上线前跑 `shipping-and-launch`** — 确保有完整的发布、监控和回滚计划
- **不确定该用哪个技能时** — 加载 `using-agent-skills`，它会帮你分析需求并推荐合适的技能

### 技能设计原则

- **每个技能专注一个领域** — 不要做大而全
- **description 写明触发条件** — 这是自动匹配的关键
- **提供可操作的步骤** — 不要只描述"做什么"，要说明"怎么做"
- **检查清单优先** — 结构化的清单比长段落描述更有用
- **保持轻量** — 长示例和参考文档放在 `references/`，不要塞进 `SKILL.md`

---

## 维护指南

### 日常维护

```bash
# 查看所有技能
ls -d ~/.claude/skills/*/

# 检查未跟踪的文件
cd ~/.claude/skills && git status

# 推送更新
cd ~/.claude/skills && git add -A && git commit -m "update skill" && git push
```

### 注意事项

- 不要提交密钥、Token、私钥、许可证文件、客户数据或机器特定的运行时输出
- 每个技能保持专注，一个技能只做一件事
- 大型示例、脚本和参考文档放在 `SKILL.md` 外部，按需加载
- 推送前检查 `git status` 是否包含不应公开的文件

---

## 许可证

MIT

---

**相关资源：**
- [Claude Agents 仓库](https://github.com/mjzappzz/claude-agents) — 100+ 领域专家 Agent（含 J.A.R.V.I.S. 路由）
- [Codex Skills 仓库](https://github.com/mjzappzz/codex-skills) — 本仓库的源项目（Codex 版本的 26 个工程技能）
- [Claude Code 官方文档](https://docs.anthropic.com/en/docs/claude-code)
- [Anthropic 官方](https://anthropic.com)
