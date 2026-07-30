# Arcee

A way to own your relationship with AI: a portable ontology (Markdown files describing your goals, projects, patterns) plus a harness-agnostic instruction set, so the intelligence reading your files stays swappable while the accumulated value — the files themselves — stays yours. Hand the core idea file to your favorite AI — Claude.ai, ChatGPT, Gemini, Cursor, Claude Code, whatever — and ask it to bootstrap a version tailored to you.

## Start here

**[`idea-file_arcee.md`](idea-file_arcee.md)** — the core idea file. Self-contained: what the system is, why it avoids vendor lock-in, and the three pieces that are actually required (a personalized ontology, a harness that treats the files as source of truth, and version control). Everything else is optional.

## Optional features

Once the core is running, `features/` holds a catalog of things one real deployment found worth building on top — each written up as its own short, standalone idea file. Pick what fits; none of them are required:

| Feature | What it adds |
|---|---|
| [Coaching layer](features/coaching-layer.md) | Three operating modes, two behavioral dials, daily/weekly rhythms |
| [Multi-agent mesh](features/multi-agent-mesh.md) | Grow from one agent to several across trust zones |
| [Parking protocol](features/parking-protocol.md) | Pause and cleanly resume conversations across sessions |
| [Co-editing convention](features/co-editing-convention.md) | Agent-voice vs. human-voice inside shared documents |
| [Sandboxed autonomy](features/sandboxed-autonomy.md) | A real sandbox, elevated privileges, deliberate doors out |
| [Mobile-first workflow](features/mobile-workflow.md) | Doing most of the real work from a phone |
| [Async batched execution](features/async-execution.md) | Unattended scheduled work, batched summaries |
| [Research patterns](features/research-patterns.md) | A cheap default and a gated, rigorous alternative |
| [Publishing pipeline](features/publishing-pipeline.md) | Cross-model QA for turning private material public |
| [Model routing](features/model-routing.md) | Matching cheap/expensive models to task classes |
| [Decision quality](features/decision-quality.md) | Structured evaluation for consequential decisions |
| [Batched task triage](features/task-batching.md) | Grouping your own required actions by context |

More are added as they prove durable in real use — this is a starting catalog, not a ceiling.

## License

[CC-BY 4.0](LICENSE). Adapt, fork, rewrite, rename — just credit the original. No warranty, no liability.
