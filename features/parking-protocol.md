# Feature: Parking Protocol

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional, but the single most-used feature in the reference deployment.** If you only add one feature from this catalog, this is the one worth trying first.

---

## The Problem It Solves

A normal chat thread has one lifecycle: open it, work in it, eventually it scrolls away or gets closed, and whatever thinking was mid-flight either gets lost or has to be painfully re-explained from scratch next time. That's fine for quick questions. It's a real cost for anything that spans multiple sessions — a half-formed plan, a design decision you're still weighing, a project you'll come back to next week but not today.

The parking protocol gives conversations a clean pause/resume lifecycle instead of an implicit, lossy one.

## How It Works

When a conversation needs to end but the thread of thinking shouldn't be lost, you say something like *"park this"*. The agent writes a structured brief to a file — a fixed, small set of sections:

1. **What we were chasing** — the actual goal, not just the surface topic.
2. **Where we left off** — the state of thinking at park-time: last conclusion, last open thread, last pending decision.
3. **Open questions** — what's blocking forward motion. Terse, bulleted. "None" is a valid answer.
4. **Next move** — the specific, concrete action to take on resume. Not vague — *"decide between X and Y, draft the spec, run it past Z"*, not *"continue thinking about this."*
5. **References** — files, links, related briefs. Breadcrumbs for a cold start.

The chat can then be closed safely. To resume, you open a fresh chat and point the agent at the brief — file path, slug, whatever addressing scheme you use. The agent reads it, summarizes back what you were doing in two or three sentences, and confirms before continuing. If the summary drifts from what you actually meant, you correct it and the agent updates the brief in the same pass.

## Why a Fixed Format Matters

The value isn't "write some notes for later" — you could do that in any scratch file. The value is that every brief has the same five sections in the same order, every time, so resuming from a brief you wrote three weeks ago costs the same low effort as resuming from one you wrote yesterday. Without a consistent, disciplined format, "notes for later" degrades into inconsistent fragments that are individually fine but collectively unusable — you end up re-reading whole threads to figure out where you left off, which defeats the purpose.

## Staleness

Briefs that sit untouched for a while are worth surfacing, not silently accumulating forever. A reasonable pattern: mention a brief in a weekly check-in once it's been untouched for ~30 days ("this has been parked a month — still relevant?"), and force an explicit kill-or-keep decision at ~60 days. When a brief's work is done or absorbed elsewhere, delete it in the same pass that captures the outcome — don't let done work linger as a parked brief.
