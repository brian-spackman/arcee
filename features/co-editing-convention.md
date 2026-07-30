# Feature: Co-Editing Convention

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md). Skip this if you only ever work with the agent in chat.

**Status: optional, but cheap to adopt and high-value if you edit files alongside the agent.**

---

## What This Adds

For anyone editing files alongside the agent — Obsidian, VS Code, any markdown surface — agreeing on a visual convention for "agent voice" vs. "your voice" inside the same document avoids confusion in co-edited files: project plans, weekly briefs, design docs, anything the two of you build together over multiple sessions.

The convention: agent contributions live in named callouts; your reactions live in plain blockquotes.

```markdown
Your text is plain prose, written normally.

> [!note] Drafting note
> Agent's suggestion or context goes here.

> agreed, let's do this — and add a follow-up to also check X.
```

The asymmetry is the point. **Named callout = agent voice; plain `>` quote = your voice.** Either party can interject anywhere, without waiting for a designated "comments" section. When the agent processes a doc you've marked up with `>` responses, it treats each one as an instruction to act on — same as chat input, just embedded in the document instead of a separate window.

The agent never edits your prose substantively. Its contributions go in callouts, not inline edits to your sentences.

---

## Why It's Worth More Than It Looks

Chat is a fine interface, but it's a narrow one: you ask, it answers, you ask again. Co-editing a document changes the shape of the collaboration — you're both looking at the same evolving artifact, and either of you can add to it at the point that matters, not just at the bottom of a scrolling transcript.

There's a plausible reason this feels better than chat beyond convenience: a shared document rewards a kind of sustained, low-pressure thinking that a back-and-forth chat window doesn't — you're not waiting for a reply to feel productive, you're both just building the thing. Take that as an informal observation, not a researched claim; nobody involved in writing this is a psychologist, and the actual mechanism (if there is one) hasn't been tested.

What's more concrete: this convention scales to documents chat doesn't handle well — long-running project plans, weekly retrospectives, anything that accumulates over weeks rather than existing inside one conversation.
