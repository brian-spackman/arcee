# Feature: Mobile-First Workflow

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional, but in the reference deployment this is the single highest-impact feature on day-to-day quality of life.** Almost all real use of the system happens away from a desk — on a train, on a couch — not sitting at a keyboard.

---

## What This Adds

A lot of the value of the setup described in the core idea file depends on low-friction capture and low-friction review: journaling on the fly, checking a task list between meetings, reading a weekly brief on a commute. If using the system requires sitting down at a computer, most of that value never gets captured — the moment passes and the thought doesn't get written down.

Two pieces make this actually work in practice:

**A mobile-capable agent client.** Something that lets you have a genuine, full-capability conversation with your agent from a phone — not a stripped-down mobile-web view, the same agent with the same tools and context you'd get at a desk. [Happy](https://happy.engineering) is one such bridge for Claude Code specifically (a self-hosted relay that lets a phone app drive a full CLI agent session running elsewhere) — but the general requirement is provider-agnostic: whatever harness you're running, make sure it has a real mobile story, not an afterthought one.

**A synced note-taking surface.** If your ontology files live in something like Obsidian, the files need to actually be current on your phone when you open the app, and changes you make on your phone need to land back on the machine your agent reads from — within seconds, not "eventually, on next manual sync." Two ways to get this: **Obsidian Sync** (the paid first-party option, simplest to set up) or **Self-Hosted LiveSync** (a free, self-hosted alternative using CouchDB, more setup but no subscription and no third-party server holding your notes). Either works; a stale or manually-triggered sync defeats the purpose — you want it automatic and fast enough that you never think about it.

## Why This Matters More Than It Sounds

It's tempting to treat "works on mobile" as a nice-to-have polish item, something to add once the core system is solid. In practice, if most of your actual thinking happens away from a keyboard — which for most people, most of the time, it does — a system that only works well at a desk will get used far less than one that works wherever you actually are. This is less an architectural feature and more a distribution decision: get the mobile story right early, because it changes how much the rest of the system actually gets used.
