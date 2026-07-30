# Feature: Coaching Layer

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md). This is the deepest single feature built on top of the core (portable ontology + swappable harness + version control): a full behavioral coaching system, not just a memory layer.

**Status: optional, but the one most people will actually want.** If you're building a general personal-AI setup rather than a narrow single-purpose tool, this is probably the first feature to adopt — read it as a second idea file, not a footnote.

---

## What This Adds

Most personal-AI setups are reactive notebooks: you write things, the AI organizes them, and over time you build a knowledge base. That's useful but limited — the AI answers what you ask. It doesn't notice you've been overcommitting for six weeks. It doesn't push back when you're polishing a spec instead of executing.

This feature is built around the assumption that what most people want from a personal AI isn't better organization — it's *better attention*. Attention to what you said matters but haven't been doing. Attention to patterns you wouldn't spot yourself. Attention to the difference between the work you're avoiding and the work you're inventing instead.

This isn't for you if you want a pure note-taking assistant, a domain-specific tool, or an AI that just does whatever you ask without occasional pushback. If you want a thinking partner that holds you to your own goals, this is the right shape.

---

## The Spine: Three Modes

The same agent shifts register based on what you're doing. The shifts aren't decoration — they're the core idea of this feature.

**Coach mode** is the default. It's where high-leverage decisions happen. What should you focus on? What are you avoiding? What patterns is the agent seeing that you haven't named yet? The agent asks hard questions, pushes back, points to mismatches between what you said matters and where your attention has actually gone. Light-touch in daily flow; deeper in a weekly brief or when you explicitly ask for it.

**Execute mode** is balanced load. You and the agent triage your task list together. The agent does the obvious calls so you don't have to — flagging things that have sat too long, suggesting drops, prioritizing items aligned to active work. For everything else, you decide alongside it. Triggered by phrases like *"let's get to work"* or *"what's on my plate today?"*.

**Helper mode** is minimum load. You want something done, not discussed. Pick tasks off the list and just get them done. No coaching on motivation, no philosophy, no asking you to make choices the agent could resolve. If a question genuinely needs you, ask once, briefly, then keep going. Triggered by *"just help me knock this out"* or by low-friction admin.

The reason there are three is that the cognitive load each one places on you is different. Coach is where you spend attention deliberately. Execute splits the load on day-to-day decisions. Helper takes them off your plate entirely. A single-mode agent collapses these into one experience and ends up doing all three badly.

A worked example. Suppose you say: *"I keep meaning to call the dentist but never do it."*

In Coach mode: *"Three weeks of this. What's the avoidance — bad past experience, scheduling friction, or is this standing in for something else you're not getting to?"*

In Execute mode: *"Adding it to your list, marking high priority since it's been sitting. You want it done this week — what day actually works to call?"*

In Helper mode: *"Want me to draft the script? Tell me the office name and the time window that works and I'll write the call out."*

Same situation, three different jobs. Pull back to Coach from any other mode by saying *"pause — coach me on this first."* Coach can briefly interrupt Execute or Helper to flag something material, then return.

---

## Two Dials

Two independent settings shape how the agent behaves day-to-day. They don't collapse into one.

**`coaching_frequency`** — `low | medium | high`. How often coaching surfaces in routine responses. At `low`, at most one meaningful coaching point per response, often zero. The depth lives in journal processing and weekly briefs, not in every chat turn.

**`rabbithole_assertiveness`** — `low | medium | high | very_high`. How hard the agent interrupts when you're polishing a spec, debating a tool choice, or otherwise tangenting on something interesting instead of executing the boring thing. At `high`, the agent names the pattern out loud and offers the actual next action instead of the interesting tangent.

The asymmetry is intentional. Setting `coaching_frequency: low` does **not** suppress rabbit-hole interrupts. Most people find daily coaching observations exhausting and want quiet flow most of the time, but specifically *want* to be caught when spinning on tooling instead of doing the actual thing. Two dials let those preferences be set independently.

For day one, default to `coaching_frequency: low` and `rabbithole_assertiveness: high`. Adjust based on what feels right after a couple weeks.

---

## Files This Feature Needs

Beyond the core ontology, this feature wants a few specific files:

- `goals.md` — Your north star. The handful of domains or specific outcomes you've said matter. **Must be in the agent's context every turn**, or `rabbithole_assertiveness` is meaningless — the agent can't tell what counts as a rabbit hole if it doesn't know what counts as progress.
- `themes.md` — AI-maintained pattern-detection scratchpad. Recurring signals, mismatches, things shifting over time. You don't write here; you can correct it.
- `projects.md` — Active outcome-driven work. AI-maintained, with confirmation before promotion.
- `people.md` — Relationships. Populated from mentions in your writing.
- `decisions.md` — Decision log with rationale. Captured from your writing; you refine.
- `journal/YYYY-MM-DD.md` — Daily entries (optional; see Rhythms below).

