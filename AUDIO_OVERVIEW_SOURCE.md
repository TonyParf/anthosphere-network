# Anthosphere Projects Network — Audio Overview Source

> **Use this document as input for NotebookLM Audio Overview.**
> Upload `TZ_v8.md`, `README.md`, and this file together.
> Then in NotebookLM, click **"Customize"** before generating audio and paste
> the **Customization Prompt** below.

---

## Customization Prompt (paste into NotebookLM)

> Generate an 8-minute Audio Overview in **English**, in conversational
> two-host podcast style, for a community of **volunteers and contributors**
> — people considering joining the network, not investors or academics.
>
> Tone: warm, curious, grounded, occasionally playful. Not corporate. Not
> academic. Like two thoughtful people genuinely discovering something they
> find interesting.
>
> **Lead with the human stake**, not the architecture. The architecture is
> evidence, not the headline.
>
> **Highlight these as the genuine innovations**, in this order of weight:
>
> 1. **Axiom-bound architecture** — the philosophy is mathematically embedded
>    in the points formula and the database schema, not just stated in a
>    mission page.
> 2. **Multi-AI consensus** — Claude, GPT, Gemini can score the same
>    submission, and the system supports four merge strategies (single,
>    average, weighted, majority).
> 3. **Soft-contract claims** — multiple builders can work on the same task
>    in parallel; the network rewards quality, not speed of grabbing.
> 4. **AI + human moderation as paired layers** — neither alone is trusted;
>    the AI evaluates, a human moderator confirms, and both leave provenance.
> 5. **Re-audit guard** — once an author edits the description after the AI
>    audit, the score is invalidated and a fresh audit is required before
>    publishing. Closes a real exploitation vector.
> 6. **Negative-space scoring** — the audit detects what a project *lacks*
>    among the 17 Foundations, not just what it has.
>
> Do **not** describe the system as "another platform" or "marketplace". It
> is neither. Frame it as **civic infrastructure for collective evaluation
> of life-aligned action**.
>
> End with a clear, simple invitation to the listener: how to join, what a
> first step looks like, and why it matters.

---

## Speaking Notes for the Hosts (background context, not script)

The two hosts can riff freely, but these are the ideas they should hit.

### Opening — the human stake (≈1 min)

Most online platforms ask: *what can we sell, what can we monetize, what
can we measure?* Anthosphere asks something else: **does this work serve
life?** That is the question, and everything in the network is built to
answer it precisely.

Start with a small concrete image. Someone has an idea — say, restoring a
forgotten mineral spring in their village, or building a tool that helps
elderly people stay connected with their grandchildren. They submit it.
Within minutes an AI reads it, asks the hard questions, scores it across
seventeen dimensions of life-impact. A human moderator reviews. The project
goes live. Other people pick up the tasks, do real work, get scored, get
points. The network learns what kind of life-aligned action actually
happens.

That's the system. Now the interesting parts.

### The axiom is in the math (≈1.5 min) — INNOVATION #1

Most "values-driven" platforms put a mission statement on the About page
and never touch it again. Anthosphere does the opposite. The Grand Axiom —
*life is the irreducible value of any sustainable system* — is **wired into
the formula**.

Every point earned passes through:

```
Points = base × (ai_score / 100) × LIS × FAS
```

Where **LIS** is Life Impact Scale (local, regional, global) and **FAS** is
Foundations Alignment Scale — how many of the 17 Foundations the work
actually serves. A brilliant piece of work that doesn't align with life
**cannot accumulate** in this network. The architecture enforces the axiom.
That is not common. Most systems can't tell you what they value, because
their code doesn't know.

### The 17 Foundations and 5 Domains (≈1 min)

The Foundations are not an arbitrary checklist. They come from a book —
*Architect of Reality* — that took years to formulate. Things like
biological diversity, human dignity, knowledge access, intergenerational
memory, AI alignment with life, conflict resolution, children's rights.

These get rolled up into 5 Domains: Ecology, Energy, Psychology, Peace,
Tech. Every project gets a score in each domain. The audit doesn't just
ask "is this good?" — it asks **what does this not yet support?** That
question shapes the next part.

### Negative-space scoring (≈45 sec) — INNOVATION #6

When the AI audits a project, it flags **weak foundations** — what is
*missing*. This is unusual. Most evaluation systems reward what's present
and ignore what isn't. Anthosphere treats absence as data. If a project
about clean water never mentions the people who'll maintain the system
five years from now — that gap shows up. The author can fix it, or accept
a lower score and publish anyway. Either way, the gap is visible.

### Multi-AI consensus (≈1 min) — INNOVATION #2

When you let one AI judge everything, you get one AI's blind spots
codified into the system. Anthosphere is built so that Claude, GPT, and
Gemini can all score the same submission. The provider layer is
**pluggable** — there's a clean `AIProvider` interface, and a consensus
engine that knows four strategies: take one provider's word, average them,
weight them, or go by majority.

