---
layout: post
title: AI Software Questions
date: 2025-12-24
---
## What This Document Is

A working list of questions I'm asking myself to develop a clearer view on AI investing. For each question, I document my current thinking—not as final answers, but as positions to stress-test and update as the space evolves.

## AI Endgame & Architectural Understanding

### How will a user interact with software in 5–10 years - what are the stacks and how do they work?

>**The agentic system stack**

>![](image/Pasted%20image%2020251218114018.png)

>- **User interaction**
>	- Primary interfaces shift toward multimodal inputs: speech, text, camera/video, and contextual signals from the environment.
>	- Traditional GUI remains, but most workflows begin with natural-language intent ("prepare the board pack", "analyze this dataset", "draft a contract consistent with our past versions").
>	- Many tasks become agent-initiated or agent-augmented (pre-drafting, background monitoring, auto-execution of routine tasks).
>- **Orchestrator**
>	- A persistent system-level agent sits close to the OS.
>	- It maintains awareness of identity, files, apps, screen context, and preferences.
>	- It interprets user intent, constructs structured tasks, and determines which models, tools, and vertical systems should be involved.
>	- It enforces permissions, privacy boundaries, and cross-application coordination.
>- **Planning layer**
>	- The orchestrator (or a planning sub-agent) converts intent into a task graph: subtasks, tool calls, dependencies, and checkpoints.
>	- This layer handles error recovery, long-horizon sequencing, and when to involve the user for approval or context clarification.
>- **Tools and execution agents**
>	- Domain-specific agents handle specialist actions: data analysis, code generation, CRM operations, finance workflows, document drafting, etc.
>	- Many of these agents are embedded inside existing SaaS products rather than standalone apps.
>	- Agents interact through structured APIs and capability endpoints ("create invoice", "generate SQL", "prepare shipment label").
>- **App layer and data**
>	- Vertical applications increasingly expose both data and actions programmatically.
>	- The UI becomes thinner; capabilities are invoked by the orchestrator on the user's behalf.
>	- Compliance, audit trails, and domain-specific correctness remain controlled by the vertical systems.
>- **State and memory**
>	- The system maintains short-term and long-term memory: ongoing tasks, drafts, preferences, prior interactions, and cross-app context.
>	- This memory is shared across orchestrator and key vertical systems, with strict privacy and enterprise permissioning.
>- **Overall user experience**
>	- Users continue to open individual apps for certain workflows, but a growing portion of work is delegated: declare intent → agent plans → agents execute → user reviews → agent refines.
>	- The cognitive load shifts from "how to do the task" to "what outcome is desired".
>
>**Agent loop**
>
>![](image/Pasted%20image%2020251218115025.png)
>
>An agentic system operates in a continuous loop across three stages. Each stage feeds into the next, and the loop repeats until the task is complete or escalated.
>
>**1. Think**
>- Understand user intent from multimodal inputs (text, speech, gestures, screen context)
>- Resolve ambiguity: ask clarifying questions or infer from prior interactions and preferences
>- Convert intent into a structured task with success criteria
>- Decompose the task into subtasks with dependencies and sequencing
>- For each subtask, identify relevant context (files, APIs, prior outputs, memory)
>- Select tools and determine execution strategy (parallel vs. sequential, which agents to invoke)
>
>**2. Act**
>- Execute subtasks according to plan, invoking tools and APIs as specified
>- Handle failures gracefully: retry with backoff, try fallback approaches, or flag for replanning
>- Maintain execution state: track completed steps, pending steps, intermediate outputs
>- Enforce guardrails throughout: permissions, cost limits, rate limits, safety checks
>- Stream progress to user when appropriate (for long-running tasks)
>
>**3. Observe**
>- Validate outputs against expected format, type, and quality thresholds
>- Detect errors, inconsistencies, hallucinations, or incomplete results
>- Decide next action:
>   - **Proceed**: output is acceptable, move to next subtask
>   - **Retry**: transient failure, re-execute current step
>   - **Replan**: output reveals the plan was flawed, return to Think
>   - **Escalate**: uncertainty too high or guardrail triggered, ask user for input
>- Update short-term memory with results; persist relevant learnings to long-term memory
>
>The loop is not always linear. Complex tasks may spawn nested loops (sub-agents running their own Think-Act-Observe cycles). The system must track state across nested loops and reconcile outputs. 