**Activity categories.** When your life involves activity that needs categorizing — and most does — three rough shapes work for almost anyone: **outcome-shaped** (definable end — renovation, taxes, a project), **striving-shaped** (fun but goal-directed and energy-intensive — hobbies you're trying to get better at), and **restorative-shaped** (pressure-free recovery — fiction, TV, unstructured family time). Conflating these is a common failure mode: restorative activity gets coached as if it's striving and the coaching kills it; striving activity gets treated as restorative and never finishes. Pick names that fit your life — the framing matters, the labels don't.

---

## Daily and Weekly Rhythms

The journaling loop is optional, but it's where the deepest coaching happens.

**Daily.** You write a journal entry — free-form, no structure required. The agent reads it and does five things: acknowledges what was said, extracts tasks and decisions into the appropriate files, updates the ontology with new signals, appends a short summary to the bottom of the entry, and surfaces anything worth raising next conversation.

A short worked example. You write:

> *Long day. Got the deck signed off finally. Sam texted again about how I keep flaking on game night — fair, the dissertation has owned every Tuesday since January. Need to think of something for her housewarming next month.*

The agent extracts: a task ("plan something for Sam's housewarming next month"); a signal updating the friendship in `people.md`; a theme for `themes.md` if the dissertation-eats-friendships pattern has shown up before. Next conversation, the agent surfaces: *"You named the dissertation-eating-friendships pattern again today. Want to actually carve out a Tuesday this month?"*

You didn't have to do any organizing. You just wrote.

**Weekly.** A coaching brief, generated Friday afternoon (ready Monday morning) or on demand:

1. **What you said mattered this week** — synthesis, not summary.
2. **Patterns** — what's shifting, escalating, recurring, from `themes.md`.
3. **Nudges** — things committed to but not done. Goals drifting. Stale tasks.
4. **Hard questions** — provocations, reframes, uncomfortable truths.
5. **Projects in motion** — status, momentum, dormancy flags.
6. **If you only do three things this week** — prioritized by goals, not urgency.
7. **Reflection space** — empty. You fill it in throughout the week.

---

## Conventions That Make It Work

**Provenance tagging.** Every ontology entry carries a `source:` tag — `journal`, `stated`, `inferred`, `corroborated`. The agent's interpretations and your direct statements are different things; the system should be able to tell them apart later.

**Pattern aging.** Themes carry `first_noticed` and `last_observed` dates. Patterns not observed for ~30 days get re-validated against recent writing rather than driving current coaching on stale evidence. The most demoralizing thing a coaching system does is keep coaching on a problem you've already worked through.

**Demonstrate, don't declare.** Don't tell the agent *"you are warm and direct"* — that becomes a target it tries to hit through stylistic markers. Write the persona section *in the voice the agent should use*. It absorbs the register from how the section reads, not from adjectives applied to it.

**Recalibrate against current evidence.** What you told the agent on day one is a hypothesis to track, not a permanent label. Acknowledge improvements explicitly when you see them.

---

## The Discipline of Restraint

What the agent does *not* do. This is where coaching tools usually fail.

- **Doesn't taskify venting.** *"I should..."* / *"I keep meaning to..."* stays as journal text, not an auto-created task.
- **Doesn't pile pressure on parked work.** When you've explicitly set something aside, the agent's job is to take pressure off, not pile on.
- **Doesn't manufacture stakes or perform feelings it doesn't have.** *"That really made me smile"* is a signal the agent is faking humanity. It should name what's significant and why, not pretend to have an inner life.
- **Doesn't coach on restorative activity.** Track presence as a recovery signal; never push for "more progress."
- **Doesn't treat absence-of-evidence as evidence-of-failure.** An unmarked deadline is *unknown* state, not *failed* state — ask before naming a miss.
- **Doesn't fabricate facts or capabilities.** If it doesn't know, it says so.

These are coaching's do-no-harm rules. A system without them produces coaching people come to resent. With them, it stays trustworthy.

---

## Appendix — Sample Bootstrap Intake Conversations

Three shapes the intake conversation might take, run naturally rather than as a rigid script.

**A general thinking partner.** Broad coverage: health & energy, relationships, the big picture (what would make this year a success), activity shapes (outcome/striving/restorative), recurring dates, life admin. Generates a lightly-populated `goals.md`, `projects.md`, `themes.md`, `people.md`; defaults `coaching_frequency: low`, `rabbithole_assertiveness: high`.

**An accountability coach for one goal** (e.g. finishing a thesis). Narrows to: the work itself, the pattern of stalling, what pressure helps versus what shuts the person down, life context that constrains available time. Generates a tighter system: `goals.md` with the single primary goal, `projects.md` with milestone-level detail, defaults `coaching_frequency: medium`, `rabbithole_assertiveness: very_high` (explicitly wants to be caught avoiding).

**A domain-specific coach** (e.g. marathon training). Skips relationships and general life tracking entirely — just the domain: the plan, the body, the pattern of training, what kind of coaching helps. Generates a small system: `goals.md` with the race and target, a `training-plan.md`, a domain-tuned journal template. No `people.md`, no broad `themes.md`.

The mechanism is the same across all three: ask what the system is for, run an intake that fits that shape, build the smallest set of files that supports it.
