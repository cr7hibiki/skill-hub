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

### Memory Feature: Remember Last Vault

**When the skill loads:**
1. First check if a vault path was previously saved in the `llm-wiki-memory.json` file in this skill directory
2. If a vault path exists **AND** the vault still exists (`.obsidian/` folder found), add an extra option to the menu: `0. 📂 Open last vault: [vault-path]`
3. If the saved path **no longer exists**, automatically clear the expired memory and show the normal menu (no extra option)
4. This provides one-click access for returning users

### Show Interactive Menu

WHEN THIS SKILL LOADS, ALWAYS START BY SHOWING THIS MENU:

If no vault saved:
```
🧠 Welcome to LLM Wiki Pattern!

What would you like to do?

1. 🆕 Create a new Obsidian vault
2. 📂 Open an existing Obsidian vault
3. 📖 Learn more about what this skill can do
4. ❓ Just ask a question
5. 👋 Exit / Do something else
```

If vault saved (and still exists):
```
🧠 Welcome to LLM Wiki Pattern!

What would you like to do?

0. 📂 Open last vault: [saved-path]
1. 🆕 Create a new Obsidian vault
2. 📂 Open an existing Obsidian vault
3. 📖 Learn more about what this skill can do
4. ❓ Just ask a question
5. 👋 Exit / Do something else
```

Then ask the user to pick an option.

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
3. Create directory structure:
   ```
   [vault]/
   ├── .obsidian/ (if not exists)
   ├── Attachments/
   └── LLM-Wiki/
       ├── Notes/
       ├── Concepts/
       ├── HELP.md
       ├── Index.md
       ├── Schema.md
       └── ChangeLog.md
   ```
4. Create and initialize all 4 core files using the templates provided
5. **Save the full vault path** to `llm-wiki-memory.json` in this skill directory for future quick access
6. Show the "What's Next" menu

The memory file format:
```json
{
  "last_vault_path": "/full/path/to/vault",
  "last_vault_name": "vault-name",
  "last_opened": "ISO-8601-date"
}
```

### Option 0: Open Last Vault (from memory)

1. Use the saved path from `llm-wiki-memory.json
2. Verify the vault still exists
3. Load it directly - no need to ask for path again
4. Show current status and "What's Next" menu

### Option 2: Open Existing Vault

1. Ask for vault path (user can paste full path from Obsidian)
2. Check for `.obsidian/` folder to confirm this is really an Obsidian vault
3. Look for existing `LLM-Wiki/` folder structure
4. If found:
   - Count existing notes/concepts
   - Show status: "Found LLM-Wiki with X notes and Y concepts"
   - Save the full vault path to `llm-wiki-memory.json`
   - Show "What's Next" menu
5. If not found:
   - Offer: "This is an Obsidian vault but doesn't have LLM-Wiki structure yet. Shall I initialize it?"
   - If user agrees, create the full structure and initialize all core files
   - Save path to memory after initialization
   - Show "What's Next" menu

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
   - 🤖 Auto-detect (recommended - I'll figure it out)
   - URL (web page, YouTube, etc.)
   - Text/paste content
   - Topic (create from scratch)
   - File (PDF, doc, etc.)
   
   **If user chooses Auto-detect:** Just ask them to provide the content/URL/text, and you automatically determine the best way to process it.

2. Process and identify key concepts
3. Determine target file path (LLM-Wiki/Notes/ or LLM-Wiki/Concepts/)
4. **Check for conflicts**: If a file with the same name already exists:
   - Ask user: "A page named 'X' already exists. Would you like to (O)verwrite, (R)ename, or (C)ancel?"
   - Respect the user's choice
5. Show a preview of what will be created
6. Confirm before writing
7. After writing, update Index.md (if needed) and log entry in ChangeLog.md

### 2. Query (Answer Questions)

**Interactive Flow:**
1. Load Index.md and scan for relevant pages
2. Synthesize answer from existing wiki content
3. Show the answer to the user
4. If the answer is comprehensive and good:
   - "This comprehensive answer would make a great wiki page! Want me to save it to your wiki?"
   - If user confirms:
     - Save to `LLM-Wiki/Notes/` as a new page
     - Add to Index and log in ChangeLog
5. **Always log the query** in ChangeLog.md even if you don't save the full answer

**Best Practice:** Save answers that are likely to be useful again in the future - this builds your compounding knowledge!

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
2. Explore the Graph View in Obsidian to see knowledge connections
3. **Install the Dataview plugin** for dynamic tables on the [[Index]] page
4. See [[Schema]] for this wiki's structure and naming conventions
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

### LLM-Wiki/Schema.md (Configuration & Conventions)

```markdown
---
tags: [schema, llm-wiki]
---

# 📐 LLM Wiki Schema & Conventions

This file defines the structure and naming conventions for your LLM Wiki.

## Folder Organization

