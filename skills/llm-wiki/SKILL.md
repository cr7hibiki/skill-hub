---
name: llm-wiki-pattern
description: |
  🧠 LLM Wiki Pattern - Build persistent, compounding personal knowledge bases with Obsidian vault integration.
  ALWAYS USE THIS SKILL WHEN:
  - User says "help me build a knowledge base" or "organize my notes"
  - User wants to persist information for later reference
  - User mentions Obsidian, vault, or wants to create interlinked notes
  - User talks about "compounding knowledge", "incremental learning", or "personal wiki"
  - User wants to save good answers for future reuse
  - User has scattered information they want synthesized
  - User asks "what can this skill do?" or "how do I use this?"
  QUICK START: When skill first loads, ALWAYS show the interactive menu!
  DO NOT USE WHEN: Simple one-off Q&A (just answer directly)
---

# 🧠 LLM Wiki Pattern Skill (Obsidian-optimized)

Build persistent, compounding personal knowledge bases with native Obsidian vault integration.

## 🎯 FIRST THING TO DO: Show Interactive Menu

WHEN THIS SKILL LOADS, ALWAYS START BY SHOWING THIS MENU:

```
🧠 Welcome to LLM Wiki Pattern!

What would you like to do?

1. 🆕 Create a new Obsidian vault
2. 📂 Open an existing Obsidian vault
3. 📖 Learn more about what this skill can do
4. ❓ Just ask a question
```

Then ask the user to pick an option (1-4).

---

## 💡 What This Skill Can Do

### 📚 Three Core Operations

| Operation | What it does | Best for |
|-----------|-------------|----------|
| **Ingest** | Process sources into wiki pages | New articles, papers, notes |
| **Query** | Answer from wiki + save good answers | Studying, reviewing |
| **Lint** | Health check your wiki | Regular maintenance |

### 🎪 Example Use Cases

- **Personal Learning**: Track what you learn about ML, programming, etc.
- **Research**: Organize papers and notes for a project
- **Book Notes**: Create a "book companion" wiki as you read
- **Course Notes**: Build a persistent knowledge base from courses
- **Hobby Deep-Dive**: Document your learning about any topic

### 🔗 Obsidian Native Features

- [[WikiLinks]] for connecting ideas
- YAML frontmatter for metadata
- Callouts (`> [!note]`, `> [!tip]`)
- Dataview queries for dynamic indexes
- Canvas support for visual mind maps

---

## 🚀 Quick Start Guide

### Option 1: Create a New Vault

1. Ask user for vault name
2. Suggest default location: `~/Obsidian/[vault-name]`
   - On Windows: `C:\Users\[username]\Obsidian\[vault-name]`
   - On Mac/Linux: `~/Obsidian\[vault-name]`
3. Create structure and initialize core files
4. Show the "What's Next" menu

### Option 2: Open Existing Vault

1. Ask for vault path
2. Check for `.obsidian/` folder to confirm
3. Look for existing `LLM-Wiki/` folder
4. If found, load and show current status
5. If not found, offer to initialize LLM-Wiki structure

### Option 3: Learn More

Show this section of the skill and then return to the main menu.

---

## 📁 Standard Vault Structure

```
[Vault Root]/
├── .obsidian/              # Obsidian config (auto-managed)
├── Attachments/             # Raw, immutable sources
└── LLM-Wiki/
    ├── HELP.md             # 🆕 This skill's guide (in-vault)
    ├── Schema.md           # Configuration and conventions
    ├── Index.md            # 🏠 Starting page + Dataview
    ├── ChangeLog.md        # 📋 Activity log
    ├── Notes/              # Primary content notes
    └── Concepts/           # Atomic concept definitions
```

---

## Core Operations in Detail

### 1. Ingest (Process New Sources)

**Interactive Flow:**
1. Ask what type of source:
   - URL (web page, YouTube, etc.)
   - Text/paste content
   - Topic (create from scratch)
   - File (PDF, doc, etc.)
