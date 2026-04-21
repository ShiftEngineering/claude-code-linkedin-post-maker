# LinkedIn Post Maker

A multi-agent Claude Code pipeline that turns a topic or rough draft into a polished, human-sounding LinkedIn post. It researches the topic, writes 3 variants, critiques them, humanizes them, and picks the best one — all automatically.

## What it does

You give it a topic. It gives you a ready-to-post LinkedIn post.

Behind the scenes, 5 specialized AI agents run in sequence:

1. **Researcher** — fetches any URLs you provide, then searches the web for supporting stats, news, and industry examples
2. **Writer** — writes 3 post variants: short & punchy, story-led, and contrarian
3. **Skeptic** — critiques each variant for buzzwords, vague claims, and AI-sounding patterns
4. **Humanizer** — rewrites each variant using the critique to make it sound like a real person
5. **Judge** — scores all 3 humanized variants and picks the winner

The full session (research, variants, critiques, scorecard, winning post) is saved to `posts/` as a markdown file.

## Requirements

- [Claude Code](https://claude.ai/code) — the CLI tool from Anthropic

## Setup

**1. Clone or copy this directory** to your local machine.

**2. Customize `config.md` for your voice.** Open `config.md` in the project root and update it with your details. This is the only file you need to change — the agents read it automatically.

```
config.md
├── About You       — your name, role, company, website
├── What You Do     — one-line description of your work
├── Your Audience   — who reads your posts and what they care about
├── Your Voice      — how you write: tone, style, what to avoid
└── Topics          — the subjects you post about
```

**3. Open the project in Claude Code:**

```bash
cd linkedin-post-maker
claude
```

## Usage

Run the `/linkedin-post` command followed by your topic:

```
/linkedin-post why most AI pilots in banking never reach production
```

Pass a URL and the researcher will read it as the primary source:

```
/linkedin-post https://example.com/article-about-ai-in-banking
```

Or hand it a rough draft to refine:

```
/linkedin-post I want to write about how we helped a regional bank cut their loan review time in half using AI agents. Here's a rough draft: [paste draft]
```

The pipeline runs automatically. When it's done, you'll see:
- The **winning post** ready to copy and paste
- The **runner-up** in case you prefer it
- A one-line reason why the winner was chosen

The full session is saved to `posts/YYYY-MM-DD-topic-slug.md`.

## Tips

- **Be specific with your topic.** "AI in banking" is too broad. "Why AI agents are better than RPA for back-office ops" gives the researcher something to work with.
- **Pass a URL to anchor the post.** If there's an article, report, or announcement you want to respond to, include the URL. The researcher reads it first and uses it as the primary source.
- **Share real context if you have it.** If you have a real story, stat, or client observation, include it in your prompt. The agents are instructed never to fabricate anecdotes — so real material makes the post stronger.
- **Check the runner-up.** Sometimes it's actually better for your specific situation.
- **The full session file is useful.** It contains the research brief, all 3 variants, and the critique — good raw material if you want to manually tweak the winning post.

## Project structure

```
linkedin-post-maker/
├── .claude/
│   ├── agents/          # The 6 specialist agent definitions
│   └── commands/        # The /linkedin-post slash command
├── posts/               # Generated posts (one file per run)
├── config.md            # Your author config — edit this to customize the pipeline
└── CLAUDE.md            # Project instructions for Claude Code
```