### What are the gaps today to reach that endgame?

>- **Intent understanding**: Interpret what the user actually wants.
>  Gaps: Long instructions still required; models struggle with ambiguous intents; weak adaptation to individual preferences.
>- **Planning and task decomposition**: Transform intent into a structured workflow or task graph.
>  Gaps: Inconsistent decomposition; hallucinated steps; poor error handling; weak long-horizon coordination.
>- **Tool selection and execution**: Choose appropriate models to solve each subtask based on complexity, call relevant tools (SQL, Python, API calls), and execute them reliably.
>  Gaps: Poor model routing; fragile schema handling; inconsistent tool-use protocols; high sensitivity to minor tool changes.
>- **Modality**: Text-based interaction is inefficient. Users should be able to prompt and provide context via speech and camera. Agents should autonomously gather context and suggest next actions.
>  Gaps: Speech input has made progress, but visual context (screen, camera) remains underutilized. Proactive context gathering is still rare.
>- **Dynamic context engineering**: Gather relevant data across documents, files, apps, screens, APIs, and prior interactions for each sub-task.
>  Gaps: Context gathering remains manual. Users must know what context to provide and how to provide it efficiently. The agent should know where to find context and what to pull automatically.
>- **Programmable prompt engineering**: Craft and refine prompts to get the best results from models.
>  Gaps: Prompt iteration is manual and tightly coupled to evaluation. Users modify prompts based on subjective judgment of outputs. Ideally, systems should evaluate results systematically and adjust prompts programmatically. Additionally, best practices differ across models and evolve quickly, making it hard to stay current.
>- **Evaluation and correction**: Grade outputs, detect errors, and enforce quality thresholds.
>  Gaps: No reliable method for evaluating subjective tasks; limited self-evaluation capability; poor rubric enforcement; subjective outputs are hard to verify.
>- **Memory (short-term and long-term)**: Retain previous tasks, drafts, user preferences, and recurring workflows.
>  Gaps: No true long-term memory. RAG provides retrieval, not learning. Personalization remains superficial. No continuous learning from interactions.
>- **Cross-agent communication**: Enable LLMs to communicate with each other and with applications. Anthropic's MCP is a promising step toward standardizing how agents discover capabilities and coordinate execution.
>  Gaps: Interoperability is still immature. Dominant platforms are reluctant to expose their capabilities to orchestrating agents, since doing so dilutes their control over user workflows. Those who resist will eventually be replaced by agent-native alternatives.
>- **Agentic coding**: Tools like Cursor and Claude Code are already generating code effectively.
>  Gaps: Pain points remain in codebase management (keeping code clean, scalable, and well-structured) and deployment workflows.

### What are the strongest reasons this endgame might not happen? 
>- **Technical constraints**
>	- Planning, long-horizon reliability, and error recovery may plateau. LLMs may excel at short tasks but remain brittle on complex workflows.
>	- Safe continuous learning and long-term personalization remain unsolved; without them, agents stay stateless or require heavy human configuration.
>	- Tool-use and schema-adaptation may not reach enterprise-grade robustness.
>- **Economic constraints**
>	- Multi-agent workflows are compute-intensive. If inference costs or latency do not fall as fast as expected, many end-to-end automated workflows may be uneconomical.
>	- Enterprises may cap automation levels to reduce infra complexity, debugging cost, and risk exposure, limiting "fully autonomous" scenarios.
>- **Regulatory and privacy constraints**
>	- Cross-app visibility and central orchestration may be restricted by privacy rules, data-localization requirements, and enterprise governance.
>	- OS vendors may deliberately limit screen access, keyboard events, permission scope, and automation APIs for safety/compliance.
>- **User-behavior and organizational constraints**
>	- In high-stakes domains (legal, medical, finance), organizations may enforce “human-in-the-loop” as mandatory.
>	- Users may prefer predictable workflows over opaque agents, slowing adoption of end-to-end automation.
>- If these constraints persist, the ecosystem skews toward powerful embedded copilots inside existing SaaS/OS platforms rather than fully autonomous cross-app agents.

