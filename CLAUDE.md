# LinkedIn Post Maker — Claude Code Project

## Purpose
A multi-agent pipeline that turns a topic or draft into a polished, human-sounding LinkedIn post for Michael Prichard's personal account. Posts target financial services leaders on topics of AI and AI agents.

## Author Context
Defined in `config.md` at the project root. The Manager agent reads this file and passes the author context to all downstream agents. To customize the pipeline for a different author, only `config.md` needs to be updated.

## How to Run
```
/linkedin-post your topic here
```
Or pass a draft and the pipeline will research, critique, humanise, and judge it.

## Agent System (`.claude/agents/`)

| Agent | File | Tools | Role |
|---|---|---|---|
| Manager | `linkedin-manager.md` | Agent, Write, Read | Orchestrates the full pipeline |
| Researcher | `linkedin-researcher.md` | WebSearch, WebFetch | Finds stats, news, finserv examples |
| Writer | `linkedin-writer.md` | — | Generates 3 post variants |
| Skeptic | `linkedin-skeptic.md` | — | Critiques each variant |
| Humanizer | `linkedin-humanizer.md` | — | Rewrites using critique |
| Judge | `linkedin-judge.md` | — | Scores all 3, picks winner |

## Pipeline Flow
```
Input (topic or draft)
        │
        ▼
  [Researcher]  — web search + scrape → research brief
        │
        ▼
  [Writer]      — 3 variants (punchy / story-led / contrarian)
        │
        ▼
  [Skeptic]     — critique of each variant
        │
        ▼
  [Humanizer]   — revised variants using critique
        │
        ▼
  [Judge]       — scorecard → winning post
        │
        ▼
  Saved to posts/YYYY-MM-DD-slug.md
```

## Posts
All generated posts saved to `linkedin-post-maker/posts/` as markdown files.
Each file includes: topic, research brief, all 3 variants, critiques, scorecard, and winning post.

## Status
- [x] All 6 agents created in `.claude/agents/`
- [x] `/linkedin-post` command created in `.claude/commands/`
- [x] `posts/` directory created
- [ ] End-to-end test run completed
