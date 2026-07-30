# Feature: Research Patterns

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional. Worth adopting even in a minimal setup, because the "gate the heavy version" lesson below is cheap insurance.**

---

## What This Adds

"Research this for me" can mean two very different things, and conflating them is expensive. Most questions want a quick, cheap synthesis. A smaller number of questions genuinely need a rigorous, fact-checked, adversarially-verified answer — because you're about to act on the conclusion irreversibly, or the stakes of being wrong are high. Treating every question as if it needs the second kind of treatment burns a lot of resources on questions that didn't need it.

**A lightweight default.** Split the question into a few angles, run a handful of cheap subagents in parallel — one per angle — and have the calling agent read and synthesize the results itself. No verification pass, no fixed budget concern. This should be the default for anything that sounds like "look into X" or "what do people think about Y."

**A heavy, explicitly-gated mode for when it actually matters.** A full multi-source fan-out with adversarial verification — each claim checked by independent reviewers trying to refute it, not just confirm it — followed by a synthesis pass that only keeps what survived scrutiny. This is dramatically more expensive (many times the token/API cost of the lightweight version) and should never fire silently just because a question sounds like it wants "deep" research.

## The Lesson Behind the Gate

The gate on the heavy mode isn't theoretical caution — it's a direct response to a real incident where a routine, lay-of-the-land question triggered the heavy harness by accident (the wording sounded like it warranted deep verification when it didn't), and the resulting fan-out burned an enormous amount of budget on a question that needed a five-minute answer.

The fix: make the heavy mode require an explicit, named confirmation before it ever runs — even when the user's phrasing sounds like a match ("dig into this," "really research this properly"). Ask something like *"Do you want the full verification pipeline for this, or the quick version?"* and only proceed on an unambiguous yes. Default to the lightweight version whenever there's any doubt. The cost of asking once is trivial; the cost of guessing wrong in the expensive direction is not.