2. Process and identify key concepts
3. Show a preview of what will be created
4. Confirm before writing
5. Update Index.md and ChangeLog.md

### 2. Query (Answer Questions)

**Interactive Flow:**
1. Load Index.md and scan for relevant pages
2. Synthesize answer from wiki content
3. If answer is good:
   - "This would make a great wiki page! Want me to save it?"
4. Always log the query in ChangeLog.md

### 3. Lint (Health Check)

**Check for:**
- Broken [[WikiLinks]]
- Orphaned pages (no incoming links)
- Missing YAML frontmatter
- Contradictory claims across pages

**Output:** A health report note with actionable items.

---

## 📝 Special Files Templates

### LLM-Wiki/HELP.md (NEW - User Guide in Vault)

Create this file so users have help inside their vault!

```markdown
---
tags: [help, llm-wiki]
---

# 🧠 LLM Wiki Help

Welcome to your LLM Wiki! Here's how to use it.

## What is this?

This is a personal knowledge base built using Andrej Karpathy's LLM Wiki pattern.
- **Raw Sources** → **Structured Wiki** → **Compounding Knowledge**

## How to Use with Claude

Just talk to Claude! Try:
- "Ingest this article: [URL]"
- "What do I know about X?"
- "Check my wiki for issues"

## Folder Structure

- **Notes/** - Main content pages
- **Concepts/** - Atomic definitions
- **Attachments/** - Original sources

## Tips

1. Use [[WikiLinks]] to connect ideas
2. Explore the Graph View in Obsidian!
3. Install Dataview plugin for dynamic queries
```

### LLM-Wiki/Index.md (Enhanced)

```markdown
---
tags: [index, llm-wiki, moc]
---

# 🏠 LLM Wiki Index

> [!tip] Getting Started
> - Add new content by talking to Claude: "Ingest this..."
> - Ask questions: "What do I know about..."
> - Need help? See [[HELP]]

## 📂 Quick Navigation

- [[HELP]] - How to use this wiki
- [[ChangeLog]] - What's changed recently
- [[Schema]] - Wiki structure and conventions

## 📚 Notes

```dataview
TABLE file.tags as "Tags", file.ctime as "Created"
FROM "LLM-Wiki/Notes"
SORT file.ctime DESC
```

## 💡 Concepts

```dataview
TABLE file.tags as "Tags"
FROM "LLM-Wiki/Concepts"
SORT file.name ASC
```

## 🎯 What's Next?

Tell Claude what you want to learn about next!
```

### LLM-Wiki/ChangeLog.md

```markdown
---
tags: [changelog, llm-wiki]
---

# 📋 LLM Wiki Change Log

## [[Date]]

> [!success] [Time]
> Vault initialized! Welcome to your LLM Wiki. 🎉
>
> Created:
> - [[HELP]] - How to use this wiki
> - [[Index]] - This page
> - [[Schema]] - Configuration
```

---

## 🎨 User Experience Guidelines

### Always Be Interactive

- **Never assume**: Ask before creating/modifying
- **Show previews**: "Here's what I plan to create..."
- **Offer choices**: "Would you like A or B?"

### Smart Path Handling

- **Default location**: Use standard Obsidian folder
  - Windows: `C:\Users\[name]\Obsidian\`
  - Mac/Linux: `~/Obsidian/`
- **Remember**: If user has a preferred location, use that!
- **Ask**: "Should I create it in the default Obsidian folder, or somewhere else?"

### After Each Action

Show a "What's next?" menu:

```
✅ Done! What would you like to do now?

1. 📥 Ingest something else
2. ❓ Ask a question about your wiki
3. 🔍 Check wiki health
4. 👋 Take a break
```

---

## Smart Triggering Reminder

**When to use this skill:**
- User wants to PERSIST knowledge
- User mentions Obsidian/vault
- User asks "what can this do?"

**When NOT to use:**
- Simple one-off question → just answer!
- User says "just tell me, don't save it"

**When in doubt:** Ask! "Would you like me to save this to your knowledge base, or just answer?"
