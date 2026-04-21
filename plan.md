# Pipeline Design Plan

## Phase 1: Interactive (current)
Run the full 5-agent pipeline within a Claude Code conversation using the Agent tool.
Each agent is a subagent with a focused prompt and specific tools.

## Agent Specs

### 1. Researcher
- Tools: WebSearch (Brave), WebFetch (Firecrawl)
- Input: topic string
- Output: structured research brief (key stats, recent news, relevant examples, contrarian takes)
- Constraint: only use sources from last 12 months where possible

### 2. Writer
- Tools: none (uses research brief)
- Input: topic + research brief + author persona
- Output: 3 post variants
  - Variant A: Short & punchy (hook + 3 lines + CTA), under 150 words
  - Variant B: Story-led (open with a specific moment/observation), 150-250 words
  - Variant C: Insight/contrarian (challenge a common belief), 150-250 words

### 3. Skeptic
- Tools: none
- Input: all 3 variants
- Output: critique of each — what's generic, what's unsupported, what a skeptical finserv exec would push back on

### 4. Humanizer
- Tools: none
- Input: all 3 variants + their critiques
- Output: revised version of each — more personal, specific, imperfect sentences, first-person voice
- Rules: no em-dashes, no "In today's world", no "game-changer", no rhetorical questions as openers

### 5. Judge
- Tools: none
- Input: all 3 humanized variants
- Output: ranked scorecard (resonance, authenticity, clarity, finserv relevance) + winning post

## Phase 2: Slash Command
Create `.claude/commands/linkedin-post.md` for `/linkedin-post <topic>` invocation.

## Phase 3: Refinements (future)
- Tone profile calibration based on saved post history
- Engagement tracking input ("this one did well, learn from it")
- Draft mode (user provides partial draft, pipeline polishes it)
