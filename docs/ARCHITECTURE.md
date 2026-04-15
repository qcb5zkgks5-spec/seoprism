# SEO Prism Architecture

## System Overview

```mermaid
flowchart LR
    subgraph INPUT["Weekly Data Exports"]
        GSC["Google Search Console\n(XLSX)"]
        GA["Google Analytics\n(CSV)"]
        BING["Bing Webmaster Tools\n(CSV)"]
        AI_PERF["Bing AI Performance\n(CSV, Beta)"]
        YT["YouTube Analytics\n(CSV)"]
    end

    subgraph RAW["raw/ (Immutable)"]
        FILES["Export files\nDrop here, never modify"]
    end

    subgraph WIKI["wiki/ (AI-Maintained)"]
        direction TB
        SCHEMA["CLAUDE.md\n(Schema & Rules)"]
        IDX["index.md\n(Content Catalog)"]
        SRC["sources/\n(One page per export)"]
        ENT["entities/\n(One page per site)"]
        CON["concepts/\n(Methodology)"]
        ANA["analyses/\n(Cross-site comparisons)"]
    end

    subgraph INTERFACES["How You Interact"]
        OBS["Obsidian\nBrowse + Graph View"]
        CC["Claude Code\nAsk Anything"]
        MC["Mission Control\nDashboard"]
    end

    INPUT --> RAW
    RAW --> |"Claude ingests"| WIKI
    WIKI --> OBS
    WIKI --> CC
    RAW --> |"Parsers read directly"| MC
```

## Data Flow

```mermaid
sequenceDiagram
    participant User
    participant Raw as raw/ folder
    participant Claude as Claude Code
    participant Wiki as wiki/ pages
    participant MC as Mission Control

    Note over User: Weekly export cycle
    User->>Raw: Drop GSC/GA/Bing exports
    User->>Claude: "Ingest new files in raw/"

    Claude->>Raw: Read export files
    Claude->>Wiki: Create/update source summary
    Claude->>Wiki: Update entity pages (per site)
    Claude->>Wiki: Cross-reference with existing data
    Claude->>Wiki: Update analyses (comparisons)
    Claude->>Wiki: Update index.md + log.md
    Claude->>User: Report findings + flag anomalies

    User->>MC: Refresh browser
    MC->>Raw: Read export files directly
    MC->>MC: Render charts + comparisons

    Note over User: Query anytime
    User->>Claude: "Compare Google vs Bing positions"
    Claude->>Wiki: Read relevant pages
    Claude->>User: Answer with citations
```

## Folder Structure

```
your-project/
├── CLAUDE.md                    # Schema — rules for the AI
├── raw/                         # Immutable source data
│   ├── *-Performance-*.xlsx     # GSC exports
│   ├── Reports_snapshot*.csv    # GA exports
│   ├── bing_*_performance_*.csv # Bing exports
│   └── bing_*_ai_performance_*.csv
├── wiki/                        # AI-maintained wiki
│   ├── index.md                 # Content catalog
│   ├── log.md                   # Operation history
│   ├── overview.md              # High-level synthesis
│   ├── sources/                 # One page per data export
│   ├── entities/                # One page per site
│   ├── concepts/                # Methodology pages
│   └── analyses/                # Cross-site comparisons
└── mission-control/             # Optional dashboard
    ├── backend/                 # FastAPI (Python)
    │   ├── main.py
    │   ├── parsers/
    │   │   ├── gsc_parser.py
    │   │   ├── ga_parser.py
    │   │   └── bing_parser.py
    │   └── data/
    │       └── projects.json    # Kanban state
    └── frontend/                # React + Vite
        └── src/
            └── pages/
                ├── Portfolio.jsx
                ├── TrafficSources.jsx
                ├── PrismView.jsx
                ├── SiteDetail.jsx
                └── Projects.jsx
```

## The Prism Metaphor

Like a prism splits white light into a spectrum of colors, SEO Prism splits your site's search data into its component sources — revealing the full picture that no single tool shows.

```mermaid
graph LR
    SITE["Your Site's\nSearch Data"] --> PRISM["SEO\nPrism"]
    PRISM --> G["Google\nPosition & Traffic"]
    PRISM --> B["Bing\nPosition & Traffic"]
    PRISM --> DDG["DuckDuckGo\nTraffic via Bing Index"]
    PRISM --> Y["Yahoo\nTraffic via Bing Index"]
    PRISM --> AI["AI Search\nChatGPT · Copilot · Perplexity"]
    PRISM --> SOCIAL["Social & Referral\nFacebook · Reddit · Cross-site"]

    style PRISM fill:#818cf8,color:#fff,stroke:#818cf8
    style G fill:#4285f4,color:#fff
    style B fill:#00897b,color:#fff
    style DDG fill:#de5833,color:#fff
    style Y fill:#7b1fa2,color:#fff
    style AI fill:#10a37f,color:#fff
    style SOCIAL fill:#f97316,color:#fff
```

## Key Design Decisions

| Decision | Rationale |
|----------|-----------|
| **Markdown, not a database** | Human-readable, version-controlled, portable. Works with Obsidian. No setup. |
| **AI maintains the wiki** | Humans are bad at cross-referencing and bookkeeping. LLMs don't get bored or forget to update a page. |
| **Raw data is immutable** | Source of truth never changes. The wiki interprets; it doesn't alter. |
| **Ingest-time synthesis** | Cross-references are built when data arrives, not re-derived on every query. Cheaper and more reliable than RAG. |
| **Local-first** | No cloud services, no API keys for the KB itself, no subscription beyond Claude Code. Your data stays on your machine. |
| **Dashboard reads raw/** | Mission Control doesn't duplicate data. It reads the same files the KB uses. One source of truth. |
