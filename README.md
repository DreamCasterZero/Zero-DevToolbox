English | [简体中文](README_zh.md)

# Zero-DevToolbox

> A compact collection of reusable, low-coupling skills for AI-assisted development across projects.

![License](https://img.shields.io/badge/License-MIT-green)

Zero-DevToolbox currently provides nine opt-in workflow skills under `.agents/skills/`. Unlike skills written around one application's architecture or business rules, these skills contain project-agnostic workflows that inspect the target repository at runtime. Copy the collection, or only the skill directories you need, into a new project and use them without rewriting their core instructions.

The skills address recurring development problems such as redundant code, difficult code-flow analysis, inconsistent documentation, repetitive Git delivery, and project context being lost between Codex sessions. The repository also includes a Cursor rule, shared ignore templates, and EditorConfig settings.

## Why these skills are reusable

- **Low coupling:** the workflows do not hard-code a specific application's modules, framework, data model, or business logic. They derive relevant details from the target project's code, configuration, tests, `AGENTS.md`, and documentation.
- **Portable by design:** each skill has a focused responsibility and lives in its own directory. Copy the complete `.agents/skills/` collection or select only the workflows a project needs.
- **Focused and concise:** skills operate on an explicit target, avoid unrelated changes, and include safety and verification rules for common development tasks.
- **Context continuity:** `$init-project-knowledge` creates a lightweight, structured, version-controlled project knowledge base, while `$update-project-knowledge` records only confirmed, durable changes. Together they reduce the loss of important project context across sessions.
- **Different from project-specific skills:** project-specific skills encode one repository's architecture or internal process. Zero-DevToolbox supplies general workflows that adapt to the repository where they are installed.

## Included skills

Invoke each skill explicitly with its `$skill-name`. All bundled `agents/openai.yaml` files disable implicit invocation.

| Skill | Purpose |
|---|---|
| `$add-code-comments` | Add concise comments to a specified code scope without changing behavior; intended for languages that support `//` comments. |
| `$commit` | Inspect Git changes, prepare a repository-style commit message, then stage, commit, and push the selected changes. |
| `$generate-latex-document` | Turn notes or codebase analysis into a standalone `.tex` document using the bundled template; it does not compile a PDF locally. |
| `$init-project-knowledge` | Analyze a project and initialize or complete an `AGENTS.md`-guided, structured knowledge base. |
| `$optimize-target-code` | Analyze and optimize a specified function, class, file, or small feature while preserving behavior and validating the change. |
| `$readme` | Create, review, or synchronize English and Chinese READMEs from the project's actual code, configuration, scripts, and documentation. |
| `$reduce-code-redundancy` | Audit duplicate implementations, unused code, redundant files, and reusable utilities; cleanup requires verified evidence. |
| `$trace-code-flow` | Read-only tracing of a specified feature's call chain, data flow, state changes, units, and coordinate systems. |
| `$update-project-knowledge` | Update an existing knowledge base only when completed work produced confirmed, durable information. |

## Quick start

Clone the repository:

```bash
git clone https://github.com/DreamCasterZero/Zero-DevToolbox.git
```

For a tool that discovers project-local skills from `.agents/skills/`, copy the full collection or selected skill directories into the target project's `.agents/skills/` directory.

macOS/Linux:

```bash
mkdir -p /path/to/your-project/.agents
cp -R Zero-DevToolbox/.agents/skills /path/to/your-project/.agents/
```

PowerShell:

```powershell
New-Item -ItemType Directory -Force C:\path\to\your-project\.agents
Copy-Item -Recurse Zero-DevToolbox\.agents\skills C:\path\to\your-project\.agents\
```

Then invoke the required workflow explicitly:

```text
$trace-code-flow trace the checkout request from its API endpoint to the database write.
$optimize-target-code optimize the parser in src/parser.ts and run its focused tests.
$readme check this project and update its English and Chinese READMEs.
```

Each `SKILL.md` defines the workflow's scope, safety rules, validation, and completion report. Workflows that need a target file or feature ask for that scope instead of scanning the entire project.

## Supporting configuration

### Cursor rule

`.cursor/rules/karpathy-guidelines.mdc` is an always-applied Cursor rule that emphasizes surfaced assumptions, simple solutions, focused changes, and verifiable success criteria. Copy `.cursor/` into a project to use it there.

### Ignore templates

`ignore/` contains `.gitignore`, `.claudeignore`, and `.cursorignore` templates covering common secrets, dependencies, generated output, logs, databases, media, editor metadata, and caches.

Review the patterns before copying a template: the defaults intentionally exclude items such as lock files and images, which some projects should commit.

### EditorConfig

`.editorconfig` sets UTF-8 and LF defaults, final newlines, trailing-whitespace behavior, and indentation for Python, web/config files, Markdown, Makefiles, and shell scripts.

## Repository layout

```text
.agents/skills/                 Nine explicitly invoked workflow skills
  generate-latex-document/     Includes a template and two workflow references
.cursor/rules/                 Always-applied Cursor coding guideline
ignore/                        Git, Claude Code, and Cursor ignore templates
.editorconfig                  Shared editor formatting
LICENSE                        MIT license
README.md                      English project overview
README_zh.md                   Chinese project overview
```

This repository contains configuration and Markdown/LaTeX resources rather than an executable application, so it has no package installation, build, or automated test command.

## License

Licensed under the [MIT License](LICENSE). Copyright (c) 2026 DreamCasterZero.
