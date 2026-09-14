---
name: run-self-feedback
description: Reviews how YOU performed on your own recorded calls and writes candid, quote-backed self-feedback — 2 things you did well, top 3 things to improve, each with a verbatim quote from the transcript, plus technical notes when a claim the user made doesn't hold up. Pulls raw transcripts from Granola. Use whenever the user asks for feedback on their calls, a weekly call review, "how did I do on that call", "review my sales/coaching/client calls", "what should I improve on calls", "run self-feedback", or wants a recurring call-performance review — even if they only say "review my week" and recent meetings exist.
---

# Run Self-Feedback

Give a consultant, coach, or founder honest feedback on how *they* showed up on their own calls. The subject is always the user's behavior — how they listened, asked, advised, priced, steered, and closed — never the client's problems or the content of the deal.

One exception: technical soundness. If the user asserted something that isn't correct, say so and say what is correct. Advice delivered well is still bad advice if it's wrong, and nobody else on the call is going to check it. This is the only place the review touches content, and it covers what the user claimed, never what the client claimed.

The feedback is only useful if it's grounded. Every observation must be backed by something the user actually said, quoted verbatim from a transcript. If you can't find a quote for a point, drop the point.

## Workflow

### 1. Get the raw transcripts

Work from **verbatim transcripts**, not AI meeting summaries. Summaries capture what was decided; they erase *how* it was said — the hedges, interruptions, "say that again", the think-aloud before a recommendation.

- Use Granola: `list_meetings` for the window (default: the past 7 days, or whatever the user asks for), then `get_meeting_transcript` for each call. Use meeting summaries only to triage which calls to include, never as the thing you analyze.
- If Granola isn't connected, or a call wasn't recorded there, ask the user to paste the transcript or point to a file.
- Long transcripts may be truncated in tool output. If so, save them to files and read them in full. Never analyze a call you only half-read.
- If there are no calls in the window, say so and stop. Don't invent examples.

### 2. Sort each call into a bucket and skip the ones that don't count

Read `references/dimensions.md` first — it defines the buckets and what to look for in each.

- **Sales** — prospects who aren't paying yet: intro/discovery, proposal, pricing, follow-ups.
- **Client** — paying work: advisory, coaching, project check-ins, team meetings the user runs or attends as the expert.
- **Peer** — accountability partners, masterminds, peer groups, mentoring, co-planning, networking that isn't a pitch.

Skip, but list as "not reviewed": calls where the user was mostly a passive attendee (webinars, large groups where they barely spoke) and anything personal or non-work. For personal calls, name only the title and "personal" — don't summarize their contents.

### 3. Analyze — patterns over one-offs

For each call, read with the dimension list open, but don't let it close you off to what it doesn't name. Note moments with the exact quote and who said it. Then look *across* calls:

- A behavior that shows up in three calls usually matters more than a striking one-off. Usually, not always: a single moment that cost the user real money, trust, or standing outranks a tic that recurs.
- **Go looking for what the dimensions don't cover.** They're a floor. The sharpest item in a review is often something specific to this user, this client, this week that no rubric row anticipates. Say it, quote it, and rank it against everything else on equal terms. If every observation you made maps cleanly onto a dimension, read the calls again.
- Count where you can (questions asked before the first recommendation, times the user asked someone to repeat, hedges before a piece of advice). Numbers make the feedback harder to argue with and easier to track next week.
- Check technical soundness: were the claims the user stated as fact actually right? Read the "Technical soundness" section of `references/dimensions.md` for the bar to clear before flagging one, and for what to do when you aren't sure.
- Be candid. The user asked for this; softening it wastes their time. Be kind by being specific and by explaining *why* something worked or didn't.

### 4. Write the review

Use the template in `references/output-template.md` exactly. The shape is deliberate:

- **2 things done well** and **top 3 things to improve**. Not more, not fewer. Forcing the cut makes you pick the highest-leverage items.
- Every item has a **direct quote** from a call. Paraphrase only when the transcript is garbled, and say so.
- **Bullets, short plain sentences.** The user reads this in five minutes, probably on a phone. No paragraphs, no jargon, no filler adverbs.
- Explain *why* a strength worked and *what to try instead* for each improvement. An observation without a mechanism isn't actionable.
- **Technical notes** only when a claim didn't hold up. Leave the section out entirely when everything checked out. Never pad it.
- End with 1–2 goals for next week that are observable in a transcript ("ask three open questions before describing a service"), each with one line on how they'll know it worked.

See `references/example-output.md` for what a finished review looks like. It's there for shape and density only — the findings in it belong to one specific week and should never be reused.

### 5. Deliver

- If a docs tool is available (Google Drive, Notion, etc.), create a document titled `YYYY-MM-DD-Weekly Call Feedback`. With Google Drive, use `create_file` with `contentMimeType: text/html` so headings and bullets render. Otherwise write a Markdown file with the same name.
- In the reply: one line naming the top strength, one line naming the top improvement, and the link. Don't restate the doc.
- Never paste transcripts into the review.

## Running it weekly

This skill works best as a recurring review: same day each week, same window. If the agent supports scheduled tasks, set one up with a prompt like: "Run self-feedback on my calls from the past 7 days and save the review as a doc."

## Things that make this go wrong

- **Analyzing the summary instead of the transcript.** You'll end up praising decisions and missing delivery. Always fetch the verbatim text.
- **Reviewing the client.** "The team lacks a labeling process" is about them. "You gave the labeling recommendation before asking what they'd tried" is about the user.
- **Unquoted claims.** "You tend to over-explain" with no quote reads as an opinion. With the quote it reads as evidence.
- **Padding the strengths.** Strengths matter as much as critiques, but only if they're real and specific. "Good rapport" with no example is filler.
- **Filling in the form.** The dimension list is a starting point, not the assignment. When every finding in a review happens to match a rubric row, the rubric did the reading. The observation the user couldn't have predicted is worth more than the one they could.
- **Nitpicking in the technical notes.** Loose terminology, a simplification made for the audience, and a judgment call you'd have made differently are not errors. Flag a claim when it's both wrong and load-bearing.
- **Ten small notes instead of three big ones.** Combine related observations into one pattern. Leave the rest out.
