# Sunbeam Skills

Skills that help AI agents run an independent consulting or coaching practice.

First skill:
**run-self-feedback** reads your call transcripts and gives you feedback on how you're doing. Use this to grow and become more self-aware as a consultant.

## Why a skill for this

Most of the leverage in a consulting practice is in *how* you show up: how many questions you ask before you recommend something, whether you state your price plainly, whether the call ends with a dated next step. None of that is visible in a meeting summary. It's only in the transcript, and nobody re-reads their own transcripts or has a manager giving them active feedback. 


## Installation

Install with [npx skills](https://github.com/vercel-labs/skills):

```bash
npx skills add dianamp/sunbeam-skills
```

Install one skill only:

```bash
npx skills add dianamp/sunbeam-skills --skill run-self-feedback
```

Check for updates:

```bash
npx skills check
npx skills update
```

Claude Code users can also install it as a plugin:

```
/plugin marketplace add dianamp/sunbeam-skills
/plugin install sunbeam@sunbeam-skills
```

Or copy a skill folder straight into `~/.claude/skills/` (or your agent's equivalent).

## Available skills

| Skill | What it does |
|-------|-------------|
| run-self-feedback | Reviews how you performed on your own recorded calls and writes a weekly review: 2 strengths, top 3 improvements, technical notes, goals for next week |

## The run-self-feedback skill

It needs verbatim transcripts. It's built around [Granola](https://www.granola.ai) and expects a Granola connection that exposes full transcripts, not just AI summaries.

Given a window (default: the past 7 days), the agent:

1. Pulls every transcript in the window and sorts each call into **sales**, **client**, or **peer**. Passive-attendee and personal calls are listed but not reviewed.
2. Reads each transcript against a set of dimensions that fit the call type — talk/listen share, questions before answers, hedging, recommendation-first, presence, next steps with owners, technical soundness on technical calls, and about twenty more (see [`dimensions.md`](skills/run-self-feedback/references/dimensions.md)). Benchmarks come from conversation-intelligence research and the ICF coaching competencies.
3. Looks *across* calls for patterns and counts them. A hedge that shows up in four calls outranks a single long monologue.
4. Writes the review using a fixed template: 2 things you did well, top 3 things to improve, 1–2 goals for next week that are observable in a transcript. Every item carries a direct quote. On technical calls, if the user asserted something that doesn't hold up, a technical notes section says what's wrong and what's actually true. Non-technical weeks don't get that section. The whole thing reads in about five minutes.

It saves the review as a Google Doc when Drive is connected, otherwise as a Markdown file, and replies with one line on the top strength and one on the top improvement.

Once installed:

```
Run self-feedback on my calls from this week.
```

It's meant to run weekly. Set it up as a scheduled task in your agent if it supports one.

## Write your own skills

The dimensions in `references/dimensions.md` are general. Your practice has its own rubric for the kind of feedback you'd like. Fork the skill and add them.

## License

MIT.
