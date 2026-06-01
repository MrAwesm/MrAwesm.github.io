---
layout: post
title: "Claude Code Rules & Memory 系统 — 速读笔记"
date: 2026-06-01
categories: [AI-tools, workflow]
tags: [Claude-Code, rules, memory, auto-memory, agent-memory]
---

# Claude Code Rules & Memory 系统 — 速读笔记

一句话先甩出来：**Rules 是墙上的告示牌，Memory 是跨会话的笔记本。前者按条件自动贴，后者按角色自己写。**

---

## 一、Rules 系统 — 条件加载的告示牌

### 🪧 Rules vs CLAUDE.md — 啥区别？

| 维度 | CLAUDE.md | Rules |
|------|-----------|-------|
| 加载时机 | 每次会话启动全量加载 | 按 `paths:` 条件懒加载 |
| 上下文开销 | 固定占用 | 按需占用 |
| 文件位置 | `.claude/CLAUDE.md`、`~/.claude/CLAUDE.md` | `.claude/rules/*.md`、`~/.claude/rules/*.md` |
| 约束力 | 软（prompt 级） | 软（prompt 级） |

💡 **一句话**：CLAUDE.md 是"公告板"，Rules 是"按工种发的操作规范"。

---

### 🏗️ 两种加载模式

**无 `paths:` → 会话启动时全量加载**

```yaml
# .claude/rules/general-style.md
# （无 frontmatter 或无 paths）
# → 每次会话都加载，效果等同 CLAUDE.md
```

**有 `paths:` → 触摸匹配文件时懒加载**

```yaml
# .claude/rules/python-style.md
---
paths:
  - "src/**/*.py"
  - "scripts/*.py"
---
# → 只有 Claude 读/写 .py 文件时才加载
```

🔑 **核心收益**：5 个文件类型规范 × 各 30 行 = 150 行。用 paths 拆分后，每次会话只加载相关规范，**上下文不浪费**。

![Rules 加载模式对比](/images/posts/rules-and-memory-notes/rules-loading-flow.svg)
<center><small>无 paths 全量加载 vs 有 paths 懒加载流程对比</small></center>

---

### ⚠️ Rules 的隐式失败 — 最容易踩的坑

Rules 没生效？**两个排查方向**：

| 排查层 | 问题 | 现象 |
|--------|------|------|
| 1. 加载了吗？ | `paths:` 没匹配到被编辑的文件 | Rule 静默跳过，**无报错无提示** |
| 2. 被遵守了吗？ | Rule 是软约束，模型可能不遵守 | Claude "忽略" 了规则 |

⚠️ **关键**：paths 不匹配 = 沉默失败，不像 allowedTools 缺工具会报错。调试 Rules 问题时，永远先确认"加载了吗"。

---

### 🔀 谁能看到 Rules？

| 上下文 | CLAUDE.md | Rules（有/无 paths） |
|--------|-----------|---------------------|
| **主会话** | ✅ | ✅ |
| **Subagent** | ✅ 启动时注入 | ❌ 不继承 |
| **Skill** | ✅ 在主会话内执行 | ✅ 继承主会话 |

🔑 **关键**：CLAUDE.md 是**唯一跨主会话+Subagent 可见的知识载体**。Subagent 看不到 Rules。

---

## 二、Memory 系统 — 四套记忆各管各的

### 📝 四套系统一览

| 系统 | 谁写 | 谁读 | 位置 | 持久？ |
|------|------|------|------|--------|
| **CLAUDE.md** | 人手写 | 主会话 + Subagent | 项目根 / `~/.claude/` | 永久 |
| **Rules** | 人手写 | 主会话 | `.claude/rules/` | 永久 |
| **Auto Memory** | Claude 自动 | 仅主会话 | `~/.claude/projects/<hash>/memory/` | 永久 |
| **Agent Memory** | Agent 自己 | 仅该 Agent | 三个 scope 可选 | 永久 |

💡 **隔离原则**：主会话看不到 Agent Memory，Agent 也看不到 Auto Memory。**两套系统完全隔离**。

![Memory 四套系统架构](/images/posts/rules-and-memory-notes/memory-systems-architecture.svg)
<center><small>四套 Memory 系统的写入者、可见性和存储位置</small></center>

---

### 🧠 Agent Memory 三种 Scope

| Scope | 存储位置 | Git 提交？ | 适用场景 |
|-------|----------|-----------|----------|
| **user** | `~/.claude/agent-memory/<name>/` | 否 | 跨项目通用知识（**推荐默认**） |
| **project** | `.claude/agent-memory/<name>/` | 是 | 项目特定经验，团队共享 |
| **local** | `.claude/agent-memory-local/<name>/` | 否（git-ignored） | 个人调试笔记 |