| Folder | Purpose | Content Type |
|--------|---------|--------------|
| **LLM-Wiki/Notes/** | Full-length articles and notes | Processed sources, comprehensive topics, detailed explanations |
| **LLM-Wiki/Concepts/** | Atomic concept definitions | Short definitions of terms, ideas, people, technologies |
| **LLM-Wiki/Attachments/** | Raw sources | Original unmodified content, PDFs, screenshots |

## When to use which?

- **Notes**: "What is X? How does it work? What have I learned about it?" - full coverage of a topic
- **Concepts**: "What does X mean?" - one-paragraph definition for quick reference

## Naming Conventions

- Use human-readable titles: `Machine Learning.md` not `machine-learning.md`
- Spaces are fine in Obsidian - keep it readable
- For duplicates: add context: `Transformer (Deep Learning).md`, `Transformer (Cryptography).md`

## Tagging Conventions

- Use lowercase hyphenated tags: `machine-learning`, `programming/go`, `book-notes`
- Every page should have at least one topic tag
- Core system tags are reserved: `llm-wiki`, `help`, `index`, `schema`, `changelog`

## Linking Style

- Use [[WikiLinks]] for internal links between concepts
- Link to concepts when they are first mentioned
- Add backlinks to related topics
- Don't over-link - only link when it adds value

## YAML Frontmatter

Every page should have frontmatter:

```yaml
---
title: [Page Title]
tags: [tag1, tag2]
created: [YYYY-MM-DD]
source: [URL or description of source]
---
```

## Metadata Best Practices

- Always include `source` when ingesting from external content
- Always include `created` date for tracking knowledge growth
- Keep tags focused (2-5 tags per page is ideal)
```

### LLM-Wiki/ChangeLog.md

```markdown
---
tags: [changelog, llm-wiki]
---

# 📋 LLM Wiki Change Log

## 2024-01-01

> [!success] 14:30
> Vault initialized! Welcome to your LLM Wiki. 🎉
>
> Created:
> - [[HELP]] - How to use this wiki
> - [[Index]] - This page
> - [[Schema]] - Configuration
```

**Date format:** Use `YYYY-MM-DD` for dates (e.g., `2024-03-15`). Time is optional but recommended in `HH:MM` 24-hour format.

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
- **Persistent memory**: After first use, the vault path is saved in `llm-wiki-memory.json`
- **One-click access**: Next time you use the skill, you can directly open the last vault without retyping the path
- **Ask**: "Should I create it in the default Obsidian folder, or somewhere else?"

### After Each Action

Show a "What's next?" menu:

```
✅ Done! What would you like to do now?

1. 📥 Ingest something else
2. ❓ Ask a question about your wiki
3. 🔍 Check wiki health
4. 🏠 Return to main menu
5. 👋 Exit / Do something else
```

Option 4 returns to the initial interactive menu (for switching vaults, etc.)

---

## 💾 Memory Management

The skill persists the last used vault path in `skills/llm-wiki-pattern/llm-wiki-memory.json`. This enables:

- **One-click access** when returning to your wiki
- **No need to re-type** the full path every time
- **Auto-switch**: Opening a different vault automatically updates the saved path
- **To forget/switch**: Just select "Open an existing Obsidian vault" and enter a new path - the memory will update automatically

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

---

## 🌟 Example Usage Scenarios

### Scenario 1: Learning a New Programming Topic

**User:** "I want to learn about React hooks. Can you help me build a knowledge base?"

**Flow:**
1. Skill shows main menu → user chooses "Create a new Obsidian vault"
2. User names vault "React-Learning"
3. Skill creates vault structure at `C:\Users\[name]\Obsidian\React-Learning`
4. User says: "Ingest this article: https://react.dev/learn/rules-of-hooks"
5. Skill processes the article, identifies key concepts:
   - [[Rules of Hooks]] (concept)
   - [[useState Hook]] (concept)
   - [[useEffect Hook]] (concept)
   - "React Hooks Rules" (note with full article)
6. Shows preview, confirms, creates files
7. Updates Index and ChangeLog

### Scenario 2: Researching for a Paper

**User:** "I need to organize my research papers on machine learning."

**Flow:**
1. Skill shows main menu with "Open last vault" option (from memory)
2. User opens existing "ML-Research" vault
3. User says: "Here's a PDF I saved - can you ingest it?"
4. Skill: "What type of source is this? (🤖 Auto-detect / URL / Text / Topic / File)"
5. User chooses "Auto-detect"
6. Skill processes PDF, creates:
   - [[Attention Is All You Need]] (note with paper summary)
   - [[Transformer Architecture]] (concept)
   - [[Self-Attention]] (concept)
7. Asks: "This comprehensive answer would make a great wiki page! Want me to save it?"

### Scenario 3: Quick Question from Existing Knowledge

**User:** "What do I know about transformers?"

**Flow:**
1. Skill loads Index.md and scans vault
2. Finds: [[Transformer Architecture]], [[Self-Attention]], [[Attention Is All You Need]]
3. Synthesizes answer from existing content
4. Asks: "Want me to save this synthesis as a new note?"
5. Logs the query in ChangeLog even if not saved

### Scenario 4: Wiki Health Check

**User:** "Can you check my wiki for issues?"

**Flow:**
1. Skill runs Lint/Health Check
2. Checks for:
   - Broken [[WikiLinks]]
   - Orphaned pages (no incoming links)
   - Missing YAML frontmatter
3. Creates a health report note with actionable items
4. Shows "What's next?" menu
