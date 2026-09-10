# Sunbeam Skills

Skills that help AI agents do the unglamorous parts of running an independent consulting or coaching practice.

I'm Diana Pfeil. I run [Sunbeam Consulting](https://sunbeams.ai), an ML advisory and CTO-coaching practice. These skills started as things I built for myself and kept using. They assume you're a solo operator (or a very small team) whose work happens mostly on calls, and that the calls are recorded.

## Why skills for this

Most of the leverage in a consulting practice is in *how* you show up: how many questions you ask before you recommend something, whether you state your price plainly, whether the call ends with a dated next step. None of that is visible in a meeting summary. It's only in the transcript, and nobody re-reads their own transcripts.

An agent will. These skills point it at the raw transcripts and make it report back with evidence.

**run-self-feedback** is the first one. Every week it reads your calls and tells you three things you did well and three things to fix, each backed by a verbatim quote from something you actually said.

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
| run-self-feedback | Reviews how *you* performed on your own recorded calls and writes a quote-backed weekly review: 3 strengths, top 3 improvements, goals for next week |

## The run-self-feedback skill

The skill reviews the user, not the client. "The team has no labeling process" is a note about them. "You gave the labeling recommendation before asking what they'd tried" is a note about you. Only the second kind makes it into the review.

It needs verbatim transcripts. It's built around [Granola](https://www.granola.ai) and expects a Granola connection that exposes full transcripts, not just AI summaries. Summaries record what was decided and erase how it was said, which is the whole point. If a call isn't in Granola, you can paste the transcript.

Given a window (default: the past 7 days), the agent:

1. Pulls every transcript in the window and sorts each call into **sales**, **client**, or **peer**. Passive-attendee and personal calls are listed but not reviewed.
2. Reads each transcript against a set of dimensions that fit the call type — talk/listen share, questions before answers, hedging, recommendation-first, presence, next steps with owners, and about twenty more (see [`dimensions.md`](skills/run-self-feedback/references/dimensions.md)). Benchmarks come from conversation-intelligence research and the ICF coaching competencies.
3. Looks *across* calls for patterns and counts them. A hedge that shows up in four calls outranks a single long monologue.
4. Checks follow-through on commitments from earlier calls and on last week's goals, if a previous review exists.
5. Writes the review using a fixed template: 3 things you did well, top 3 things to improve, open loops, 1–2 goals for next week that are observable in a transcript. Every item carries a direct quote. The whole thing reads in about five minutes.

It saves the review as a Google Doc when Drive is connected, otherwise as a Markdown file, and replies with one line on the top strength and one on the top improvement.

Once installed:

```
Run self-feedback on my calls from this week.
```

It's meant to run weekly. Set it up as a scheduled task in your agent if it supports one, so each week's goals get checked against the next week's transcripts.

## Write your own skills

The dimensions in `references/dimensions.md` are general. Your practice has its own tells — the phrase you use when you're about to under-price, the client who always gets the long version. Fork the skill and add them. The [skill template](https://github.com/anthropics/skills/tree/main/template) in Anthropic's skills repo is a good starting point.

## License

MIT.
