# Feature: Publishing Pipeline

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional — only relevant once you want to turn private working material into something you share publicly.** This is, for what it's worth, the process that produced this very repository.

---

## What This Adds

At some point a system like this accumulates working knowledge worth sharing — a design pattern, a write-up, a piece of the system itself. Publishing it safely has two distinct risks: the writing might be unclear or wrong, and the material might contain identifying details that shouldn't go out (real names, internal hostnames, private paths, anything that fingerprints the specific person or setup it came from). A single self-review by the same agent that wrote the draft is weak on both counts — it shares the draft's own blind spots.

The pipeline:

1. **Draft**, written directly by the main agent from what's actually true today — no bug-history narrative, no internal jargon, objective register.
2. **Readability QA**, run twice in parallel by two independently-trained models (a frontier model and a different-lineage open-weight model), scoped narrowly to clarity, grammar, and whether any build instructions are actually unambiguous — explicitly *not* a redesign pass.
3. **Adjudicate**, cross-checking where the two reviewers agree against the actual draft, applying the high-value fixes, skipping low-value nitpicks.
4. **Information-leak QA**, the same two-reviewer structure, different rubric: scan for real IPs, domains, names, hostnames, internal paths — anything that fingerprints the specific deployment or its owner.
5. **Human review and go/no-go** — the adjudicated findings presented plainly, letting the human decide final scope (e.g., docs-only vs. docs-plus-code) and where it gets published.
6. **Publish**, confirming the account and scope match what was actually reviewed before it goes out.

## Why Two Independent Models, Twice

The core design choice: run each QA pass with two models from genuinely different training lineages, not two calls to the same model or family. When two independently-trained models converge on the same finding without seeing each other's output, that convergence is itself strong evidence the finding is real — it's much less likely to be a shared training artifact than a single model's guess would be. When they disagree, that's the signal to go verify against the actual source rather than trust either one blindly.

Two other things worth keeping if you adopt this: state an explicit "80/20, not perfection" bar to every reviewer and to yourself during adjudication, and require every reviewer to say an explicit "stop-publishing" flag is either present or absent — never leave "nothing came back" ambiguous between "everything's fine" and "the reviewer just didn't flag anything."

## A Legitimate Fallback

If a leak-scan pass finds real identifying information baked into code or scripts that would otherwise ship alongside a write-up, it's a completely legitimate outcome to publish the conceptual write-up alone and hold the code back for later sanitization — say so explicitly in what you do publish, framed as a deliberate choice rather than an admission of incompleteness. Docs-only is a fine first release.
