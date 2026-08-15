[English](README.md) | 简体中文

# Zero-DevToolbox

> 一套简洁、通用、低耦合，可跨项目复用的 AI 辅助开发 Skill。

![License](https://img.shields.io/badge/License-MIT-green)

Zero-DevToolbox 目前在 `.agents/skills/` 下提供 9 个按需调用的工作流 Skill。与围绕某个具体项目架构或业务规则编写的 Skill 不同，这些 Skill 保存的是通用工作流，执行时再读取目标仓库的真实内容。将整套 Skill 或所需的单个 Skill 目录复制到新项目后，即可直接使用，无需重写核心指令。

这些 Skill 用于解决开发中的常见问题，包括代码冗余、调用流程难以追踪、文档不一致、Git 交付流程重复，以及 Codex 跨会话后项目上下文丢失。仓库还包含 Cursor 规则、通用 ignore 模板和 EditorConfig 配置。

## 为什么适合跨项目复用

- **低耦合：** 工作流不写死某个应用的模块、框架、数据模型或业务逻辑，而是从目标项目的代码、配置、测试、`AGENTS.md` 和文档中获取所需信息。
- **可直接迁移：** 每个 Skill 职责单一并拥有独立目录。可以复制完整的 `.agents/skills/`，也可以只选择当前项目需要的工作流。
- **简洁且聚焦：** Skill 围绕明确目标执行，避免无关修改，并为常见开发任务内置安全边界和验证要求。
- **保持上下文连续：** `$init-project-knowledge` 会创建轻量、结构化、可版本管理的项目知识库，`$update-project-knowledge` 只记录经过确认且长期有效的变化，两者共同减少跨会话时重要项目上下文的丢失。
- **区别于项目专用 Skill：** 项目专用 Skill 通常固化某个仓库的架构或内部流程；Zero-DevToolbox 提供的是能够适应安装目标仓库的通用工作流。

## 内置 Skill

所有 Skill 都需要使用 `$skill-name` 显式调用。每个 Skill 附带的 `agents/openai.yaml` 均已禁用隐式调用。

| Skill | 用途 |
|---|---|
| `$add-code-comments` | 为指定代码范围补充简洁注释且不改变行为；适用于支持 `//` 注释的语言。 |
| `$commit` | 检查 Git 改动、生成符合仓库风格的提交信息，然后暂存、提交并推送选定改动。 |
| `$generate-latex-document` | 使用内置模板将笔记或代码库分析整理为独立的 `.tex` 文档；不会在本地编译 PDF。 |
| `$init-project-knowledge` | 分析项目并初始化或完善由 `AGENTS.md` 引导的结构化知识库。 |
| `$optimize-target-code` | 分析并优化指定函数、类、文件或小范围功能，同时保持行为并验证修改。 |
| `$readme` | 根据项目真实代码、配置、脚本和文档创建、检查或同步中英文 README。 |
| `$reduce-code-redundancy` | 审计重复实现、未使用代码、冗余文件和可复用工具；仅清理证据充分的内容。 |
| `$trace-code-flow` | 以只读方式追踪指定功能的调用链、数据流、状态变化、单位和坐标系。 |
| `$update-project-knowledge` | 仅在已完成工作产生经过确认且长期有效的信息时更新现有项目知识库。 |

## 快速开始

克隆仓库：

```bash
git clone https://github.com/DreamCasterZero/Zero-DevToolbox.git
```

如果 AI 编码工具从 `.agents/skills/` 发现项目级 Skill，请将完整集合或选定的 Skill 目录复制到目标项目的 `.agents/skills/` 目录。

macOS/Linux：

```bash
mkdir -p /path/to/your-project/.agents
cp -R Zero-DevToolbox/.agents/skills /path/to/your-project/.agents/
```

PowerShell：

```powershell
New-Item -ItemType Directory -Force C:\path\to\your-project\.agents
Copy-Item -Recurse Zero-DevToolbox\.agents\skills C:\path\to\your-project\.agents\
```

随后在 AI 编码会话中显式调用所需工作流：

```text
$trace-code-flow 追踪结账请求从 API 端点到数据库写入的流程。
$optimize-target-code 优化 src/parser.ts 中的解析器并运行相关测试。
$readme 检查当前项目并更新中英文 README。
```

每个 `SKILL.md` 都定义了工作流的范围、安全规则、验证方式和完成报告。需要目标文件或功能的工作流会要求用户明确范围，不会直接扫描整个项目。

## 配套配置

### Cursor 规则

`.cursor/rules/karpathy-guidelines.mdc` 是一条始终应用的 Cursor 规则，强调明确假设、采用简单方案、保持改动聚焦，以及定义可验证的成功标准。将 `.cursor/` 复制到项目中即可使用。

### Ignore 模板

`ignore/` 包含 `.gitignore`、`.claudeignore` 和 `.cursorignore` 模板，覆盖常见密钥、依赖、生成内容、日志、数据库、媒体文件、编辑器元数据和缓存。

复制前请检查具体规则：默认模板会忽略锁文件和图片等内容，而部分项目需要提交这些文件。

### EditorConfig

`.editorconfig` 设置 UTF-8、LF、文件末尾换行、行尾空格处理方式，以及 Python、Web/配置文件、Markdown、Makefile 和 Shell 脚本的缩进。

## 仓库结构

```text
.agents/skills/                 9 个需要显式调用的工作流 Skill
  generate-latex-document/     包含一个模板和两份工作流参考
.cursor/rules/                 始终应用的 Cursor 编码规则
ignore/                        Git、Claude Code 和 Cursor ignore 模板
.editorconfig                  通用编辑器格式配置
LICENSE                        MIT 许可证
README.md                      英文项目说明
README_zh.md                   中文项目说明
```

本仓库包含配置以及 Markdown/LaTeX 资源，不是可执行应用，因此没有依赖安装、构建或自动测试命令。

## 许可证

本项目采用 [MIT License](LICENSE)。Copyright (c) 2026 DreamCasterZero。
