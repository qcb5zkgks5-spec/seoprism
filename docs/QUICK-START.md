# SEO Prism Quick Start Guide

Set up your own SEO Prism knowledge base in about 20 minutes.

## Prerequisites

- **Claude Code** — [claude.ai/claude-code](https://claude.ai/claude-code) (requires Pro, Max, Team, or Enterprise subscription)
- **Obsidian** — [obsidian.md](https://obsidian.md) (free, optional but recommended)
- **Google Search Console** — verified for your site(s)
- **Google Analytics** — configured for your site(s)
- **Bing Webmaster Tools** — [bing.com/webmasters](https://www.bing.com/webmasters) (free)

## Setup

### 1. Create your project folder

```bash
mkdir SEOPrism
cd SEOPrism
```

### 2. Launch Claude Code

```bash
claude
```

### 3. Initialize the knowledge base

Copy the full text of [Karpathy's LLM Wiki paper](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) and paste it into Claude Code. Append this at the end:

> You are now my LLM Wiki agent for SEO analysis. Implement this exact idea file as my persistent knowledge base for tracking search performance across my websites. Guide me step-by-step: create the CLAUDE.md schema file with full rules for SEO data ingestion, set up index.md and log.md, define folder conventions, and show me the first ingest example. From now on, every interaction follows the schema.

Claude builds everything: `CLAUDE.md`, `raw/`, `wiki/`, index, log, overview.

### 4. Open in Obsidian

Open the project folder as an Obsidian vault. Pin `wiki/index.md`. This is your visual browser.

## Weekly Data Cycle

### Export your data

| Source | Steps | Format |
|--------|-------|--------|
| **Google Search Console** | Performance → Search results → Last 28 days → Export → Download Excel | XLSX |
| **Google Analytics** | Reports → Reports Snapshot → Share → Download CSV | CSV |
| **Bing Webmaster Tools** | Search Performance → Set date range → Export | CSV |
| **Bing AI Performance** | AI Performance (Beta) → Download | CSV |

### Name your files

| Source | Naming Convention |
|--------|------------------|
| GSC | Keep default name (auto-includes domain and date) |
| GA | `Reports_snapshot_{site}_{date}.csv` or keep default |
| Bing | `bing_{site}_performance_{date}.csv` |
| Bing AI | `bing_{site}_ai_performance_{date}.csv` |

**Site abbreviations** — use short codes for your sites (e.g., `hvd`, `spl`, `dgl`).

### Drop and ingest

1. Move all export files to `raw/`
2. Open Claude Code in your project directory
3. Tell Claude: **"Ingest all new files in raw/"**

Claude will:
- Read each file
- Create or update source summary pages
- Compare against previous week's baseline
- Update entity pages for each site
- Cross-reference across sites and data sources
- Update the index and log
- Flag anything unusual

### Ask anything

After ingestion, your knowledge base is current. Ask Claude:

- "Which site has the best CTR trend?"
- "Compare my Google vs Bing positions for the same queries"
- "What's the biggest change from last week?"
- "What patterns from my best site should I propagate to the others?"
- "What's the biggest risk to my traffic right now?"

### Browse in Obsidian

Refresh Obsidian to see updated pages. Use the graph view to visualize connections. Click through wikilinks to explore relationships between sites, queries, and analyses.

## Tips

- **Weekly cadence works best.** GSC and GA data has a 2-3 day reporting lag. Export on Sunday/Monday for the cleanest data.
- **Multiple sites multiply the value.** Single-site tracking is useful. Multi-site comparison is where SEO Prism shines — patterns visible across sites that aren't visible in isolation.
- **Let Claude find the story.** Don't just ask for numbers. Ask "what's the most important thing in this week's data?" The KB has context you don't.
- **Save valuable queries as wiki pages.** If Claude produces an analysis worth keeping, tell it to file it in `wiki/analyses/`. Ephemeral chat is lost; wiki pages compound.
- **Lint periodically.** Once a month, ask Claude to health-check the wiki: contradictions, stale data, orphan pages, missing cross-references.

## Next Steps

- **Mission Control Dashboard** — A visual dashboard for your SEO Prism data. Available to [Patreon supporters](https://patreon.com/ThePracticalAIShift).
- **Production CLAUDE.md Schema** — The exact rules file used in the SEO Prism project. Available on [Patreon](https://patreon.com/ThePracticalAIShift).
- **Watch the journey** — [The Practical AI Shift on YouTube](https://www.youtube.com/@ThePracticalAIShift)
