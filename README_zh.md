[English](README.md) | [简体中文](README_zh.md)

# Zero-DevToolbox

> 为 AI 编码工具精心配置的工具箱——Claude Code / Codex 的 Agent、Skill、编程准则，外加通用 ignore 模板和编辑器配置——让 AI 辅助开发真正好用。

![License](https://img.shields.io/badge/License-MIT-green)
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

Zero-DevToolbox 是一套即插即用的开发者工具箱，为多个 AI 编码工具扩展经过打磨的 Agent、工作流 Skill、编程准则和通用 ignore 模板。无需逐个配置，克隆本仓库即可获得跨工具的完整 AI 开发环境。

配置理念源于 Andrej Karpathy 对 LLM 编码陷阱的观察：
- **先思考，再编码** —— 明确假设，主动暴露权衡，不猜不蒙
- **简单优先** —— 用解决问题的最少代码，不写投机性的抽象
- **外科手术式改动** —— 只动必须动的地方，其余保持不变
- **目标驱动执行** —— 定义可验证的成功标准，循环到通过为止

## 功能特性

### AI 工具覆盖

| 工具 | 配置目录 | 包含内容 |
|------|---------|---------|
| [Claude Code](https://claude.ai/code) | `.claude/` | Agent、Skill、编程准则 |
| [Codex](https://github.com/openai/codex) | `.codex/` | Agent、Skill、编程准则 |
| [Cursor](https://cursor.com) | `.cursor/rules/` | 语义规则（自动应用） |

### 专用 Agent

5 个专用 Agent，Claude Code 和 Codex 共享：

| Agent | 模型 | 用途 |
|-------|------|------|
| `code-reviewer` | Opus | 全面代码审查：安全性、正确性、性能、可维护性 |
| `python-pro` | Sonnet | 生产级 Python：类型安全、异步模式、现代最佳实践 |
| `performance-engineer` | Sonnet | 识别并消除应用、数据库、基础设施的性能瓶颈 |
| `git-specialist` | Haiku | 复杂 Git 操作：冲突解决、rebase、分支管理 |
| `test-writer` | Sonnet | 为算法和优化代码编写单元测试（调度、运筹、数值计算） |

### Skill（斜杠命令）

Claude Code 和 Codex 中均可使用：

| Skill | 触发方式 | 功能说明 |
|-------|---------|---------|
| `/commit` | "提交" / "commit" / "push" | 读取 diff，生成简洁中文 commit 信息，自动执行 add → commit → push |
| `/readme` | "写个README" / "make a readme" | 为当前项目生成中英文双语 GitHub README |

### 编程准则

| 文件 | 说明 |
|------|------|
| `CLAUDE_coding_guidelines.md` / `AGENTS_coding_guidelines.md` | 四条工程原则：先思考再编码、简单优先、外科手术式改动、目标驱动执行。源自 Andrej Karpathy 对 LLM 编码陷阱的观察。 |
| `CLAUDE_python_algo.md` / `AGENTS_python_algo.md` | Python/算法项目约定：conda 环境管理、类型注解适用范围、numpy 向量化优先、随机算法（GA/SA/ALNS/PSO）必须支持固定随机种子以保证可复现性。 |

### 通用 Ignore 模板

`ignore/` 目录提供三份内容相同的忽略规则（`.gitignore`、`.claudeignore`、`.cursorignore`），覆盖：

- 密钥与凭据（`.env`、`*.pem`、`*.key`、`credentials.json` 等）
- 依赖目录（`node_modules/`、`.venv/`、`venv/` 等）
- 构建产物（`dist/`、`build/`、`__pycache__/` 等）
- 锁文件（`package-lock.json`、`yarn.lock`、`poetry.lock` 等）
- 测试与覆盖率输出（`coverage/`、`.pytest_cache/` 等）
- 日志与临时文件（`*.log`、`tmp/`、`*.bak`、`*.swp` 等）
- 数据库文件（`*.sqlite`、`*.db`、`dump.sql`）
- 二进制与媒体文件（`*.zip`、`*.png`、`*.mp4` 等）
- IDE 与系统文件（`.idea/`、`.vscode/`、`.DS_Store`、`Thumbs.db`）
- 工具缓存（`.cache/`、`.mypy_cache/`、`.ruff_cache/`）
- AI 工具内部文件（`.claude/sessions/`、`.codex/log/`）

### 编辑器配置

`.editorconfig` 统一编辑器格式设置：
- UTF-8 编码，LF 换行，自动去除行尾空格
- Python：4 空格缩进，最大 88 字符
- Web/配置文件：2 空格缩进
- Markdown：2 空格缩进，保留行尾空格
- Makefile：Tab 缩进

## 项目结构

```
Zero-DevToolbox/
├── .claude/                        # Claude Code 配置
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
├── .codex/                         # Codex 配置（与 .claude 镜像）
│   ├── AGENT/
│   │   ├── AGENTS_coding_guidelines.md  # 同上编程准则
│   │   └── AGENTS_python_algo.md        # 同上 Python 约定
│   └── skills/
│       ├── commit/SKILL.md         # 同上 commit 技能
│       └── readme/SKILL.md         # 同上 readme 技能
├── .cursor/rules/                  # Cursor 配置
│   └── karpathy-guidelines.mdc     # 编程准则（自动应用规则）
├── ignore/                         # 通用忽略规则模板
│   ├── .gitignore                  # Git 忽略规则
│   ├── .claudeignore               # Claude Code 忽略规则
│   └── .cursorignore               # Cursor 忽略规则
├── .editorconfig                   # 编辑器格式统一
├── README.md                       # 本文件（英文）
├── README_zh.md                    # 本文件（中文）
└── LICENSE                         # MIT
```

> **说明：** `.codex/` 下的 Agent（`general-purpose`、`code-reviewer`、`git-specialist`、`performance-engineer`、`python-pro`、`test-writer`）引用共享定义，映射到同名 Agent。

## 安装方法

**前提条件：** 已安装 [Claude Code](https://claude.ai/code) 和/或 [Codex](https://github.com/openai/codex) 和/或 [Cursor](https://cursor.com)。

按需复制配置到你的项目根目录：

```bash
# 克隆工具箱
git clone https://github.com/DreamCasterZero/Zero-DevToolbox.git

# 复制 Claude Code 配置
cp -r Zero-DevToolbox/.claude /path/to/your-project/

# 复制 Codex 配置
cp -r Zero-DevToolbox/.codex /path/to/your-project/

# 复制 Cursor 规则
cp -r Zero-DevToolbox/.cursor /path/to/your-project/

# 复制通用 ignore 模板
cp Zero-DevToolbox/ignore/.gitignore /path/to/your-project/
cp Zero-DevToolbox/ignore/.claudeignore /path/to/your-project/
cp Zero-DevToolbox/ignore/.cursorignore /path/to/your-project/

# 复制编辑器配置
cp Zero-DevToolbox/.editorconfig /path/to/your-project/
```

也可以直接 fork 本仓库，在此基础上构建你自己的项目。

> **提示：** 各工具的配置文件会被自动识别，无需额外注册。

## 使用方法

### 使用 Agent

Agent 会根据任务描述自动调用，也可以在对话中直接指定：

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

编程准则和 Python 约定作为持久化指令自动生效。Claude Code 和 Codex 在会话中自动遵循。Cursor 自动应用 `karpathy-guidelines.mdc`（已设置 `alwaysApply: true`）。

### Ignore 模板

三份 ignore 文件（`.gitignore`、`.claudeignore`、`.cursorignore`）内容相同。通过符号链接或复制到项目根目录，各工具将自动跳过密钥、依赖、构建产物、日志、数据库、二进制和缓存文件。

## 技术栈

- **[Claude Code](https://claude.ai/code)** —— Anthropic 的 AI 驱动 CLI
- **[Codex](https://github.com/openai/codex)** —— OpenAI 的编码 Agent
- **[Cursor](https://cursor.com)** —— AI 优先的代码编辑器
- **Markdown** —— 所有配置和准则均为纯 Markdown 文件
- **Git** —— 版本控制，`/commit` Skill 的基础工具

## 许可证

MIT © 2026 [DreamCasterZero](https://github.com/DreamCasterZero)
