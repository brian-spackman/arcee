# Arcee — Own Your Relationship With AI

You can call it whatever you want. The agent that bootstraps it from this file will ask you on day one.

---

## What This Is

Every mainstream AI product wants to be where your context lives. Your chat history, your preferences, your accumulated understanding of your own life — all of it sits inside one company's product, readable only by that company's model, gone (or exportable-at-best) the day you switch providers or the product changes shape under you.

Arcee is the opposite bet: your context lives in files you own, on a machine you control, and the model reading them is a swappable part. Point Claude at the files today, point Gemini or a local model at them next year — the files don't change, only the reader does. The value compounds in the ontology, not in the vendor relationship.

Hand this file to your favorite AI — Claude.ai, Gemini, ChatGPT, Claude Code, Cursor, whatever — and ask it to bootstrap a version tailored to you. By the end of the first conversation, you'll have a small set of structured Markdown files and an agent that knows how to read, update, and reason against them as you work.

If you've read Andrej Karpathy's [personal-LLM-wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), the file structure and update mechanism here will look familiar. Arcee was developed independently — I built it without knowing about his work and read the gist only after — but the format of this document borrows directly from him: sharing the idea as a single portable file that bootstraps each user's own version is a much better distribution model than shipping code, and credit for that goes to him.

---

## Why You Might Want This

Most personal-AI setups are rented, not owned. You write things into a product's memory feature, the product organizes them, and over time the product knows you — but only inside that product. Switch tools and you start over. The company changes its retention policy, its pricing, or its model lineup, and your accumulated context moves or degrades with it.

