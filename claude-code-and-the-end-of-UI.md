---
layout: post
title: Claude Code and the End of UI
date: 2025-11-15
---

I've been thinking a lot about how humans will eventually interact with software in a few years. Currently we interact with software through GUIs - clicking, scrolling and typing on our computers, tapping buttons, scrolling and swiping on our phones.

It's very likely that AI is going to enable "intent-based interaction". For example, when I want to buy something on Amazon, I shouldn't have to open the Amazon website, search for the item I want, check reviews and Google a bit for which one to buy. It should be an end-to-end experience where I simply state "I want to buy X, with a budget of Y and want features of Z, recommend top 3 options for me to choose". Then I just choose one, and AI takes care of filling up the address, payment, etc.

## Breaking down the architecture

Let's break that interaction down into different layers to understand what's actually happening.

**Layer 1: Human intent**
This is where humans state what they want. "I want to buy X with budget Y and features Z." We're not telling the system how to do it - we're just saying what we want done.

Currently we handle this orchestration in our brains. We decide which app to go to for specific use cases - we go to Google when we want to search things, we go to Instagram when we want to check what our friends have been doing, we text people on WhatsApp. This leads to more and more apps on our devices because every specific use case has an expert app for it. In the future, AI should handle this orchestration for us.

**Layer 2: Lead orchestration**
When the lead orchestrator takes the intent from the human, it needs to figure out which systems to talk to. For the Amazon example, it needs to route the request to shopping platforms, review aggregators, payment systems, and shipping services. It's translating high-level intent ("buy this thing") into a plan that involves multiple specialized systems.

**Layer 3: Niche orchestration**
Each system has its own internal logic. Amazon needs to search its catalog, rank results, check inventory. The review system needs to aggregate scores and filter relevant feedback. The payment processor needs to validate your card and process the transaction. Each of these is a specialist taking a piece of the overall intent and executing it.

Currently this niche orchestration is also controlled by users. If I go to Booking.com, I manually click a lot of buttons to select the dates and location of my trip, and my desired settings like price and quality, then I go through results one by one and check user reviews to make my decision. In the future, I expect niche orchestrators to only return results that closely match user intent back to the lead orchestration layer.

**Layer 4: Execution primitives**
This is where actual work happens - APIs, database queries, functions that do the real operations. Amazon's search API, Stripe's payment API, address validation services. Without this layer, nothing actually executes. The orchestration layers above are just planning and routing; this layer is where rubber meets the road.

Each layer translates higher-level intent into lower-level operations until you get to something that can actually execute.

## Claude Code as the blueprint

After breaking these layers down, you see something very familiar - that's right, Claude Code with sub-agents and skills.

In Claude Code, users chat with the main orchestrator to state our intent - what we want this codebase to do, what our plan is, what changes we need.

The main orchestrator then decides how to approach the task. It might handle simple requests directly, or it might call sub-agents for complex exploration, or it might invoke skills for specialized workflows (the yaml gets loaded into context so it knows what's available).

Sub-agents and skills are the niche orchestrators. The Explore agent specializes in understanding codebases. The Plan agent specializes in breaking down implementation steps. Skills specialize in domain-specific workflows like generating meeting notes or creating new skills. Each one takes a piece of the overall intent and figures out how to execute it.

Finally, they all use tools - Read, Edit, Write, Bash, Grep, etc. These are the execution primitives. They're the APIs of the filesystem and terminal. They actually do the work.

So the mapping is:
- **You** → state intent ("refactor this to use async/await")
- **Main orchestrator** → plans approach, decides if it needs sub-agents
- **Sub-agents/skills** → execute specialized workflows
- **Tools** → perform actual operations (read files, edit code, run commands)

This is already the four-layer architecture working in practice.

## The endgame

Here's what's really interesting: there's no GUI needed for Claude Code. You never clicked a "refactor" button or opened a "code analysis" panel. You stated intent, and it executed directly through tool use.

That's the actual endgame for how humans interact with software. UIs exist because humans need visual representations to make decisions and navigate complexity. Once AI can reliably translate intent into execution, the UI layer becomes optional overhead, not a requirement.

Right now we're in a transition state where AI assists us in using GUIs. But the final state is intent → execution, with UI only when you explicitly want to see what's happening.

Software becomes pure capability, not a visual representation of capability. You don't interact with representations of actions (buttons, menus, forms). You just state what you want, and the capability executes.

Claude Code isn't just a better way to interact with code. It's demonstrating the pattern for how humans will eventually interact with all software. 