# Feature: Batched Task Triage

A supplement to [`idea-file_arcee.md`](../idea-file_arcee.md). Pairs naturally with [async batched execution](async-execution.md), but solves a different problem: not "let the agent work while you're away," but "don't make the human the bottleneck one interruption at a time."

**Status: optional, and one of the more broadly useful features in this catalog for anyone juggling several ongoing threads of work with an agent.**

---

## The Problem It Solves

In normal serial agent work, you become the bottleneck in a specific, annoying way: a thread of work runs until it hits a step only you can do — approve something, provide a credential, make a judgment call — and because that step is often several moves into the thread rather than the very next action, the whole thread stalls and gets set aside. You end up getting contacted reactively, one interruption at a time, as each thread separately reaches its own blocking point.

## The Inversion

Instead of waiting to hit blocking steps one at a time, have the agent read across *all* current threads of work, project each one forward to completion, and extract every human-required step in advance — including steps that are several moves out, not just the immediate next one. Then group those extracted steps by the *context* you'd actually be in when you do them, GTD-style: an "at a computer" batch, a "on your phone" batch, a "pure decision, no tooling needed" batch.

You clear an entire batch in one focused sitting instead of getting pulled in repeatedly. Each cleared item can unblock one or more threads for the agent to keep running on its own.

## Why This Is a Real Multiplier, Not Just Organization

The value isn't just tidiness — it changes the shape of the collaboration. One short, focused sitting at a computer can unblock several separate threads instead of five separate mid-task interruptions spread across a day. You go from being a reactive, serial blocker to something more like a batch oracle: the agent brings you a curated set of decisions and actions, you clear them together, and it goes back to running several threads in parallel against what you just unblocked.

## How to Represent It

A simple, queryable convention works well: give the agent plain bullets for its own actionable steps, and give you checkboxes for the steps only you can do — tagged with the context they need (`#computer`, `#phone`, `#decision`). If your note-taking tool has any kind of task-query plugin, this means a filtered view of "everything only I can do, grouped by where I need to be to do it" is always one query away, without the agent's own steps cluttering the view.
