# claude-code-skills

> 🚀 Claude Code 自定义技能集合  
> [🇺🇸 English](./README.md)

Claude Code 自定义技能集合，为 Claude Code 提供专业化工作流和领域能力扩展。

## 可用技能

| 技能 | 描述 |
|-------|-------------|
| **[llm-wiki-pattern](./skills/llm-wiki/)** | 构建持久复利增长的个人知识库，原生支持 Obsidian 集成 |

*更多技能即将加入...*

## 快速开始

### 安装单个技能

通过 [skills CLI](https://skills.sh/) 安装：

```bash
# 只安装 llm-wiki-pattern 技能
npx skills add cr7hibiki/skill-hub --path skills/llm-wiki
```

### 安装所有技能

```bash
# 安装本仓库所有技能
npx skills add cr7hibiki/skill-hub
```

在 Claude Code 对话中，技能会根据上下文自动触发。例如：
> *"帮我用 Obsidian 构建一个个人知识库"*

## 添加技能

每个技能放在 `skills/[名称]/` 目录下，只需要：
- `SKILL.md` - 包含触发规则和工作流的技能定义

## 许可证

MIT
