---
layout: post
title: The AI-Native Playbook
date: 2026-07-17
---
Practical companion to [The AI-Native Way to Run a Traditional Business]({{ 'the-ai-native-way-to-run-a-traditional-business' | relative_url }}). The thesis says what an AI-native business is; this says how I would install one in a real company — the Edgera model: buy the business, install the OS. Everything here comes from an architecture I already run daily. Where something is not yet proven at company scale, I say so.

Two terms from the thesis, used throughout: **the layer** — the company's knowledge and records as one system agents read and write (files + the existing ERP/CRM); **exhaust** — records the layer captures automatically as a byproduct of doing the work, no separate documentation step.

## The premise

The tech is the smaller problem. Knowledge management failed for twenty years on adoption and incentives, not tooling. This playbook is mostly about people; the stack gets one section.

## The three roles

Three roles, not a task force. Two are hats, one is a hire-or-contract.

**1. The owner.** Top-down or nothing — but top-down means the owner has a part to play, not just power to grant. Three duties that cannot be delegated:

- Change compensation: work that doesn't flow through the layer doesn't count toward pay or bonus.
- Go first, visibly: the owner's own decisions and questions run through their agent before anyone else is asked to change.
- Hold the line: when the top sales guy passive-resists, only the owner's authority resolves it.

Delegate these and the adoption lead becomes a staff person pushing a tool — the project dies the way every knowledge-management project dies.