Right now Claude is the active provider. The architecture is ready for
the others. This matters because it means **no single AI gets to define
what life-aligned looks like**.

### Soft-contract claims (≈1 min) — INNOVATION #3

This one is subtle but important for the volunteer experience. When you
take a task in most systems, you either lock it (nobody else can work on
it) or it's a free-for-all (whoever submits first wins).

Anthosphere does neither. You can **claim** a task — it tells everyone
you're working on it, for 72 hours — but **other builders can still
submit**. The system isn't a race to grab; it's a collaboration with
visibility. If two people submit good work, both get evaluated. The one
who claimed first gets moderator priority, but quality wins. Up to ten
active claims per builder, parallel-safe.

This is built specifically because **rewarding speed of grabbing produces
worse work than rewarding quality**.

### AI plus human, as paired layers (≈1 min) — INNOVATION #4

Every action in the network leaves a trail. AI evaluates, human moderator
confirms. Two layers, both required. Both logged. The points ledger has
full provenance — base reward, AI score percentage, LIS multiplier, FAS
multiplier, timestamp.

If anything ever needs to be audited or reversed — it can be. Nothing in
this network is "magic". Every point came from a sequence of decisions
you can trace back.

Community moderators have levels — one to five — based on their
**accuracy over time**. A moderator whose decisions diverge too often from
final outcomes loses standing. The system learns who to trust.

### Re-audit guard (≈30 sec) — INNOVATION #5

Small detail with big consequences. Once the AI audits your project, you
get suggestions. You can accept them — but the moment you change the
description, the original score is **invalidated**. You must re-run the
audit before publishing. This closes a real exploit: the old "edit after
review" trick used in most submission systems. You can't game the AI by
adding the right keywords after the score.

### What this is not (≈30 sec)

It's not Upwork — points aren't money, this isn't a freelance marketplace.

It's not Reddit — moderation is **substantive**, not popularity-based.

It's not crowdfunding — though projects can ask for help and resources.

It's not a catalog — it's an **active network of action**.

Closest analogy: a civic infrastructure layer. Like a library, or a
volunteer fire department, but for life-aligned digital and real-world
projects.

### The invitation (≈45 sec)

If you've ever wanted to do work that matters — and felt that most online
spaces are built to extract attention rather than channel effort — this
is for you.

There are three ways to start:

- **Submit a project.** Anything you genuinely care about that works in
  service of life. The audit will help you see it more clearly.
- **Take a task.** Browse open tasks at network.anthosphere.com/tasks.
  Pick one. Do real work. Earn points that mean something.
- **Become a moderator.** If you've earned standing in the network and
  want to help shape it, the path is open.

The system is at network.anthosphere.com. The architecture is open source
under CC BY 4.0. The book that grounds it — *Architect of Reality* — is
at anthosphere.com.

We're not asking for your money. We're asking for your attention, and a
small piece of your real work.

That's the invitation.

---

## Key facts the hosts should get right

- **Author / Architect:** Tony Parf (Anton Parf), based in Osijek, Croatia
- **AI co-author:** Claude (Anthropic)
- **Stack:** PHP 8 + MySQL 8, no framework, hosted on DirectAdmin
- **Active AI:** Claude Sonnet (the network is provider-pluggable)
- **License:** CC BY 4.0
- **Domain:** network.anthosphere.com
- **Foundation work:** *Architect of Reality* (2025), and 17 Foundations
- **Status (April 2026):** core cycle is closed and operational —
  submission, audit, task generation, claim, evaluation, points.

## Tone guidance

- **Don't oversell.** This is real, but it's early. Say so.
- **Don't be cynical about "tech bros".** The audience is volunteers, not
  haters. Steady, sincere energy.
- **Use specific examples**, not abstractions. "Restoring a forgotten
  mineral spring" lands; "leveraging community resources" doesn't.
- **Pause on the axiom.** It's the heart of the thing. Don't rush past it.
- **Close warmly, not urgently.** No FOMO. The invitation is open and
  patient.

## Words to avoid

- "Disrupt", "ecosystem play", "Web3", "decentralized" (technically true
  but the word is exhausted), "leverage", "synergize", "stakeholder"
- "Revolutionary", "game-changer", "next-generation"
- Any phrase that makes a volunteer feel like a "user acquisition target"

## Words and phrases that fit

- "Civic infrastructure", "life-aligned", "real work that matters",
  "collective evaluation", "the architecture enforces the axiom",
  "absence as data", "quality, not speed", "trail of decisions you can
  trace back"

---

*This document is the briefing. The hosts in NotebookLM will turn it into
conversation. Trust the format — it works best when the source is
specific and grounded.*
