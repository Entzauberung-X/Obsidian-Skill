---
name: "book-note-organizer"
description: Use when the user asks to organize a textbook into notes, summarize book chapters, find missing knowledge points, build a book outline with chapter-note mapping, or create cross-chapter supplementary material for any textbook.
---

# Book Note Organizer

Transform a textbook into an Obsidian note system: one index file (`全书脉络.md`) with a chapter→note lookup table, one note per chapter, one formula quick-reference, and supplementary notes for topics that span multiple chapters.

**Tradeoff:** These rules bias toward completeness over speed. For a single-chapter summary, use judgment.

## Directory & Naming

```
{分类}/{书名}/
├── 全书脉络.md
├── 第N章 {章节名} - 笔记.md    ← one per chapter
├── {书名}全书关键公式整理.md
└── 补充资料/
    └── {专题名}.md              ← cross-chapter topics
```

Frontmatter for every note:
```yaml
---
title: "{标题}"
author: cc
created: {YYYY-MM-DD}
tags: [{domain tags}]
---
```

**Wiki-link rule:** Use the actual filename on disk. If Obsidian auto-prefixed a file (e.g. `3.1、调制解调详解.md`), the link must include that prefix. Never guess — Glob the directory first.

## Behavioral Rules

### 1. Index before content

Before writing any chapter note, create the `全书脉络.md` with a chapter→note lookup table. Every chapter note gets a row. Every supplementary note gets a row. No file exists without a row in the index.

*Prevents: orphan notes with no discovery path.*

### 2. Notes must be reference-able, not just readable

A chapter note is incomplete if it lacks:
- At least one comparison table (方案对比 / 参数对比 / 分类总览)
- At least one formula block
- An "易错点" or "注意事项" section

Prose-only chapter summaries are not acceptable. If you wrote 50 lines of pure prose, you're not done.

*Prevents: notes that feel complete but are useless for review.*

### 3. Multi-chapter concepts get their own note

When a concept requires understanding from 2+ chapters to explain, create a standalone note in `补充资料/`. Five patterns trigger this:

| Pattern | Signal | Example |
|---------|--------|---------|
| Tool chain | ChA theory → ChB needs tool | Transmission line → Smith chart design |
| Metric cascade | Metrics from multiple chapters combine | NF + Gain + IIP₃ → Link budget |
| Tradeoff | Two design goals conflict | Noise match vs power match |
| Principle→circuit | Theory chapter → circuit chapter | Modulation theory → Modulator circuits |
| Noise propagation | Noise through system layers | Leeson model → PLL noise → Receiver SNR |

Each supplement must: name its source chapters in the opening line, link to them, and include one ASCII dependency diagram.

*Prevents: shallow treatment of interconnected concepts by siloing them in separate chapter notes.*

### 4. Every link must resolve

After writing or editing any note, verify: the `参见` section links back to `[[全书脉络]]`, and every wiki-link in the file resolves to an existing file. If a linked file doesn't exist yet, either create it or remove the link.

*Prevents: dead links that break the note network.*

### 5. Read before write, append before overwrite

When a target file already exists: Read it first. If the user asked for a supplement, append. If the user asked for a rewrite, present what you plan to change before executing. Never delete existing content without explicit instruction.

*Prevents: destroying user's accumulated notes.*

### 6. Finish means finish

After creating or updating notes, the `全书脉络.md`'s "配套资料清单" section must reflect the current state. The task is not complete until this table is updated. State what was changed so the next session knows.

*Prevents: index drift where the table says one thing and the files say another.*

### 7. Formulas in table cells: never a raw `|`

Obsidian parses Markdown tables before rendering LaTeX. A bare `|` inside `$...$` in a table cell is treated as a **column separator**, splitting the row into phantom columns (symptom: table column count goes wrong, formula looks cut off).

| Case | ❌ Wrong (in table) | ✅ Right (in table) |
|------|--------------------|--------------------|
| Absolute value | `$\|x\|$` | `$\lvert x\rvert$` |
| Norm | `$\|X\|$` | `$\lVert X\rVert$` |
| Conditional probability | `$P(B\|A)$` | `$P(B\mid A)$` |

Prefer the explicit LaTeX commands (`\mid`, `\lvert...\rvert`, `\lVert...\rVert`) — they are unambiguous in any renderer. `\|` also works *inside Obsidian table cells* (the Markdown layer escapes it to a literal `|` before LaTeX sees it), but avoid it in `$$...$$` display blocks, where LaTeX renders it as the norm symbol `‖`.

*Prevents: table cells splitting into phantom columns whenever a formula contains a pipe.*

## Verification Checklist

After each batch of changes, confirm:

- [ ] `全书脉络.md` 速查表 has a row for every `.md` file in the directory
- [ ] Every chapter note has ≥1 comparison table, ≥1 formula block, and an 易错点 section
- [ ] Every supplement note names its source chapters and includes an ASCII dependency diagram
- [ ] `[[全书脉络]]` appears in the 参见 section of every note
- [ ] Glob confirms every wiki-link target file exists
- [ ] `全书脉络.md` 配套资料清单 is current

**These rules are working if:** no chapter notes are orphaned from the index, supplement notes consistently appear for cross-chapter topics, and wiki-links don't break after file renames.