🔑 **选择逻辑**：
- 团队要共享 → `project`
- 跨项目通用 → `user`
- 个人临时 → `local`

![Agent Memory 三种 Scope](/images/posts/rules-and-memory-notes/agent-memory-scopes.svg)
<center><small>Agent Memory 的三种 scope 存储位置与 Git 提交策略</small></center>

---

### 📦 Agent Memory 的 200 行限制

Agent 启动时只注入 `MEMORY.md` **前 200 行**到系统 prompt。

```
正确做法：
MEMORY.md        → 索引（前 200 行，自动加载）
├── api-patterns.md    → 细节（按需 Read）
└── historical.md      → 细节（按需 Read）

错误做法：
MEMORY.md        → 全部内容塞进去，500 行
→ 200 行以后的内容 Agent 看不到
```

💡 和 Rules 的 progressive disclosure 同理 — **入口轻量，按需加载**。

---

## 三、约束层次模型 — 谁说了算？

从硬到软排个队：

| 层次 | 机制 | 强度 | 类比 |
|------|------|------|------|
| 🔒 硬约束 | `allowedTools` / Hook 拦截 | 技术强制 | 物理锁 |
| 📋 中约束 | Agent prompt Execution Contract | 大概率遵守 | 劳动合同 |
| 📝 软约束 | CLAUDE.md / Rules | 可能被绕过 | 门上贴纸条 |

![约束层次模型](/images/posts/rules-and-memory-notes/constraint-layers.svg)
<center><small>从硬到软的三层约束模型与类比</small></center>

### ⚔️ 冲突时谁赢？

| 冲突方向 | 结果 | 原因 |
|----------|------|------|
| CLAUDE.md 禁止，allowedTools 允许 | 大概率服从 CLAUDE.md | 模型倾向遵守 prompt |
| CLAUDE.md 要求，allowedTools 禁止 | **allowedTools 赢** | 运行时硬拦截 |
| Rule 说 A，CLAUDE.md 说 B | 不确定 | 无冲突检测机制 |

🔑 **设计原则**：**不制造冲突**。硬约束定义能力边界，软约束定义行为偏好。真要禁止某操作 → 从 allowedTools 删掉对应工具。

---

## 四、全系统可见性矩阵 — 一张表搞定

| 系统 | 主会话 | Subagent | Skill | 加载时机 |
|------|--------|----------|-------|----------|
| CLAUDE.md | ✅ | ✅ 注入 | ✅ | 会话启动 |
| Rules（无 paths） | ✅ | ❌ | ✅ | 会话启动 |
| Rules（有 paths） | ✅ 触发时 | ❌ | ✅ 触发时 | 文件匹配时 |
| Auto Memory | ✅ | ❌ | ✅ | 会话启动 |
| Agent Memory | ❌ | ✅ 仅自己的 | ❌ | Agent 启动（前 200 行） |
| 预加载 Skills | ❌ | ✅ | — | Agent 启动时注入 |

![可见性矩阵](/images/posts/rules-and-memory-notes/visibility-matrix.svg)
<center><small>各系统在不同上下文中的可见性与加载时机</small></center>

🔑 **唯一跨两层可见的**：CLAUDE.md。设计跨层级约束时，放 CLAUDE.md 最可靠。

---

## 五、决策卡汇总

### 🪧 Rules

| 问题 | 答案 |
|------|------|
| **何时用** | 项目级条件约束、按文件类型/路径的规范、拆分过大 CLAUDE.md |
| **何时不用** | Agent 内部行为约束（用 Agent prompt）、一次性知识（用 Skill） |
| **关键取舍** | 有 `paths:` = 懒加载省上下文 / 无 `paths:` = 立即加载保证生效 |
| **最大坑** | paths 不匹配 = 静默失败，无报错 |

### 🧠 Agent Memory

| 问题 | 答案 |
|------|------|
| **何时用** | Agent 需要跨会话积累经验、记住模式、保留历史 |
| **何时不用** | 一次性任务、不需要记忆的简单查询 |
| **关键取舍** | user scope = 跨项目但不共享 / project = 团队共享但锁项目 / local = 个人调试 |

### 📝 Auto Memory

| 问题 | 答案 |
|------|------|
| **何时用** | Claude 主会话自动学习，无需手动干预 |
| **何时不用** | 需要 Agent 共享知识（Agent 看不到 Auto Memory） |
| **关键取舍** | 便捷但只对主会话生效，Agent 完全隔离 |

---

## 💎 全文一句话收尾

> **CLAUDE.md 全局可见，Rules 主会话可见，Agent Memory 只 Agent 可见，Auto Memory 只主会话可见。**
> 约束从硬到软：allowedTools > Agent prompt > CLAUDE.md/Rules。
> 记住一条：**想禁止某操作，别贴纸条 — 直接把工具从 allowedTools 里删掉。**
