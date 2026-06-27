[English](README.md) | [简体中文](README_zh.md)

# Zero-DevToolbox

> 为 Claude Code 精心配置的 Agent、Skill 和编程准则集合，让 AI 辅助开发真正好用。

![License](https://img.shields.io/badge/License-MIT-green)
![Claude Code](https://img.shields.io/badge/Claude%20Code-compatible-blue)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)

## 目录

- [项目简介](#项目简介)
- [功能特性](#功能特性)
- [项目结构](#项目结构)
- [安装方法](#安装方法)
- [使用方法](#使用方法)
- [技术栈](#技术栈)
- [许可证](#许可证)

## 项目简介

Zero-DevToolbox 是一套即插即用的 `.claude/` 配置，为 [Claude Code](https://claude.ai/code) 扩展了经过打磨的专用 Agent 和工作流 Skill。无需从零配置，克隆本仓库即可获得一套完整的 AI 开发环境——涵盖代码审查、Python 开发、性能优化、Git 操作、算法测试等专用 Agent，以及自动提交、生成 README 等常用 Skill。

配置理念来自 `CLAUDE_coding_guidelines.md`（源于 Andrej Karpathy 对 LLM 编码陷阱的观察）：
- **先思考，再编码** —— 明确假设，主动暴露权衡，不猜不蒙
- **简单优先** —— 用解决问题的最少代码，不写投机性的抽象
- **外科手术式改动** —— 只动必须动的地方，其余保持不变

## 功能特性

### 专用 Agent

| Agent | 模型 | 用途 |
|-------|------|------|
| `code-reviewer` | Opus | 全面代码审查：安全性、正确性、性能、可维护性 |
| `python-pro` | Sonnet | 生产级 Python：类型安全、异步模式、现代最佳实践 |
| `performance-engineer` | Sonnet | 识别并消除应用、数据库、基础设施的性能瓶颈 |
| `git-specialist` | Haiku | 复杂 Git 操作：冲突解决、rebase、分支管理 |
| `test-writer` | Sonnet | 为算法和优化代码编写单元测试（调度、运筹、数值计算） |

### Skill（斜杠命令）

| Skill | 触发方式 | 功能说明 |
|-------|---------|---------|
| `/commit` | "提交" / "commit" / "push" | 读取 diff，生成简洁中文 commit 信息，自动执行 add → commit → push |
| `/readme` | "写个README" / "make a readme" | 为当前项目生成中英文双语 GitHub README |

### CLAUDE 编程准则

- **`CLAUDE_coding_guidelines.md`** —— 四条工程原则：先思考再编码、简单优先、外科手术式改动、目标驱动执行。每条都有具体的执行标准，帮助 LLM 规避常见编码陷阱。
- **`CLAUDE_python_algo.md`** —— Python/算法项目专属约定：conda 环境管理、类型注解适用范围、numpy 向量化优先、随机算法（GA/SA/ALNS/PSO）必须支持固定随机种子以保证可复现性。

## 项目结构

```
Zero-DevToolbox/
├── .claude/
│   ├── agents/
│   │   ├── code-reviewer.md        # 代码质量与安全审查
│   │   ├── python-pro.md           # 生产级 Python 开发
│   │   ├── performance-engineer.md # 性能优化工程
│   │   ├── git-specialist.md       # 复杂 Git 操作
│   │   └── test-automator.md       # 算法单元测试
│   ├── skills/
│   │   ├── commit/SKILL.md         # 自动中文提交并推送
│   │   └── readme/SKILL.md         # 双语 README 生成
│   └── CLAUDE/
│       ├── CLAUDE_coding_guidelines.md  # 编程行为准则
│       └── CLAUDE_python_algo.md        # Python/算法项目约定
└── LICENSE
```

## 安装方法

**前提条件：** 已安装并完成认证的 [Claude Code](https://claude.ai/code)。

将 `.claude/` 目录复制到你的项目根目录：

```bash
# 克隆工具箱
git clone https://github.com/DreamCasterZero/Zero-DevToolbox.git

# 复制配置到你的项目
cp -r Zero-DevToolbox/.claude /path/to/your-project/
```

也可以直接 fork 本仓库，在此基础上构建你自己的项目。

> **提示：** `.claude/` 目录下的 Agent 和 Skill 文件会被 Claude Code 自动识别，无需额外注册。

## 使用方法

### 使用 Agent

Agent 会根据任务描述由 Claude Code 自动调用，也可以在对话中直接指定：

```
用 code-reviewer 审查这个 PR 的安全性。
用 git-specialist 帮我解决这个 merge 冲突。
```

### 使用 Skill

Skill 通过斜杠命令或自然语言短语触发：

```
/commit          # 自动生成中文 commit 并提交推送
/readme          # 为当前项目生成双语 README

# 或使用自然语言：
"提交一下"       # 触发 /commit
"写个README"     # 触发 /readme
```

### 应用编程准则

`CLAUDE/` 目录下的文件会作为持久化指令自动生效，Claude Code 在整个会话中都会遵循其中的编程准则和 Python 约定。

## 技术栈

- **[Claude Code](https://claude.ai/code)** —— AI 驱动的软件开发 CLI
- **Markdown** —— 所有配置和准则均为纯 Markdown 文件
- **Git** —— 版本控制，`/commit` Skill 的基础工具

## 许可证

MIT © 2026 [DreamCasterZero](https://github.com/DreamCasterZero)