### What capabilities do frontier models still need to reach for that endgame to work? Which are solvable vs. structural bottlenecks? 

>- **Reliability on known tasks: Solvable**. Improvements in model architecture, distillation, structured guardrails, and filtered training data should reduce variance and increase predictability.
>- **Planning and long-horizon reasoning: Partially solvable.** Pure LLM planning is unlikely to achieve high reliability; real progress depends on hybrid systems combining LLMs with structured planners, code execution, and explicit task graphs.
>- **Tool-use robustness: Solvable with better schemas, validation layers, and more consistent API abstractions.** This is primarily an engineering problem rather than a fundamental research barrier.
>- **Long-term memory and personalization: Hard.** Current approaches (RAG, external stores) provide retrieval, not actual stateful learning. Safe online adaptation without catastrophic forgetting is an open research challenge.
>- **Continuous learning: Uncertain.** Conceptually powerful but challenging due to safety, drift, and eval overhead. Production systems will likely rely on periodic controlled fine-tuning rather than unrestricted online learning.
>- **Interpretability and safety: Structural bottleneck.** Incremental improvements are expected, but full transparency into model behavior is unlikely. This limits adoption in high-stakes environments and slows autonomy.
>- Overall, reliability and tool use trend toward solvability; long-term memory, continuous learning, and interpretability remain structural bottlenecks shaping the ceiling of agent autonomy.

### How to properly evaluate AI apps' results? 
>- Objective eval is easy: create multiple prompt-to-correct-result patterns to allow the model to learn the patterns.
>- Don't have a good answer for subjective eval yet. Currently the best approaches seem to be LLM-as-judge and A/B testing via human voting.

## Value chain and defensibility

### Who owns the "state" of the user? Is it the Model Provider (OpenAI knows my chat history), the OS (Apple knows my screen), or the Vertical App (Marriott knows my hotels)? Who wins the right to context and routing? 

>- **OS and productivity suites** (Microsoft 365, Google Workspace, Apple ecosystem)
>  Own global state: identity, device context, files, email, search, calendar, and what is on screen. This gives them a structural advantage in routing and context assembly.
>- **Vertical applications** (CRM, ERP, developer tools, design systems, healthcare systems)
>  Own deep domain state: customer data, ledgers, codebases, medical records, operational workflows. They will expose both data and domain-specific actions but retain control of business logic and compliance.
>- **Model providers** (OpenAI, Anthropic, Google models)
>  Own state only inside their hosted workspaces and agent environments (e.g., ChatGPT Teams). When serving as backend models inside other apps, they have far weaker visibility and limited identity/context access.
>- **Enterprise-controlled data stores**
>  In corporate settings, much of the durable state resides in IT-owned data lakes, vector stores, and permissions-managed knowledge bases.
>- **Routing outcome**
>	- OS/prod-suite dominates default routing for cross-application tasks due to visibility and control.
>	- Vertical systems dominate routing inside their own domains.
>	- Model providers win routing only where they control the full user experience.

### Which layers become commoditized vs. remain defensible? 

>- **Commoditizing layers**
>	- Mid-tier models and generic inference APIs, driven by open source competition and scale economics.
>	- Thin "wrapper" applications that simply provide UI over a frontier model without workflow integration, proprietary data, or domain logic.
>- **Defensible layers**
>	- Vertical applications where correctness, integration, compliance, and workflow depth matter. Defensibility comes from proprietary data, domain knowledge, and operational embedding, not the model itself.
>	- Systems that accumulate proprietary structured data and user feedback loops, enabling continuous improvement in specific high-value domains.
>	- Potentially, orchestration/planning platforms that become embedded in enterprise workflows. This layer has high upside but is strategically contested by OS vendors, SaaS ecosystems, and cloud providers.

