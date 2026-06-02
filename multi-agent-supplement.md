# Multi-Agent Supplement

A supplement to [`idea-file_arcee.md`](./idea-file_arcee.md) — or to any compatible single-agent personal-LLM coaching idea file. This document describes what changes when you grow a single-agent system into a mesh of n agents at different organizational scopes, exchanging context safely.

It's a graft, not a parallel idea file. If you haven't read the base, read it first.

---

## You Probably Don't Need This

The single-agent baseline is enough for almost everyone. The reasons to extend into a mesh are narrow and specific:

- **Privacy partition.** Content from one domain must not live on another domain's infrastructure — personal data off employer hardware, employer data off personal hardware, client data off vendor hardware.
- **Specialization that benefits from sovereignty.** A thesis coach, a marathon coach, a nutrition coach — each can be its own agent with its own ontology, voice, and rhythm, rather than one mega-agent that handles all of them clumsily.
- **Multiple humans on the same system.** A shared household agent, a partner's agent, your own agent — overlapping interests, but each owns its own data.

If you don't have one of those reasons, don't do this. LLMs are leaky. Multi-agent systems compound their failure modes. The first month is already sparse with one agent; with two it's twice as sparse. You will spend setup time on infrastructure you didn't need.

> [!warning] Use at your own risk
> Bridge files, by design, carry information from one trust zone to another. Sanitization mistakes are possible and the author takes no liability for any data that leaks where it shouldn't. **No warranty, no liability.** If you're not certain you understand the privacy and policy implications for your situation, don't run this pattern.

---

## What Stays the Same

Each agent in the mesh still runs the single-agent system. Its modes, dials, files, voice, the discipline of restraint, the journaling loop — all unchanged. Each agent has its own copy of the base instruction file and its own ontology. Two agents = two complete single-agent systems, each sovereign, plus the additions below.

## What's New

Six things, in rough order of how often they come up:

1. **Shared rules.** A small set of operational rules every participating agent loads. Bridge protocol, schema definitions, settings shared across agents.
2. **Per-pair sanitized bridges.** Transient outboxes between selected agent pairs.
3. **Shared-ontology surfaces.** Optional. Content that overlaps a subset of agents lives in a surface those agents jointly reach.
4. **A transport.** How a write by agent A becomes visible to agent B.
5. **Trust posture per pair.** Different pairs have different content rules.
6. **Provenance with peer-source tags.** Each assertion in any ontology records where it came from, including which peer if any.

---

## The Six Principles

These do real work. The protocol falls apart if any one of them is skipped.

**Per-agent sovereignty.** Each agent owns its files. No agent reads another agent's private storage. The only legitimate paths into another agent's ontology are sanitized bridges and shared-ontology surfaces the receiving agent explicitly participates in.

**Per-pair sanitized bridges, transient and append-only.** When agent A has something agent B needs to know, A writes a sanitized observation to its `A→B` outbox. B reads, integrates with judgment, deletes the entry. Steady state: bridges are empty. The actual cross-agent memory lives in each agent's own ontology and shared surfaces, with provenance tags showing what came from where.

**Receiver-applied judgment, not absorption.** The receiver does not import the sender's words as fact. It reads the entry, decides what weight to give, integrates into its own ontology with its own interpretation, and explicitly flags disagreement to the human when it sees it. This rule does real work — without it, n agents in a mesh tend to drift into a hive mind where one confident agent's claim propagates everywhere unchecked. Absorption errors compound faster than corroboration.

**Provenance everywhere.** Every assertion carries a source tag: `journal | stated | inferred | bridge:<peer> | corroborated`. When a peer-sourced observation is later corroborated by independent local evidence, the source is updated rather than overwritten. You should always be able to untangle "this agent believes X because peer Y said so" from "this agent believes X because the user said so directly."

**Shared schema, not shared data.** The canonical task format, bridge entry format, ontology field conventions — those live in the shared spine and every agent references them. Vocabulary aligns across agents that share zero content.

**Shared-ontology surfaces only where intersections earn them.** For any subset of agents that overlap on a content interest, you can give that intersection its own shared surface with explicit membership. Don't proliferate. Only stand up a surface when bridging the same content back and forth across a pair gets painful.

---

## Three Kinds of Storage

Generalizes from the single-agent file's "the files" section. In a mesh, content lives in one of three kinds of place, each with its own access semantics:

| Kind | Membership | Content rule | What it holds |
|---|---|---|---|
| **Per-agent storage** | One agent | Whatever rules that agent operates under | The agent's own ontology, journal, weekly artifacts |
| **Per-pair bridge** | One ordered pair (A→B) | Sanitization rule for that specific pair | Transient sanitized observations, append-only, drained on integration |
| **Shared-ontology surface** | Explicit subset of agents | Strictest rule of any member | Ontology content that overlaps the subset |

