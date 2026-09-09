# Graph Engineering explained — summary & explanation

- Source article: https://x.com/AnatoliKopadze/status/2080668775796314331
- Author: Anatoli Kopadze
- Posted: 2026-07-24
- Full copy: [article](2026-07-24-anatoli-graph-engineering.md)
- Companion video (Google, ~60 min, posted 2026-09-08): https://x.com/AnatoliKopadze/status/2097380989538591155

## Gist

Anatoli frames **graph engineering** as the next skill after single-agent **loops**: not one agent improving one metric in a cycle, but a **network of jobs** (nodes) connected by real data dependencies (edges). The payoff is breadth and parallelism, not better judgment. Most “workflows” people write are already graphs — just the worst shape, a straight chain.

## Core vocabulary

| Term | Meaning |
| --- | --- |
| Node | One bounded job: one agent, defined input, defined output (a **contract**) |
| Edge | Real dependency: next job needs the previous job’s artifact |
| Fake edge | Ordered only because you typed it that way; no data flows → can run in parallel |
| Diamond | Fan out → reduce (often plain code) → synthesize; the default useful pattern |
| Checker / verifier | Separate node, **fresh context**, tries to kill bad findings before merge |
| Anchor | Ground truth that cannot be argued with (real tests, banked revenue, frozen rules) |

## The fake-edge test

For each step: *does this step need the previous result?*  
Yes → keep the order. No → delete the wait and run in parallel.  
Claim: almost any linear agent script hides 2–3 fake edges; cutting them is free latency.

## Why chains hurt

A 40-step line has 40 sequential failure points and latency = sum of all steps.  
The same work as a graph has only the real dependencies (often a few layers) and finishes at the speed of the slowest layer. **The model was not the bottleneck; the line was.**

## Diamond pattern (fan out / reduce / synthesize)

1. Fan out independent workers (breadth).  
2. Reduce / compress with cheap code or batching (context hygiene).  
3. Fresh verifier(s) on separate context.  
4. One strong synthesizer writes the final answer.  

Claude’s research feature and Claude Code “workflow” prompting are presented as production diamonds: coordination as **code**, so handoffs do not re-spend chat context.

## Checker rule

Self-review is weak. Worker and verifier must **never share context**. Split checks: correct? current? source real?

## Where graphs break

1. **Context collapse** — fan-in of raw piles; fix with layered summarize-then-merge.  
2. **False independence** — shared files / rate limits = hidden edges (Bun multi-agent overwrite example).  
3. **Silent node failure** — merge must count expected inputs vs received.

## When *not* to use a graph

Small/isolated tasks; you want to approve every step; exploratory work with unknown goals; truly sequential dependencies; fake-edge test finds nothing to parallelize → stay with a loop.

## Anchors (the hard part)

A graph of mutual auditors can be **consistently wrong**. Topology ≠ truth. Need anchors: tests that actually passed, numbers that hit the bank, rules an optimizer is not allowed to weaken.

## Cost / supervision

Graphs cost more tokens. Public Bun rewrite anecdote: ~535k→1M+ lines, ~11 days, ~50 workflows, up to 64 agents, ~$165k usage, heavy human design — and debate over reviewability. Start small; widen only after a run earns it.

## Practical takeaway

Tonight: draw your current workflow, delete edges that carry no data. Learn when work is **wide** enough for a fleet vs when a single loop is enough.

## Relation to this repo

Pairs with Anthropic “loops & graphs” handbook and the Google ~60 min graph-engineering talk Anatoli shared later. Article = practitioner framing + Claude Code paste recipes; video = from single agent to 24/7 system (chapters in video tweet).