### Incumbents vs. disruptors: who will win in each area?

>The outcome depends on where a use case falls on these axes. One end favors disruptors; the other favors incumbents.
>- **Workflow redesign potential and autonomy**: When a workflow can be completely reimagined in an AI-native way (reducing human decision points, collapsing multiple steps, allowing agent autonomy), disruptors win. When the workflow must preserve existing structure and human checkpoints, incumbents win by adding AI as an enhancement layer.
>- **Distribution**: When the efficiency gain of a new interface outweighs switching friction, disruptors can build their own distribution (Google Search → ChatGPT/Perplexity). When workflows are deeply embedded in existing platforms, incumbents control distribution and disruptors must go through them (AI features inside Excel, not a new spreadsheet app).
>	- After winning the right for distribution, disruptors can then accumulate data efficiently. 
>- **Incumbent self-conflict**: When automation directly cannibalizes the incumbent's revenue model, disruptors have an opening (seat-based pricing vs. automation, hourly billing vs. outcome pricing). When incumbents can adopt AI without self-harm, they absorb the threat.
>- **Regulatory/compliance burden**: In heavily regulated domains (healthcare, finance, legal), incumbents with existing compliance infrastructure have an advantage. In lightly regulated domains, disruptors move faster without permission. 
>- **End-to-end niche workflows** (disruptor-only advantage): AI-native players can own complete workflows in niches that incumbents overlook. This builds user trust and proprietary data, creating a beachhead for expansion.

### What are the areas that will be captured by LLM providers vs. applications?

>- Conditions that favor applications:
>	- External systems are required: Workflows that are not just token-in/token-out require embedding proprietary external systems into the LLM as context (e.g., APIs, databases, devices, production systems)
>	- State persistence is important: Complex workflows that require persistence of state across the process (project management, multi-step workflows, team collaboration)
>	- Accountability: The more accountability solution providers need to take, the more favorable it is for apps (high-stakes tasks like legal, audit, compliance)
>- Examples that will likely be captured by LLM providers:
>	- Image/video/content generation: No external system required, stateless, low accountability (usually reviewed by humans)
>	- Drafting high-stakes artifacts without ownership: Legal contracts, investment memos

### Are vertical agents more VC-investable than general agents? Will vertical agents just end up being tools of the state owners (e.g., OS)?