Each instance of each kind has an explicit access matrix. The topology you pick (next section) determines which bridges and shared surfaces are worth having.

Don't conflate the three. The mistake people make on day one is putting cross-agent content directly in their own per-agent ontology and bridging it constantly — eventually they realize they have the same content in three places. The shared-ontology surface is what fixes that, when the intersection is stable.

---

## Topologies

Three shapes show up in practice. Pick based on how many agents you have and how the content actually overlaps:

**Hub-and-spoke.** One central agent (typically the personal-life or general-thinking-partner) plus specialist agents (thesis coach, training coach, work agent). The hub talks to each specialist; specialists generally don't talk to each other. Bridges run hub ↔ spoke. Shared surfaces, if any, are hub ⊕ spoke. This is the right shape for most non-trivial setups — it scales linearly in pairs as you add specialists, and it matches how humans actually delegate (you're the hub; the specialists report to you).

**Full mesh.** Every pair has a bridge. Possible shared surfaces between any subset. Becomes unwieldy past ~4 agents — n agents means n(n-1) directional bridges, which is more discipline than most humans want to maintain. Use only when peers really do need to coordinate directly.

**Topic-based.** Bridges keyed by topic rather than agent pair. Multiple agents subscribe to a topic; writes fan out. Useful when you have many specialists with overlapping interests, but adds infrastructure complexity. Skip unless you're past 4-5 agents and the per-pair model has started to break.

If you're starting from one agent, you're almost certainly going to hub-and-spoke. Mesh emerges only if specialist agents need to coordinate without going through the hub, which is rare in personal-coaching systems.

---

## Trust Posture Per Pair

Each pair gets its own content rule. The matrix is a deployment-time artifact, not a built-in policy.

A worked example for a three-agent setup (personal + work + thesis-coach):

| From → To | Content allowed | Sanitization | Human-in-the-loop |
|---|---|---|---|
| personal → work | Directional load signals only (`life load is high`); no names, no specifics | Hard | Periodic or direct |
| work → personal | Directional load signals; no client names, no proprietary work content | Hard | Periodic or direct |
| personal → thesis | Anything relevant to the thesis — schedule, energy, blockers | Light | Direct |
| thesis → personal | Anything | Light | Direct |
| work ↔ thesis | (Bridge not used — they have nothing to coordinate on directly) | — | — |

The asymmetry is the point. Pairs that cross trust boundaries get heavy sanitization and possibly human-in-the-loop review. Pairs inside a single trust zone can be loose.

Write the matrix down when you start the mesh. Re-read it whenever a bridge entry surprises you.

---

## Shared-Ontology Surfaces

The third kind of storage — and the most under-described piece of multi-agent personal-LLM systems.

When the same content interest overlaps a stable subset of agents, force-fitting it into a single agent's ontology produces awkward bridging back and forth. The pattern is to give that intersection its own shared surface, with explicit membership.

Concrete examples:

- **Professional development across personal and work agents.** Goals, plan, evidence, contacts — the content belongs to the person, not to either employer or personal domain, and both agents reason against it. Lives on a surface both agents reach.
- **Shared finances and family calendar across personal and partner agents.** Both spouses' agents need to read and write; neither agent privately owns it.
- **Health goals across personal, nutrition-coach, and training-coach agents.** All three reason against the same goal-set; siloing it to one would mean the others either reach in (violating sovereignty) or get stale copies via bridge.

The rule for what can live on a shared surface: **the strictest content rule of any participating agent applies.** If one participating agent lives on infrastructure where company-proprietary content is forbidden, that rule applies to the whole surface, even content that other participants could technically handle locally. The boundary is set by the most-restricted zone touching the surface.

A useful heuristic for whether shared content belongs on a given surface: imagine the most-restricted member receiving an audit on its infrastructure. Would the content embarrass them? If yes, it doesn't belong on the shared surface — cite-don't-copy, or keep it in the more-restricted agent's private storage and bridge sanitized references only.

Don't proliferate surfaces. Each one is operational overhead. The test for whether an intersection earns a shared surface: are you bridging the same content back and forth three or more times a month? If yes, the intersection is real and stable, and a shared surface saves work. If no, keep using bridges and accept the duplication.

---

## Human-in-the-Loop Slider, Per Pair

Whether outbound bridge writes require human review is a deployment knob — and the choice constrains which transports work for the pair, so it has to be named before the transport menu. Three positions, set per pair:

1. **Per-entry review.** Every outbound write is reviewed by the human before the peer can see it. Highest friction; most auditable. Use for high-trust-cost pairs (cross-organization, regulated industries, vendor ↔ customer with contract obligations, or any pair you don't yet trust the sanitization rules on).
2. **Periodic review.** The agent writes freely to a staging area; the human approves batches on a cadence (daily, end-of-week, whenever a notification fires). Medium friction; the human eyeballs everything but in batches rather than one at a time. Good for pairs that cross trust zones when per-entry review is overkill but you still want eyes on what's leaving.
3. **Direct.** Agent writes become visible to the peer without any human action; audit is post-hoc via the transport's log (git history, object versions, queue history, mail archive). Lowest friction. Right for pairs inside a single trust zone, or for cross-zone pairs once the sanitization rules and receiver-applied judgment have been rehearsed enough that you trust the system to catch mistakes downstream.

Different pairs in the same mesh can sit at different positions. Personal ↔ work at per-entry review; personal ↔ thesis-coach at direct. Set the position deliberately at deployment time and revisit if a sanitization mistake makes it through — the right response to a leak is usually to move that pair one position up the slider, not to add new rules.

Not every transport supports every position natively. The transport menu below has a column showing which positions each option supports; pick a transport that supports the position the pair needs, or move the pair to a position the transport can handle.

---

## The Transport Menu

How does a write to an outbox by agent A become visible to agent B? Any transport works as long as it meets the contract below. Pick the one that fits your operational complexity tolerance.

Two kinds of friction matter and they don't track each other. **Setup friction** is what it costs to stand the transport up the first time — accounts, infrastructure, conventions. **Operational friction** is what it costs to use it once it's running — does each entry require manual handling, or is the path automated? Email-to-self has zero setup friction (you already have it) but high operational friction (every entry is a manual copy/paste). A message queue is the inverse. Pick the row whose combined cost you can actually pay.

| Transport | Setup friction | Operational friction | When it fits | Human-in-the-loop modes |
|---|---|---|---|---|
| **Email-to-self** | None — you already have email | High — every entry is a manual copy/paste between inboxes | One human, two devices, no infrastructure. Bridge entries are message bodies. | Per-entry review is **inherent** — you relay each message yourself. Direct mode isn't really achievable; this transport is human-mediated by design. |
| **Shared cloud-sync folder** (Syncthing / Dropbox / iCloud Drive) | Low — install a sync client on both ends | Low — sync is automatic once configured | Small mesh inside one trust zone; near-real-time sync; no git discipline needed | `drafts/` subfolder for per-entry review; batched promotion for periodic; or direct write to the synced outbox. |
| **Shared git repository** | Medium — repo, auth, commit conventions | Low — auto-commit + auto-push handles the loop once running | Multi-device, multi-zone, auditability matters. This is what most working setups use. | PR + merge for per-entry; stage-only + batched commit/push for periodic; auto-commit + auto-push for direct. Full slider available. |
| **Object-storage drop box** (S3, R2, GCS) | Medium — bucket, credentials, prefix conventions | Low — programmatic reads and writes | Cross-org, no shared git, want a programmatic write path | `pending/` → `live/` prefix promotion for per-entry; batched promote for periodic; direct write to `live/` for direct. |
| **MCP server-as-bridge** | Medium-high — stand up and host a server | Low — typed API once running | Real-time, agents are short-lived, you want a typed API | Server-side approve action for per-entry; approve-queue cleared on cadence for periodic; immediate exposure for direct. |
| **Message queue / pubsub** (NATS, Redis streams, MQTT) | High — broker, auth, topic conventions | Low — publish/subscribe handles the loop | Many agents, high write rate, you've outgrown polling | Per-entry review **impractical at real-time rates** — gating each message defeats the point of the queue. Periodic via a batched moderation pass; or direct publish. |
| **HTTP webhook / intake API** | High — endpoints, auth, deployment per agent | Varies — direct POST is automatic; human-relayed intake adds steps per entry | Cross-org with no shared infrastructure; agents have public endpoints | Human-relayed intake (e.g., Slack approval before forwarding) for per-entry; daily relay sweep for periodic; direct POST for direct. |

The protocol on top is identical in every case. Only the mechanics of "A writes," "B reads," and "where the human can stand in between" change.

For your first mesh, start with whichever transport you're already operating. If you live in Dropbox, use Dropbox. If you have a git habit, use git. The transport choice is reversible — you can swap it later without rewriting the agents.

## Transport Contract

What every transport must guarantee:

1. **Durability of the outbox.** Entries are not lost between write and read.
2. **FIFO ordering within a pair.** B sees A's entries in the order A wrote them.
3. **Visibility delay acceptable to the use case.** Real-time chat needs seconds; weekly-brief coordination tolerates hours.
4. **Two-way.** Every pair has a path in each direction.
5. **Auditability.** The human can inspect what was written and when, after the fact.

Things you do *not* need: transactional semantics, exactly-once delivery, sub-second latency, high throughput. Personal-LLM mesh traffic is low-volume by definition.

If a candidate transport meets the five guarantees, it works. If not, find a different one or build a thin shim on top of it (e.g., adding append-only ordering on top of an unordered object store).

---

## Bootstrap Extensions

When growing from one agent to n, the bootstrap conversation gets a few extra questions:

- **Which agents will participate?** Name them and their roles. Where does each one live (which zone, which infrastructure)?
- **What's the topology?** Hub-and-spoke is usually right. If anything else, why?
- **What shared-ontology surfaces are worth standing up?** Walk through the content interests that overlap multiple agents. Be skeptical — most intersections aren't stable enough to earn their own surface.
- **What transport?** Start with what you already operate.
- **What's the trust matrix?** Per pair, what content is allowed, what sanitization applies, and where on the human-in-the-loop slider does it sit?

After the user answers, the bootstrapping agent generates the shared spine (rules, schemas, settings), creates the bridge files for the pairs that need them, sets up the shared surfaces, and writes a short trust-matrix document into the spine for reference.

---

## Two Worked Examples

**Example A — Two agents, two zones.** Personal-life agent on home infrastructure, work agent on employer infrastructure. Hub-and-spoke is moot at n=2 (single edge). One shared-ontology surface: professional development (overlaps both, no employer-proprietary content allowed). Transport: shared git repository on a personal GitHub account (the only host both zones can reach). Trust matrix: heavy sanitization both directions; direct because the air gap plus content rules carries the load. Outcome: two sovereign systems, holistic coaching across work and personal life, no personal data on employer hardware.

**Example B — Three agents, one zone.** Hub: a general thinking-partner agent. Spokes: a thesis coach, a training coach. All three run on the user's own infrastructure. Hub ↔ thesis bridge for schedule/energy/blockers; hub ↔ training bridge for sessions/recovery/race-readiness. Two shared-ontology surfaces — hub ⊕ thesis holds thesis goals and milestones; hub ⊕ training holds the training plan and race calendar. The training and thesis specialists don't talk to each other directly. Transport: a Syncthing folder shared between three local processes (no git needed inside one zone). Trust matrix: light sanitization both directions; direct everywhere. Outcome: three voices tuned to three roles, coordinated through the hub, no cross-coaching pressure where it doesn't belong.

---

## Cautions and Pitfalls

The honest list, on top of the single-agent cautions:

- **LLMs are leaky.** Sanitization is the human's responsibility on each write. Belt-and-suspenders (topological partition where possible plus content rules) reduces but does not eliminate the residual risk.
- **Receiver-applied judgment is harder than it looks.** Models bias toward agreeing with confident-sounding peer input. Without explicit prompting to disagree, they tend to absorb. The "flag disagreement" instruction in the rules is doing real work and must be rehearsed regularly. With n agents, this gets worse: confident claims propagate further before anyone pushes back.
- **Bridge growth is quadratic past 4 agents.** N agents means up to n(n-1) directional bridges. Hub-and-spoke prevents the explosion; mesh does not. If you're heading past 4 agents on a full mesh, you have already failed to pick the right topology.
- **Trust matrix decay.** The matrix you wrote down at bootstrap will drift out of date as the system evolves. Re-read it quarterly. Surprise bridge entries are the symptom of a stale matrix.
- **Anthropomorphic drift compounds.** Each agent has its own persona discipline; cross-agent reflections amplify any one agent's drift. Surface mismatches between agents' takes on the same situation — they're the leading indicator.
- **The cold-start problem doubles.** "First month is sparse" was already punishing UX with one agent. With two, the bridge stays empty for weeks before there's anything real to exchange. Don't manufacture entries to fill it.
- **One human, multiple agents, divergent timestamps.** When the same observation arrives at the hub from two specialists with conflicting framings, the hub has to reconcile. Provenance tags make this possible; without them you can't tell which agent saw what when.

---

## License

Released under [Creative Commons Attribution 4.0 International (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Adapt it, fork it, rewrite it, rename it, build something commercial on top — all fine. Just credit the original. **No warranty, no liability.** You build the system at your own risk; you operate it at your own risk.

---

## Make It Yours

The right shape of a mesh emerges from your actual zones, your actual specialists, your actual overlaps — not from a template. Most of what's described here will be overkill for any specific user; pick the pieces that match the situation you actually have. Two agents in two zones is a lot; four agents is more than most setups need; six is almost certainly a sign you're solving the wrong problem.

If a section here doesn't fit your case, drop it. If something obvious is missing for your shape, add it. The supplement is a starting catalog of moves, not a prescription. The mesh you end up with should be just complex enough to do its job and no more.