Arcee decouples the two things that usually get bundled: the *substance* (what you've told an AI about your life, your goals, your patterns) and the *intelligence* (whichever model happens to be best, cheapest, or most private this month). The substance lives in your files. The intelligence is rented, deliberately, because renting the smartest available model is fine — renting your own memory is not.

This file isn't for you if you're happy with a single vendor's ecosystem, want a pure note-taking tool, or need a domain-specific product (a coding agent, a writing collaborator) rather than a general context layer. Take what's useful and leave the rest.

If you want the leverage of frontier AI without the lock-in, this is the right shape.

---

## What's Actually Required (Not Optional)

Everything past this section is a menu. These three pieces aren't — skip any one of them and you don't really have the thing described above, you have a slightly-more-organized chatbot.

**1. Ontology files that are actually yours.** A small set of structured Markdown files describing your goals, projects, people, patterns — whatever your version of "the things worth remembering" turns out to be. What goes in here is genuinely different for every person; a thesis-coaching setup and a general life-assistant setup share almost no file names. The bootstrap conversation below is how you find your own shape — don't copy someone else's file list and expect it to fit.

**2. A harness that treats the ontology as the source of truth, not the model.** Whatever CLI or app you're running — Claude Code, an AGENTS.md-reading tool, a bare chat window with the files pasted in — its job is to read these files, update them, and reason against them every session. The test: could you point a *different* model at the same files tomorrow and lose nothing? If the answer is no, the setup has quietly become vendor-shaped again.

**3. Version control, even if it's just a local git repo.** Not for collaboration — for the agent's own sake. A git history means the agent (and you) can look back at how the ontology actually evolved, catch when a file got corrupted or a bad edit crept in, and recover cleanly from a mistake instead of trusting whatever state happens to be on disk right now. `git init` in a folder on your own machine satisfies this — you don't need GitHub, a remote, or any of the collaboration features. If git is genuinely not available to you, a hand-maintained `LOG.md` — a chronological, append-only file the agent updates each session, date-stamped entries describing what changed and why — is a fallback, but it's a fallback, not an equivalent.

That's it. Everything else in this repo — coaching modes, multi-agent bridges, parking protocols, research patterns, publishing pipelines, model routing, sandboxed autonomy — is a feature you can bolt on because it earned its place in one real deployment. None of it is required to get the core value.

---

## The Bootstrap Conversation

Day one matters. The agent's job in your first conversation is to find out what the system is *for*, then build the smallest file set that supports it — not to hand you a template.

Ask yourself (or let the agent ask you): what do you want this to do? A broad thinking partner across all of life needs a fuller file set than a narrow accountability coach for one goal, which needs more than a single-domain assistant that only ever talks about one project. Let the answer shrink or grow the ontology — don't force your life into a generic shape because a template said so.

**Seeding from existing content.** If you already have journals, notes, or a populated note-taking system, point the agent at it and let it build the initial ontology from what's there. If not, start sparse — the first month will be slim, and that's normal. Forcing someone with years of useful notes to start from scratch is bad advice. Forcing someone with nothing to "import existing data" anyway is also bad advice.

For a worked example of what a fuller bootstrap intake looks like in practice — including the specific questions and how the answers shape the file set — see [`features/coaching-layer.md`](features/coaching-layer.md), which documents the deepest single feature built on top of this core: a full coaching layer with three operating modes and two independent behavioral dials.

---

## Feature Catalog

Everything below is optional. Each one exists because it earned its place solving a real problem in one real deployment — not because a complete system needs all of them. Pick what fits; ignore the rest; the core value (portable ontology + swappable harness + version control) holds regardless of which of these you adopt.

| Feature | What it adds | File |
|---|---|---|
| **Coaching layer** | Three operating modes (Coach/Execute/Helper), two independent behavioral dials, daily/weekly rhythms, a discipline-of-restraint rule set | [`features/coaching-layer.md`](features/coaching-layer.md) |
| **Multi-agent mesh** | Grow from one agent to several across trust zones (personal/work/specialist), with sanitized bridges and provenance tracking | [`features/multi-agent-mesh.md`](features/multi-agent-mesh.md) |
| **Parking protocol** | Pause a conversation mid-thought into a structured brief, resume it cleanly days or weeks later without losing the thread | [`features/parking-protocol.md`](features/parking-protocol.md) |
| **Co-editing convention** | A visual convention for agent-voice vs. human-voice inside shared documents, so collaborative drafting doesn't get confusing | [`features/co-editing-convention.md`](features/co-editing-convention.md) |
| **Sandboxed autonomy** | Give the agent a real sandbox with elevated privileges, safely, and a way to reach beyond it deliberately when it needs to | [`features/sandboxed-autonomy.md`](features/sandboxed-autonomy.md) |
| **Mobile-first workflow** | Do most of your actual thinking with the agent from a phone, not a desk | [`features/mobile-workflow.md`](features/mobile-workflow.md) |
| **Async batched execution** | Let the agent work unattended on a schedule and hand you a batched summary later, instead of only ever working synchronously in chat | [`features/async-execution.md`](features/async-execution.md) |
| **Research patterns** | A cheap default research mode plus a heavier, explicitly-gated adversarial-verification mode for when accuracy really matters | [`features/research-patterns.md`](features/research-patterns.md) |
| **Publishing pipeline** | A cross-model QA process for turning private working material into something safe to publish | [`features/publishing-pipeline.md`](features/publishing-pipeline.md) |
| **Model routing** | Match cheap/expensive models to task classes instead of running everything on your most expensive tier | [`features/model-routing.md`](features/model-routing.md) |
| **Batched task triage** | Group your own required actions by context (at a computer, on your phone, a decision only you can make) instead of getting interrupted one at a time | [`features/task-batching.md`](features/task-batching.md) |

More features may get written up over time as they prove durable in real use — this is a starter catalog, not a ceiling.

---

## What I Actually Use It For

A few concrete, personal-optimization uses that aren't worth their own idea file but are worth knowing this kind of system is good for: weekly meal planning against a recipe library, trip-packing lists tailored to weather and duration, reordering a shopping list into store-walk order, camping trip planning against weather and fire-ban data, and flight-day automation (reminders, calendar events) triggered off a booked flight. None of these are architecturally interesting — they're just examples of the everyday value once the core pattern is in place. Build your own version of these; they're the easiest on-ramp once the ontology and harness exist.

---

## License

Released under [Creative Commons Attribution 4.0 International (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Adapt it, fork it, rewrite it, rename it, build something commercial on top — all fine. Just credit the original. **No warranty, no liability.** You build the system at your own risk; you operate it at your own risk.

---

## Make It Yours

This document describes Arcee's core idea, not a template to copy verbatim. Your version should not look like mine — it should look like you. The bootstrap conversation is supposed to bend the system to your goals, your categories, your file inventory. If a feature in the catalog above doesn't fit your life, skip it. If something obvious is missing, add it and consider writing it up.

The system is supposed to emerge from your actual life, not from a template. The first month will be sparse if you're starting from nothing — that's normal. Sparse is honest.

Hand this file to your AI of choice. Tell it what you want the system to do for you. Let it run the bootstrap.