>- Vertical agents look more VC-investable at the moment, as this is where disruptors have structural advantages. Startups begin by solving specific user pain points that are niche enough to be overlooked by large players, yet valuable enough that users will pay for results. They accumulate user base and trust, then expand via vertical integration (e.g., meeting note-taker → calendar manager) or potentially horizontal use cases if they build enough scale (though there's no good example of this yet).
>- The general agent game has far more strong contenders: OS vendors (Microsoft, Apple), device makers (Apple, Samsung), LLM providers (OpenAI, Anthropic, Google, xAI), and emerging players like ByteDance (via Doubao and Doubao Phone).
>- Will vertical agents become tools of orchestrators? Likely yes, but with varying degrees of leverage. Vertical agents that own irreplaceable data (user history, domain-specific corrections, proprietary workflows) or have deep system integrations can resist commoditization. Those that are stateless and easily substitutable become interchangeable tools that the orchestrator can swap at will.

### Will the AI era also end up being a winner-takes-all situation? 

>- The key gateway will likely converge to a few winners: the interface where users state their intent. This will probably be a device- or OS-level orchestrator, or a model provider embedded within one. Similar to Chrome in web browsers, but with a key difference: the orchestrator actively routes tasks, giving it leverage over downstream tools.
>- There will also be category leaders in specific domains: vertical agents that can execute tasks accurately and reliably. But they will likely function more as tools called by the orchestrator than as standalone products.
>- What enables a vertical agent to resist commoditization? Proprietary data that improves with usage (user corrections, domain-specific training), deep integrations that are painful to replicate, and workflows where switching costs are high (e.g., accumulated context, team habits, compliance configurations). Without these, the orchestrator can substitute one vertical agent for another. 

### What are the most important moats for AI applications? 

>- **Execution reliability**: Apps that consistently complete tasks accurately. Users pay for outcomes, not tools. Reliability is table stakes, but hard to achieve and easy to lose.
>- **Accumulated context**: User preferences, background information, correction history, and recurring workflows compound over time. The more context an app holds, the higher the switching cost. This is the AI equivalent of data lock-in.
>- **Domain-specific correctness loops**: Proprietary data and feedback mechanisms that improve accuracy in ways competitors cannot easily replicate (e.g., fine-tuned models on domain data, human-in-the-loop corrections that feed back into the system). 

## Business models and economics

### How fast does inference cost need to drop for AI application economics to work? What is a "safe" gross margin level for apps? Will users accept a token-based pricing model?
>- No answer yet. 

### What is the fundamental difference between internet apps, SaaS, and AI apps? What are the differences in evaluating deals in these different sectors?

>- **Internet apps**
>	- Primarily engagement-driven systems with zero marginal cost of replication.
>	- Value comes from network effects, distribution, user acquisition funnels, and content/interaction loops.
>	- Key evaluation metrics: retention cohorts, virality, LTV/CAC, user-generated content.
>- **SaaS products**
>	- Tools purchased to achieve predictable, repeatable outcomes. Human drives the entire process.
>	- Value comes from workflow embedding, data schema control, integrations, and switching costs.
>	- Evaluation metrics: net retention, depth of workflow integration, administrative control, unit economics, modular expansion potential.
>- **AI-native apps**
>	- Users pay for a result, not a tool: accuracy, speed, reduction in manual labor, and correctness. With or without human in the process.
>	- Core differentiator is not UI but:
>		- correctness and robustness
>		- data advantage
>		- quality of planning and tool use
>		- depth of workflow integration
>	- They behave more like "managed services delivered by software" than classical SaaS.
>- **Implication for evaluating deals**
>	- Must evaluate real-world accuracy, reliability, and iteration speed, not UI polish.
>	- Must assess whether the team can keep pace with frontier model change.
>	- Defensibility depends on:
>		- proprietary data
>		- workflow lock-in
>		- integration depth
>		- domain-specific correctness loops

## VC investment 

### What are the non-negotiable characteristics of an AI founding team, and how to practically test for them? And what are the red flags that non-technical or generalist funds often miss? 

> The team should have both strong technical capability (so they can adapt to model changes and iterate very quickly) and product management experience (so they can build apps that actually solve problems with good user experience).

### How to assess whether a founder and team can survive rapid changes in the model/provider landscape over the next 5–10 years?

> The founder doesn't necessarily need ML experience, but must have a strong fundamental understanding of how LLMs work and scientific research capability so they know how to build products on top of them.

### At which stage (angel, seed, A, growth) is the risk/reward best for AI software?

>- 

### What's the exit strategy for AI startups? Any examples of M&A or secondary transactions?

>- 
## Personal AI stack 

### What models, tools, or agents do I use day-to-day, and what recent experiment has materially changed how I work?

>- Project management: Notion (superior visualization)
>- General tasks (writing notes, thoughts, etc.): Obsidian + Claude Code (direct access to local files)
>- Database: SQLite (for deal tracking)
>- General knowledge queries: GPT-5.2 + Gemini 3 Pro
>- Learning: NotebookLM + Obsidian + Excalidraw
>- Search for nuanced info: Perplexity

### What's the most recent LLM/agent paper or technical resource that changed my thinking, and how?

>- 

