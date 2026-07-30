# Feature: Async Batched Execution

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional. Pairs well with [sandboxed autonomy](sandboxed-autonomy.md) but doesn't require it.**

---

## What This Adds

Most agent interaction is synchronous: you open a chat, the agent works while you wait, you review the result immediately. That's fine for a lot of work, but it wastes the agent's most valuable property — that it doesn't need you present to make progress.

This feature lets the agent pick up scoped, well-specified work on a schedule (overnight, during idle hours) and hand you a batched summary later, rather than only ever working while you're watching.

Two complementary mechanisms make this practical:

**Scheduled unattended runs.** A queue of well-specified jobs — each one a task clear enough that a model can execute it without back-and-forth clarification — picked up on a schedule (a nightly cron tick is a natural cadence) and run to completion without supervision. The jobs that work best here are the ones where the *thinking* already happened in an earlier synchronous conversation; the unattended run is pure execution against an already-clear spec, not open-ended exploration.

**Asynchronous instructions left outside chat.** A way to hand the agent something to do without opening a chat session at all — leaving a note in whatever system you already use (a task manager comment, a note in a shared document) that the agent picks up on its own schedule. Safe, easily-reversible actions (reprioritize, relabel, mark complete) can be executed automatically; anything destructive or ambiguous gets queued for your explicit review instead of guessed at.

## Why the Summary Format Matters as Much as the Automation

The automation itself is the easy half. The part that actually determines whether this feature gets used or quietly ignored is what happens *after* the unattended work finishes: if the output of an overnight run is just "go check the log," most people never will, and the whole feature degrades into work nobody looks at. A short, readable summary — pushed to wherever you'll actually see it (a phone notification, a messaging app you check anyway) rather than left sitting in a file waiting to be opened — is what turns "the agent did some things overnight" into something you actually engage with the next morning.

This is also a genuinely good fit for anyone whose best thinking happens in bursts rather than continuously — a way to hand off a batch of well-specified work and come back to a result, instead of needing to be present for the whole arc of every task.
