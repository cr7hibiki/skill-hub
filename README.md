# claude-code-skills

> 🚀 Collection of custom skills for [Claude Code](https://claude.ai/code)  
> [🇨🇳 中文说明](./README.zh-CN.md)

A collection of custom skills that extend Claude Code with specialized workflows and domain-specific capabilities.

## Available Skills

| Skill | Description |
|-------|-------------|
| **[llm-wiki-pattern](./skills/llm-wiki/)** | Build persistent, compounding personal knowledge bases with Obsidian integration |

*More skills coming soon...*

## Quick Start

### Install a single skill

Install via [skills CLI](https://skills.sh/):

```bash
# Install just the llm-wiki-pattern skill
npx skills add cr7hibiki/skill-hub --path skills/llm-wiki
```

### Install all skills

```bash
# Install all skills in this repository
npx skills add cr7hibiki/skill-hub
```

In Claude Code conversations, skills trigger automatically based on context. For example:
> *"Help me build a personal knowledge base with Obsidian"*

## Adding Skills

Each skill lives in `skills/[name]/` and requires only:
- `SKILL.md` - Skill definition with trigger rules and workflow

## License

MIT
