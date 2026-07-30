# Feature: Model Routing

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional, and the most direct expression of "no vendor lock-in" in the whole catalog** — this feature only exists because the harness treats the model as a swappable part.

---

## What This Adds

Once you can point more than one model at the same ontology, a natural question follows: why run everything on your most expensive tier? A weekly deep-coaching session and a quick "reschedule this task" call don't need the same model. Right-sizing the model to the task saves real cost without losing quality where quality actually matters.

The pattern: keep a small, explicit mapping from task class to model tier — design/architecture/hard-planning work goes to the most capable model available; well-specified execution of an already-clear plan goes to a cheaper mid-tier model; mechanical lookups and simple parsing go to the cheapest capable model. Pick the model *at the start of a task*, not mid-task — switching models partway through means the new model has to rebuild context from scratch, which often costs more than just finishing on the model you started with.

A second layer worth adding once the basic routing is in place: a running, evidence-based catalog of which models are actually good at what — not vendor marketing claims, but your own dated observations from real use ("this model is a poor tool-caller," "this one is worth its price for bulk text processing"). Keep it as a living document the agent itself updates as it gathers evidence, not a one-time setup task.

## The Part Worth Calling Out Specifically

A genuinely low-effort, high-value extension of this pattern: letting the agent run its own quick comparisons when a routing question comes up, rather than you having to manually benchmark models yourself. "I wonder which model handles X well" can turn into the agent spinning up a small, cheap head-to-head test across a few candidate models and reporting back — often resolved in minutes, with no explicit instructions needed beyond the question itself. This turns model selection from a research project you'd otherwise skip into something that happens naturally, on demand, as questions come up.

The bigger point behind this feature: because the harness never assumes a specific model, this kind of routing and experimentation is possible at all. A setup wired to one vendor's specific product can't do this — there's nothing to route between.
