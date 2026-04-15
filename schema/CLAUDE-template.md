# LLM Wiki Schema — SEO Prism Knowledge Base (Template)

This is a starter template for the CLAUDE.md schema file. Customize it for your sites and workflow.

> **Note:** The production schema used in the SEO Prism project is available to [Patreon supporters](https://patreon.com/ThePracticalAIShift). This template gets you started.

## Directory Structure

```
your-project/
  CLAUDE.md          # This file — read first, always
  raw/               # Immutable source documents (exports, reports)
    assets/          # Downloaded images and attachments
  wiki/              # LLM-generated and LLM-maintained markdown pages
    index.md         # Content catalog — every wiki page listed
    log.md           # Chronological record of all operations
    overview.md      # High-level synthesis
    sources/         # One summary page per ingested source
    entities/        # Pages for each website/property
    concepts/        # Pages for methodology, tracking approach
    analyses/        # Comparisons, deep dives, recommendations
```

## Page Conventions

Every wiki page starts with YAML frontmatter:

```yaml
---
title: Page Title
type: source | entity | concept | analysis | overview
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
sources: [source-filename]
---
```

Use `[[Page Title]]` wikilinks for cross-references. Cite sources inline.

## Operations

### Ingest

When a new file is added to `raw/`:
1. Read the source completely
2. Create a summary page in `wiki/sources/`
3. Update or create relevant entity pages
4. Update or create relevant concept/analysis pages
5. Update `wiki/index.md`
6. Update `wiki/overview.md` if the big picture changed
7. Append to `wiki/log.md`

### Query

When answering questions:
1. Read `wiki/index.md` to find relevant pages
2. Read the relevant wiki pages
3. Synthesize an answer with citations
4. If the answer is substantial, offer to file it as a new analysis page

### Lint

When asked to health-check:
- Contradictions between pages
- Stale claims superseded by newer data
- Orphan pages with no inbound links
- Missing cross-references
- Data gaps worth investigating

## Principles

- The wiki is the primary artifact. Chat is ephemeral; the wiki persists.
- Sources are immutable. Never modify anything in `raw/`.
- Compound, don't repeat. Each new source enriches existing pages.
- Flag contradictions explicitly. Don't silently pick a side.
- Stay grounded. Every claim traces back to a source.
- Keep the index and log current. Updated on every operation.