**2. The adoption lead.** One business person with owner-granted authority (in Edgera's case, me or Jett). Not a tech role. The craft is **skillification**: sit with the veteran, watch how she actually qualifies a supplier or builds a quote, distill it into a skill the agent executes. The loop is mechanical:

- Someone does a task twice → adoption lead writes it as a skill → third time, the agent does it.
- Enforce the loop until it becomes culture; then department champions (see interface ladder) skillify their own departments.

Owns the KPIs (below). Full-time during rollout, then recedes.

**3. The platform owner.** Not "a security person" — security is one duty of a builder-operator role: keep the system running, set who can read and write what, keep the audit trail, swap models, control cost, back everything up. Part-time or contracted for a 20-person SME. In the multi-acquisition play this is the leverage point: one platform owner serves every portfolio company, because the OS is the same.

## The methodology

**Two steps, strict order: make the agent useful first, make it mandatory second.**

1. **Useful first.** In the first weeks the agent only gives and asks nothing back: it drafts follow-ups, recalls client history, preps meetings. Each person feels "this saves me time" before the company demands anything of them.
2. **Mandatory second.** Once people already work through the agent because it's faster, the owner flips the rule: a quote, PO, or client record officially exists only if it went through the layer, and work outside the layer doesn't count for comp.

Wrong order kills it. Mandate first and people fake it — they chat with the agent for show while doing real work the old way, and nothing real gets captured.

**One department first.** Pick the one with the most repetitive external communication (usually sales or purchasing). Build its context + skills, wire its agent to the existing CRM/ERP. The 90-day goal is proof: show the owner a written record of client/supplier knowledge that until now lived only in employees' heads. Then expand along the process chain; each new department multiplies the layer's value because handoffs between departments start flowing through it.

**The interface ladder.** Chat is the onboarding interface, not the ceiling. Three rungs, all sessions on the same harness and org layer — the interface changes, the layer doesn't:

1. **LINE chat** — everyone starts here; zero learning curve. Most employees stay here permanently, and that's success: the harness does the heavy lifting behind them.
2. **Rendered surfaces** — the read side: per-role dashboards and digests the server regenerates.
3. **Direct harness access** (terminal / Claude Code / Codex-style sessions on the org repo) — for the minority who ask for more on their own: "can it do X every time?" That self-driven demand, not a schedule, is what earns the upgrade.

Rung 3 produces **department champions** — they start writing their own skills, and skillification stops depending on the adoption lead. The trap: sideways moves. Handing eager users personal ChatGPT/Claude subscriptions feels like an upgrade but is a regression — a personal account isn't connected to the company's layer, so their best work stops being captured and knowledge goes back into heads. Upgrades go up the ladder, never sideways to disconnected tools.

**Skillification cadence.** Weekly, the adoption lead reviews what people actually asked their agents (the transcripts are the discovery tool): repeated asks become skills, bad answers become context fixes, unused agents become conversations.

## The metrics

Don't measure adoption by who chats with the agent — a mandate makes everyone chat, so the number proves nothing. Measure what the layer actually captured. One number per question:

| Question | Metric |
|---|---|
| Is the layer becoming the business? | **Write-path coverage** per process: quotes issued through the agent / total quotes |
| Is knowledge being distilled? | **Skills shipped per month** |
| Is it self-interested yet? | **Time-to-first-value** per employee: days from onboarding to the first real hour saved |
| Ready to let agents work unsupervised? (the thesis's Phase 2) | **Exception rate** per process: how often the routine case turns out not to be routine, measured from captured records |

Time-to-first-value is the leading indicator: if people don't feel the agent saving them time early, the coverage numbers will be faked no matter how hard the owner pushes.

## The stack

Five pieces. One real build.

1. **One always-on server** — a Mac mini in the office or a small cloud server; either covers a 20-person SME.
2. **The org repo** — the data + context layers as files: org context, department context, per-user context, skills, unstructured data. Bridges into the existing ERP/CRM (agents use the same interfaces staff do; nothing gets ripped out).
3. **A model-agnostic harness** (e.g. Hermes) — the software that runs the agents. One install; every conversation starts with the right context for whoever is talking (company + department + personal). Model-agnostic means the underlying AI (Claude, GPT, others) can be swapped — the hedge against any single vendor's pricing or terms.
4. **The LINE gateway** — the only real software to build, and it's small: LINE user ID → user config → that user's scoped session. Employees just chat; zero learning curve, in the app they already live in.
5. **Approval + audit built into the system** — not left to people's discipline. High-stakes writes (pricing, commitments, anything client-facing) pause automatically and ping the record's owner on LINE to approve or reject. Every write logged.

Two honest limits of chat-only:

- Chat is the best way to put work in and the worst way to get an overview out. The PM's all-projects view and the owner's dashboard need one read-only page (a web page the server regenerates, or a daily per-role digest). Don't pretend chat covers the read side.
- A conversation that ends without writing anything to the layer captured nothing. The fix: when a conversation ends, the system automatically extracts the records in it (a client preference, a quote sent, a delivery date slipped) and files them. This is the machinery behind "exhaust, not homework" — invisible to employees, which is the point.

## Access sequencing

What an agent knows and what it may touch are the same boundary: the sales agent reads sales, not finance. The platform owner's access expands with the rollout — full access to what's live, finance last, with the audit trail earning each expansion.

No owner should hand anyone full access to their stack on day one — and the sequencing above is why they never have to. Access follows the rollout, the books come last, and the audit log is what earns each step. It is also why the install is more credible in a company you own than in one you advise: as owner-operators we face the easiest version of the trust problem.

Non-technical users can't tell a wrong answer from a right one. The permission structure is what makes the system safe for someone who trusts it completely: the agent may be wrong in chat; it must not be able to be wrong in the ledger without a human signature.

## Economics

- **Starting out:** subsidized consumer subscriptions (Codex-class) make per-seat cost trivial while the ROI is being proven. But don't build the plan on the subsidy lasting — per-seat terms, rate limits, and the subsidy itself can vanish with one pricing change.
- **Long run:** pay-per-use API keys once value is proven. Because the harness is model-agnostic, the switch is a settings change, not a migration.
- **Cost centers:** platform owner (part-time), adoption lead's time (heavy at the start, then tapering), server (one-time). The expensive input is the adoption lead's attention, not the AI usage.

## Where this stands today

The fair question is: where's the case study? Straight answer, in three parts.

**What runs today.** My own operation, on exactly this architecture: an org layer of files plus structured data, layered company/department/personal context, procedures captured as skills an agent executes, work captured as a byproduct of doing it. Two machines, one always on, agents coordinating through the same layer, in daily production for months. Small, but real — this document was produced by that system.

**What is not yet proven.** The same install across a company of employees: the incentive problem at scale, the adoption curve, non-technical users trusting a system they can't debug. Nobody has many-year case studies here; the tools this depends on are barely two years old. That cuts both ways — it's why the opportunity exists and why it can't be de-risked by waiting for someone else's proof.

**How the proof gets made.** The first install is the case study, and it's designed to fail fast if it fails: one department, 90 days, and the metrics above (write-path coverage, time-to-first-value) are deliberately measurable from the start. If the exhaust isn't visible at day 90, we'll know early and cheaply — that's the accountability instrument, for us and for anyone backing us.
