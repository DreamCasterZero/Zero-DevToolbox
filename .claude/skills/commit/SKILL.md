---
name: commit
description: 自动生成中文 git commit 信息并提交推送。读取当前改动，用简洁的中文一句话概括改动内容，然后自动执行 git add、commit、push。当用户说"提交""commit""提交代码""推送"时使用。
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*), Bash(git branch:*)
---

# 自动 commit 并 push

读取当前 git 改动，生成简洁的中文 commit 信息，然后自动提交并推送。

## 执行步骤

### 1. 查看当前状态

先了解仓库当前情况：

```bash
git status
git diff --stat        # 看改动了哪些文件、改动量
git diff               # 看未暂存的具体改动
git diff --staged      # 看已暂存的具体改动
git log --oneline -5   # 看最近几次提交风格，保持一致
```

### 2. 分析改动

基于 diff 内容，理解这次改动**实际做了什么**：

- 新增了什么功能/文件
- 修改/修复了什么
- 删除/重构了什么
- 是文档、配置还是代码改动

**不要凭文件名猜测，要看实际 diff 内容。**

### 3. 生成 commit 信息

要求：

- **中文**，简洁，**一句话**概括这次改动的核心内容
- **不要前缀**（不用 feat/fix/docs 这种 Conventional Commits 前缀）
- 直接描述做了什么，动词开头，如"添加 ALNS 自适应大邻域搜索算法"、"修复 POX 交叉中的索引越界问题"、"重构 FJSP 解码逻辑去掉 AGV 部分"
- 如果一次改动包含多个不相关的事情，提示用户是否要分开提交（但默认仍按一条处理）
- 长度控制在一行能看完，不写冗长描述

### 4. 自动提交并推送

确认 commit 信息后，依次执行：

```bash
git add -A                          # 暂存所有改动
git commit -m "生成的中文commit信息"
git push                            # 推送到当前分支的远程
```

### 5. 处理常见情况

- **没有改动**：如果 `git status` 显示没有改动，告知用户无需提交，停止
- **push 失败**：
  - 如果是因为远程有新提交（需要先 pull），告知用户，建议先 `git pull` 或 `git pull --rebase`，**不要自动强推**
  - 如果是没有配置远程或没有 upstream 分支，提示用户，给出 `git push -u origin <分支名>` 的建议命令
  - 如果是认证问题，告知用户检查凭证
- **当前在重要分支**（如 main/master）：正常执行，但在输出里提示一下当前分支名，让用户心里有数

### 6. 输出

完成后简要报告：

- 生成的 commit 信息
- 提交到了哪个分支
- push 是否成功

## 注意事项

- commit 信息必须如实反映 diff 内容，不编造
- push 失败时不要用 `--force` 强推，交给用户决定
- 如果改动很大很杂，主动提示用户考虑拆分提交，但不强制
