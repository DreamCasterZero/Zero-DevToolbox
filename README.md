[English](README.md) | [简体中文](README_zh.md)

# Zero-DevToolbox

> A curated collection of Claude Code agents, skills, and coding guidelines to supercharge your AI-assisted development workflow.

![License](https://img.shields.io/badge/License-MIT-green)
![Claude Code](https://img.shields.io/badge/Claude%20Code-compatible-blue)
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

Zero-DevToolbox is a drop-in `.claude/` configuration that extends [Claude Code](https://claude.ai/code) with battle-tested agents and workflow skills. Instead of starting from scratch, clone this repo and get a fully-wired AI development environment with specialized agents for code review, Python development, performance engineering, git operations, and algorithm testing — plus skills that automate common chores like writing commit messages and generating READMEs.

The configuration philosophy follows three principles (from `CLAUDE_coding_guidelines.md`):
- **Think first, code second** — no guessing, expose trade-offs explicitly
- **Simplest thing that works** — no speculative abstractions or unnecessary flexibility
- **Surgical changes** — only touch what the task actually requires

## Features

### Agents

| Agent | Model | Purpose |
|-------|-------|---------|
| `code-reviewer` | Opus | Comprehensive review: security, correctness, performance, maintainability |
| `python-pro` | Sonnet | Production-ready Python: type safety, async patterns, modern best practices |
| `performance-engineer` | Sonnet | Identify and eliminate bottlenecks across app, database, and infrastructure |
| `git-specialist` | Haiku | Complex git operations: conflict resolution, rebase, branch management |
| `test-writer` | Sonnet | Unit tests for algorithms and optimization code (scheduling, OR, numerics) |

### Skills (Slash Commands)

| Skill | Trigger | What it does |
|-------|---------|--------------|
| `/commit` | "提交" / "commit" / "push" | Reads the diff, writes a concise Chinese commit message, then `git add` → `commit` → `push` |
| `/readme` | "写个README" / "make a readme" | Generates bilingual (English + Chinese) GitHub README for the current project |

### CLAUDE Guidelines

- **`CLAUDE_coding_guidelines.md`** — Four engineering principles derived from Andrej Karpathy's observations on LLM coding pitfalls: think before coding, prefer simplicity, make surgical changes, and define verifiable success criteria.
- **`CLAUDE_python_algo.md`** — Project conventions for Python/algorithm work: conda environment management, type annotation scope, numpy-first numerics, and reproducibility requirements for stochastic algorithms (GA, SA, ALNS, PSO).

## Project Structure

```
Zero-DevToolbox/
├── .claude/
│   ├── agents/
│   │   ├── code-reviewer.md       # Code quality & security review
│   │   ├── python-pro.md          # Production Python development
│   │   ├── performance-engineer.md # Performance optimization
│   │   ├── git-specialist.md      # Advanced git operations
│   │   └── test-automator.md      # Algorithm unit testing
│   ├── skills/
│   │   ├── commit/SKILL.md        # Auto Chinese commit & push
│   │   └── readme/SKILL.md        # Bilingual README generation
│   └── CLAUDE/
│       ├── CLAUDE_coding_guidelines.md  # Engineering behavior guidelines
│       └── CLAUDE_python_algo.md        # Python/algorithm conventions
└── LICENSE
```

## Installation

**Prerequisites:** [Claude Code](https://claude.ai/code) installed and authenticated.

Copy the `.claude/` directory into your project root:

```bash
# Clone the toolbox
git clone https://github.com/DreamCasterZero/Zero-DevToolbox.git

# Copy configuration into your project
cp -r Zero-DevToolbox/.claude /path/to/your-project/
```

Or use it as a starting point by forking/cloning and building your project on top of it.

> **Note:** Agent and skill files in `.claude/` are automatically picked up by Claude Code — no additional registration step required.

## Usage

### Using Agents

Agents are invoked automatically by Claude Code when the task matches their description, or you can reference them explicitly:

```
Review the security of this PR using the code-reviewer agent.
Use the git-specialist to help me resolve this merge conflict.
```

### Using Skills

Skills are triggered by slash commands or natural-language phrases:

```
/commit          # Auto-commit with Chinese message
/readme          # Generate bilingual README for this project

# Or use natural language:
"提交一下"       # triggers /commit
"写个README"     # triggers /readme
```

### Applying Guidelines

The `CLAUDE/` files are picked up as persistent instructions. Claude Code will apply the coding guidelines and Python conventions automatically throughout your session.

## Tech Stack

- **[Claude Code](https://claude.ai/code)** — AI-powered CLI for software development
- **Markdown** — All configuration and guidelines are plain Markdown files
- **Git** — Version control, used by the `/commit` skill

## License

MIT © 2026 [DreamCasterZero](https://github.com/DreamCasterZero)
