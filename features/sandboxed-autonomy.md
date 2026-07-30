# Feature: Sandboxed Autonomy

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md).

**Status: optional, and the highest blast-radius feature in this catalog. Read the caution below before adopting.**

---

## What This Adds

Most agent setups run permission-gated: the agent proposes an action, you approve it, it runs. That's the safe default, and it should stay the default for anything touching production systems, other people's data, or irreversible operations.

But for a genuinely personal deployment — a machine that's yours, that only affects your own stuff — permission-gating every single action has a real cost: it turns the agent back into something you have to supervise constantly, which undercuts a lot of the point of running one in the first place.

The alternative: give the agent its own sandbox — a VM, an LXC container, a dedicated machine — with real privileges inside that boundary (including, if you want the full benefit, unattended `sudo`), and let it operate without a permission prompt on every step ("YOLO mode"). The sandbox is what makes this safe enough to consider: if the agent makes a mistake, the blast radius stops at the boundary of that isolated environment, not your whole digital life.

## Isolation Alone Isn't the Full Feature

A perfectly isolated agent is also a perfectly *useless* agent — it can't touch anything that actually matters to you, which is most of the point of running one. The sandbox has to have deliberate, narrow doors out to the things you actually want it reaching: your calendar, your task manager, specific home-network services, specific external APIs.

That's a distinct, second feature: a controlled way to grant an agent scoped, revocable, auditable access to specific external systems — short-lived certificates rather than standing credentials, a human-approved request-and-grant flow rather than a permanently-open door. One published reference implementation of this pattern is [jit-ca](https://github.com/brian-spackman/jit-ca) — a just-in-time certificate authority built specifically to let a sandboxed agent reach a few real machines on request, with a time-boxed, revocable grant instead of a standing key. Read it if you're adopting sandboxed autonomy and want the "safe doors out" half solved rather than improvised.

## The Actual Tradeoff

This is genuinely the highest-leverage feature in the catalog if your goal is an agent that does real, unattended, multi-step work rather than answering questions one at a time. It's also genuinely the one where a mistake costs the most. Before adopting:

- Make sure the sandbox boundary is real — a container escape or a shared filesystem with your main machine defeats the entire point.
- Have a real backup/snapshot story for the sandboxed environment, independent of the agent's own judgment about when to be careful.
- Treat any door out of the sandbox (the jit-ca pattern or equivalent) as its own security surface, reviewed with the same care you'd give a production credential — because functionally, that's what it is.

This is not a feature to adopt on day one. Get the core system working with normal permission gating first; add sandboxed autonomy once you trust the agent's judgment and have the isolation story actually in place, not just planned.
