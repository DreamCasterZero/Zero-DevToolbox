[English](README.md) | [简体中文](README_zh.md)

# Zero-DevToolbox

> A curated collection of AI coding tool configurations — Claude Code / Codex agents, skills, coding guidelines, ignore templates, and editor settings — to supercharge your AI-assisted development workflow.

![License](https://img.shields.io/badge/License-MIT-green)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Tech Stack](#tech-stack)
- [License](#license)

## Introduction

Zero-DevToolbox is a drop-in developer toolbox that extends AI coding tools with battle-tested agents, workflow skills, coding guidelines, and shared ignore files. Instead of configuring each AI tool from scratch, clone this repo and get a fully-wired environment across multiple tools.

The configuration philosophy follows four principles:
- **Think first, code second** — no guessing, surface trade-offs explicitly
- **Simplest thing that works** — no speculative abstractions or unnecessary flexibility
- **Surgical changes** — only touch what the task actually requires
- **Goal-driven execution** — define verifiable success criteria and loop until met

## Features

### AI Coding Tools Coverage

| Tool | Config Directory | What's Included |
|------|-----------------|-----------------|
| [Claude Code](https://claude.ai/code) | `.claude/` | Agents, skills, coding guidelines |
| [Codex](https://github.com/openai/codex) | `.codex/` | Agents, skills, coding guidelines |
| [Cursor](https://cursor.com) | `.cursor/rules/` | Semantic rules (auto-applied) |

### Agents

5 specialized agents shared across Claude Code and Codex:

| Agent | Model | Purpose |
|-------|-------|---------|
| `code-reviewer` | Opus | Comprehensive review: security, correctness, performance, maintainability |
| `python-pro` | Sonnet | Production-ready Python: type safety, async patterns, modern best practices |
| `performance-engineer` | Sonnet | Identify and eliminate bottlenecks across app, database, and infrastructure |
| `git-specialist` | Haiku | Complex git operations: conflict resolution, rebase, branch management |
| `test-writer` | Sonnet | Unit tests for algorithms and optimization code (scheduling, OR, numerics) |

### Skills (Slash Commands)

Available in both Claude Code and Codex:

| Skill | Trigger | What it does |
|-------|---------|--------------|
| `/commit` | "提交" / "commit" / "push" | Reads the diff, writes a concise Chinese commit message, then `git add` → `commit` → `push` |
| `/readme` | "写个README" / "make a readme" | Generates bilingual (English + Chinese) GitHub README for the current project |

### Coding Guidelines

| File | Description |
|------|-------------|
| `CLAUDE_coding_guidelines.md` / `AGENTS_coding_guidelines.md` | Four engineering principles: think first, prefer simplicity, make surgical changes, goal-driven execution. Derived from Andrej Karpathy's observations on LLM coding pitfalls. |
| `CLAUDE_python_algo.md` / `AGENTS_python_algo.md` | Python/algorithm conventions: conda env management, type annotation scope, numpy-first numerics, reproducibility via fixed seeds for stochastic algorithms (GA, SA, ALNS, PSO). |

### Shared Ignore Templates

The `ignore/` directory contains identical `.gitignore`, `.claudeignore`, and `.cursorignore` files covering:

- Secrets & credentials (`.env`, `*.pem`, `*.key`, etc.)
- Dependency directories (`node_modules/`, `.venv/`, `venv/`, etc.)
- Build artifacts (`dist/`, `build/`, `__pycache__/`, etc.)
- Lock files (`package-lock.json`, `yarn.lock`, `poetry.lock`, etc.)
- Test & coverage outputs (`coverage/`, `.pytest_cache/`, etc.)
- Logs & temporary files (`*.log`, `tmp/`, `*.bak`, `*.swp`, etc.)
- Database files (`*.sqlite`, `*.db`, `dump.sql`)
- Binary & media files (`*.zip`, `*.png`, `*.mp4`, etc.)
- IDE & system files (`.idea/`, `.vscode/`, `.DS_Store`, `Thumbs.db`)
- Tool caches (`.cache/`, `.mypy_cache/`, `.ruff_cache/`)
- AI tool internals (`.claude/sessions/`, `.codex/log/`)

### Editor Configuration

`.editorconfig` enforces consistent formatting across editors:
- UTF-8, LF line endings, trailing whitespace trimmed
- Python: 4-space indent, max 88 chars
- Web/config files: 2-space indent
- Markdown: 2-space indent, trailing whitespace preserved
- Makefile: tab indent

## Project Structure

```
Zero-DevToolbox/
├── .claude/                        # Claude Code configuration
│   ├── agents/
│   │   ├── code-reviewer.md        # Code quality & security review
│   │   ├── python-pro.md           # Production Python development
│   │   ├── performance-engineer.md # Performance optimization
│   │   ├── git-specialist.md       # Advanced git operations
│   │   └── test-automator.md       # Algorithm unit testing
│   ├── skills/
│   │   ├── commit/SKILL.md         # Auto Chinese commit & push
│   │   └── readme/SKILL.md         # Bilingual README generation
│   └── CLAUDE/
│       ├── CLAUDE_coding_guidelines.md  # Engineering behavior guidelines
│       └── CLAUDE_python_algo.md        # Python/algorithm conventions
├── .codex/                         # Codex configuration (mirrors .claude/)
│   ├── AGENT/
│   │   ├── AGENTS_coding_guidelines.md  # Same coding guidelines
│   │   └── AGENTS_python_algo.md        # Same Python conventions
│   └── skills/
│       ├── commit/SKILL.md         # Same commit skill
│       └── readme/SKILL.md         # Same readme skill
├── .cursor/rules/                  # Cursor configuration
│   └── karpathy-guidelines.mdc     # Coding guidelines (auto-applied rule)
├── ignore/                         # Shared ignore templates
│   ├── .gitignore                  # Git ignore patterns
│   ├── .claudeignore               # Claude Code ignore patterns
│   └── .cursorignore               # Cursor ignore patterns
├── .editorconfig                   # Editor formatting rules
├── README.md                       # This file (English)
├── README_zh.md                    # This file (Chinese)
└── LICENSE                         # MIT
```

> **Note:** `.codex/` agents (`general-purpose`, `code-reviewer`, `git-specialist`, `performance-engineer`, `python-pro`, `test-writer`) are referenced from shared definitions and map to the same agent names.

## Installation

**Prerequisites:** [Claude Code](https://claude.ai/code) and/or [Codex](https://github.com/openai/codex) and/or [Cursor](https://cursor.com) installed.

Copy what you need into your project root:

```bash
# Clone the toolbox
git clone https://github.com/DreamCasterZero/Zero-DevToolbox.git

# Copy Claude Code configuration
cp -r Zero-DevToolbox/.claude /path/to/your-project/

# Copy Codex configuration
cp -r Zero-DevToolbox/.codex /path/to/your-project/

# Copy Cursor rules
cp -r Zero-DevToolbox/.cursor /path/to/your-project/

# Copy shared ignore templates
cp Zero-DevToolbox/ignore/.gitignore /path/to/your-project/
cp Zero-DevToolbox/ignore/.claudeignore /path/to/your-project/
cp Zero-DevToolbox/ignore/.cursorignore /path/to/your-project/

# Copy editor config
cp Zero-DevToolbox/.editorconfig /path/to/your-project/
```

Or fork/clone and build your project on top of this repo directly.

> **Tip:** Config files are automatically picked up by their respective tools — no registration step needed.

## Usage

### Agents

Agents are invoked automatically when the task matches their description, or you can reference them explicitly:

```
Review the security of this PR using the code-reviewer agent.
Use the git-specialist to help me resolve this merge conflict.
```

### Skills

Skills are triggered by slash commands or natural-language phrases:

```
/commit          # Auto-commit with Chinese message
/readme          # Generate bilingual README for this project

# Or use natural language:
"提交一下"       # triggers /commit
"写个README"     # triggers /readme
```

### Guidelines

The coding guidelines and Python conventions are picked up as persistent instructions. Both Claude Code and Codex apply them automatically throughout your session. Cursor applies `karpathy-guidelines.mdc` automatically (with `alwaysApply: true`).

### Ignore Templates

The three ignore files (`.gitignore`, `.claudeignore`, `.cursorignore`) share identical patterns. Symlink or copy them into your project root so each tool skips secrets, dependencies, build artifacts, logs, databases, binaries, and cache files.

## Tech Stack

- **[Claude Code](https://claude.ai/code)** — Anthropic's AI-powered CLI
- **[Codex](https://github.com/openai/codex)** — OpenAI's coding agent
- **[Cursor](https://cursor.com)** — AI-first code editor
- **Markdown** — All configuration and guidelines are plain Markdown
- **Git** — Version control, used by the `/commit` skill

## License

MIT © 2026 [DreamCasterZero](https://github.com/DreamCasterZero)
