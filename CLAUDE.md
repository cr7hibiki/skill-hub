# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个 **Claude Code Skill 技能仓库**，托管 `llm-wiki-pattern` 技能。该技能帮助用户构建持久的、复利增长的个人知识库，与 Obsidian 原生集成。

## 仓库结构

```
llm-wiki/
└── skills/
    └── llm-wiki/
        └── SKILL.md     # 技能定义（核心文件，被 Claude Code 系统加载）
```

## 架构说明

### 技能角色
- **SKILL.md**: 包含技能的完整定义：
  - 触发条件：何时应该调用这个技能
  - 交互流程：创建/打开知识库、摄入内容、查询、健康检查
  - 模板：生成 Obsidian vault 需要的各种文件（HELP.md、Index.md、ChangeLog.md 等）
  - 用户体验指南：交互原则

### 文件职责
- `SKILL.md` → **被系统实际执行**：Claude Code 读取这个文件来了解技能该做什么
- `README.md`（可选）→ **仅给人阅读**：项目介绍，不被系统调用

## 常用操作

### 添加/修改技能
1. 编辑 `skills/llm-wiki/SKILL.md` 更新技能定义
2. 提交变更到 Git

### 触发技能（用户端）
当用户说以下话语时会触发该技能：
- "help me build a knowledge base" / "帮我构建一个知识库"
- "organize my notes" / "整理我的笔记"
- "persist information" / "保存信息供以后参考"
- "Obsidian" / "vault" / "个人 wiki"
- "compounding knowledge" / "incremental learning" / "复利知识" / "增量学习"

## 核心工作流程

当技能被触发时，**必须**首先显示交互式菜单：
```
🧠 Welcome to LLM Wiki Pattern!

What would you like to do?

1. 🆕 Create a new Obsidian vault
2. 📂 Open an existing Obsidian vault
3. 📖 Learn more about what this skill can do
4. ❓ Just ask a question
```

然后等待用户选择。

### 三大核心操作
| 操作 | 功能 |
|------|------|
| **Ingest 摄入** | 处理各种来源（URL、文本、文件）→ 结构化 wiki 页面 |
| **Query 查询** | 从现有知识库合成答案 → 可保存好答案回知识库 |
| **Lint 检查** | 健康检查：断开链接、孤立页面、缺少元数据等 |

## 默认位置约定

- **Windows**: `C:\Users\[username]\Obsidian\[vault-name]`
- **Mac/Linux**: `~/Obsidian/[vault-name]`

## Vault 结构（技能生成）

```
[vault-name]/
├── .obsidian/          # Obsidian 配置（自动管理）
├── Attachments/         # 原始来源文件
└── LLM-Wiki/
    ├── HELP.md         # 知识库内帮助
    ├── Schema.md       # 配置和约定
    ├── Index.md        # 主页（含 Dataview 查询）
    ├── ChangeLog.md    # 变更日志
    ├── Notes/          # 主要内容笔记
    └── Concepts/       # 原子概念定义
```
