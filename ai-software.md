---
layout: post
title: AI Software Investing
date: 2025-11-30
---

# Objective of This Question List
- List all the key questions we need to ask to develop a deep understanding of AI investing. What do we know so far, and what gaps remain?
- The list should be updated dynamically—we should update our views after insightful discussions with GPs and founders.
- The list serves as a qualitative measurement of a VC's technical depth (how well they understand the technology) and business capability (how good they are at finding and investing in good deals).

# 1. Technical depth

### 1.1 AI Endgame & Architectural Understanding

1\. In your view, how will a user interact with software in 5–10 years, and what does the underlying stack look like (interface → orchestrator → planning → tools/agents → apps)?
> LL:
>- User interaction
>	- Primary interfaces shift toward multimodal inputs: speech, text, camera/video, and contextual signals from the environment.
>	- Traditional GUI remains, but most workflows begin with natural-language intent (“prepare the board pack”, “analyze this dataset”, “draft a contract consistent with our past versions”).
>	- Many tasks become agent-initiated or agent-augmented (pre-drafting, background monitoring, auto-execution of routine tasks).
>- Orchestrator
>	- A persistent system-level agent sits close to the OS.
>	- It maintains awareness of identity, files, apps, screen context, and preferences.
>	- It interprets user intent, constructs structured tasks, and determines which models, tools, and vertical systems should be involved.
>	- It enforces permissions, privacy boundaries, and cross-application coordination.
>- Planning layer
>	- The orchestrator (or a planning sub-agent) converts intent into a task graph: subtasks, tool calls, dependencies, and checkpoints.
>	- This layer handles error recovery, long-horizon sequencing, and when to involve the user for approval or context clarification.
>- Tools and execution agents
>	- Domain-specific agents handle specialist actions: data analysis, code generation, CRM operations, finance workflows, document drafting, etc.
>	- Many of these agents are embedded inside existing SaaS products rather than standalone apps.
>	- Agents interact through structured APIs and capability endpoints (“create invoice”, “generate SQL”, “prepare shipment label”).
>- App layer and data 
>	- Vertical applications increasingly expose both data and actions programmatically.
>	- The UI becomes thinner; capabilities are invoked by the orchestrator on the user’s behalf.
>	- Compliance, audit trails, and domain-specific correctness remain controlled by the vertical systems.
>- State and memory
>	- The system maintains short-term and long-term memory: ongoing tasks, drafts, preferences, prior interactions, and cross-app context.
>	- This memory is shared across orchestrator and key vertical systems, with strict privacy and enterprise permissioning.
>- Overall user experience
>	- Users continue to open individual apps for certain workflows, but a growing portion of work is delegated: declare intent → agent plans → agents execute → user reviews → agent refines.
>	- The cognitive load shifts from “how to do the task” to “what outcome is desired”.

2\. What are the strongest reasons your endgame might not happen? Separate technical, economic, regulatory, and user-behavior constraints.
> LL: 
>- Technical constraints
>	- Planning, long-horizon reliability, and error recovery may plateau. LLMs may excel at short tasks but remain brittle on complex workflows.
>	- Safe continuous learning and long-term personalization remain unsolved; without them, agents stay stateless or require heavy human configuration.
>	- Tool-use and schema-adaptation may not reach enterprise-grade robustness. 
>- Economic constraints
>	- Multi-agent workflows are compute-intensive. If inference costs or latency do not fall as fast as expected, many end-to-end automated workflows may be uneconomical.
>	- Enterprises may cap automation levels to reduce infra complexity, debugging cost, and risk exposure, limiting “fully autonomous” scenarios.
>- Regulatory and privacy constraints
>	- Cross-app visibility and central orchestration may be restricted by privacy rules, data-localization requirements, and enterprise governance.
>	- OS vendors may deliberately limit screen access, keyboard events, permission scope, and automation APIs for safety/compliance.
>- User-behavior and organizational constraints
>	- In high-stakes domains (legal, medical, finance), organizations may enforce “human-in-the-loop” as mandatory.
>	- Users may prefer predictable workflows over opaque agents, slowing adoption of end-to-end automation.
>- If these constraints persist, the ecosystem skews toward powerful embedded copilots inside existing SaaS/OS platforms rather than fully autonomous cross-app agents.

3\. What capabilities do frontier models still need to reach for that endgame to work (e.g., reliability, planning, long-term memory, tool use, continuous learning)? Which of these do you think are solvable vs. structural bottlenecks?
> LL: 
>- Reliability on known tasks: Solvable. Improvements in model architecture, distillation, structured guardrails, and filtered training data should reduce variance and increase predictability.
>- Planning and long-horizon reasoning: Partially solvable. Pure LLM planning is unlikely to achieve high reliability; real progress depends on hybrid systems combining LLMs with structured planners, code execution, and explicit task graphs.
>- Tool-use robustness: Solvable with better schemas, validation layers, and more consistent API abstractions. This is primarily an engineering problem rather than a fundamental research barrier.
>- Long-term memory and personalization: Hard. Current approaches (RAG, external stores) provide retrieval, not actual stateful learning. Safe online adaptation without catastrophic forgetting is an open research challenge.
>- Continuous or “nested” learning: Uncertain. Conceptually powerful but challenging due to safety, drift, and eval overhead. Production systems will likely rely on periodic controlled fine-tuning rather than unrestricted online learning.
>- Interpretability and safety: Structural bottleneck. Incremental improvements are expected, but full transparency into model behavior is unlikely. This limits adoption in high-stakes environments and slows autonomy.
>- Overall, reliability and tool use trend toward solvability; long-term memory, continuous learning, and interpretability remain structural bottlenecks shaping the ceiling of agent autonomy.

4\. Who owns the "state" of the user? Is it the Model Provider (OpenAI knows my chat history), the OS (Apple knows my screen), or the Vertical App (Trip knows my hotels)? Who wins the right to context and routing?
> LL: 
>- OS and productivity suites (Microsoft 365, Google Workspace, Apple ecosystem)
>  Own global state: identity, device context, files, email, search, calendar, and what is on screen. This gives them a structural advantage in routing and context assembly. 
>- Vertical applications (CRM, ERP, developer tools, design systems, healthcare systems)
>  Own deep domain state: customer data, ledgers, codebases, medical records, operational workflows. They will expose both data and domain-specific actions but retain control of business logic and compliance.
>- Model providers (OpenAI, Anthropic, Google models)
>  Own state only inside their hosted workspaces and agent environments (e.g., ChatGPT Teams). When serving as backend models inside other apps, they have far weaker visibility and limited identity/context access.
>- Enterprise-controlled data stores
>  In corporate settings, much of the durable state resides in IT-owned data lakes, vector stores, and permissions-managed knowledge bases.
>- Routing outcome
>	- OS/prod-suite dominates default routing for cross-application tasks due to visibility and control.
>	- Vertical systems dominate routing inside their own domains.
>	- Model providers win routing only where they control the full user experience.

5\. In that endgame, which layers do you think _become commoditized_ vs. _remain defensible_? 
> LL: 
>- Commoditizing layers
>	- Mid-tier models and generic inference APIs, driven by open source competition and scale economics.
>	- Thin “wrapper” applications that simply provide UI over a frontier model without workflow integration, proprietary data, or domain logic.
>- Defensible layers
>	- Vertical applications where correctness, integration, compliance, and workflow depth matter. Defensibility comes from proprietary data, domain knowledge, and operational embedding, not the model itself.
>	- Systems that accumulate proprietary structured data and user feedback loops, enabling continuous improvement in specific high-value domains.
>	- Potentially, orchestration/planning platforms that become embedded in enterprise workflows. This layer has high upside but is strategically contested by OS vendors, SaaS ecosystems, and cloud providers.

6\. How fast do you expect inference costs to drop? 
>- 2×–5× reductions are likely in the near term through hardware efficiency, quantization, and batching.
>- 10×+ reductions are possible but dependent on breakthroughs in model architecture, compilation, and edge acceleration.
>- Agentic workflows consume significantly more compute than single-model inference; cost declines do not translate linearly to cheaper workflows.
>- If inference costs fall rapidly, more autonomous multi-agent workflows become economical; if costs stall, autonomy remains limited and SaaS-embedded copilots dominate.

---

### 1.2 Fundamental Understanding
7\. What is the fundamental difference between internet apps, SaaS, and AI apps? What are the differences in evaluating deals in these different sectors?
> LL:
>- Internet apps
>	- Primarily engagement-driven systems with zero marginal cost of replication.
>	- Value comes from network effects, distribution, user acquisition funnels, and content/interaction loops.
>	- Key evaluation metrics: retention cohorts, virality, LTV/CAC, user-generated content.
>- SaaS products
>	- Tools purchased to achieve predictable, repeatable outcomes.
>	- Value comes from workflow embedding, data schema control, integrations, and switching costs.
>	- Evaluation metrics: net retention, depth of workflow integration, administrative control, unit economics, modular expansion potential.
>- AI-native apps
>	- Users pay for a result, not a tool: accuracy, speed, reduction in manual labor, and correctness.
>	- Core differentiator is not UI but:
>		- correctness and robustness
>		- data advantage
>		- quality of planning and tool use
>		- depth of workflow integration
>	- They behave more like “managed services delivered by software” than classical SaaS.
>- Implication for evaluating deals
>	- Must evaluate real-world accuracy, reliability, and iteration speed, not UI polish.
>	- Must assess whether the team can keep pace with frontier model change.
>	- Defensibility depends on:
>		- proprietary data
>		- workflow lock-in
>		- integration depth
>		- domain-specific correctness loops

8\. Decompose a modern agentic system into major steps (intent, context, planning, tool selection, execution, evaluation, memory). Where are the biggest technical gaps today?
>- Intent understanding: What the user actually wants.
>  Gaps: long instructions still needed; models struggle with ambiguous intents; weak adaptation to individual preferences.
>- Context assembly: Gather data across documents, files, apps, screens, APIs, and prior interactions.
>  Gaps: incomplete context, permission constraints, brittle schema assumptions, inaccurate retrieval.
>- Planning and task decomposition: Transform intent into a structured workflow or task graph.
>  Gaps: inconsistent decomposition, hallucinated steps, poor error handling, weak long-horizon coordination.
>- Tool selection and execution: Choosing appropriate tools (SQL, Python, API calls) and executing them reliably.
>  Gaps: fragile schema handling, inconsistent tool-use protocols, high sensitivity to minor tool changes.
>- Iterative execution loop: Run → observe → adjust → retry.
>  Gaps: runaway loops, incomplete monitoring, failures not escalated to user, lack of robust fallback logic.
>- Evaluation and correction: Grade output, detect errors, enforce quality thresholds.
>  Gaps: limited self-evaluation, poor rubric enforcement, subjective output hard to verify.
>- Memory (short-term and long-term): Remember previous tasks, drafts, user preferences, and recurring workflows.
>  Gaps: no true long-term memory; RAG is retrieval, not learning; personalization is still superficial.
>- Summary of biggest gaps:
>	- Reliable planning and long-horizon reasoning
>	- True long-term memory and personalization
>	- Robust, schema-stable tool use
>	- Evaluation frameworks and quality control
>	- Context assembly across varied enterprise data sources 

|                                           | Description                                                                                                                                                                                                                           | How to achieve / what's missing                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Ingest goals and interpret user intent | Agents understand user intent more efficiently without the user providing a detailed plan. This includes agents understanding the user (what they do, what their preferences are) and the workflow (what the intended task could be). | Agents learn and store user preferences, frequent workflows, and commands over interactions. This could perhaps be solved by (1) LLMs having progressive learning capability, (2) agents autonomously maintaining very efficient documentation systems.                                                                                                                                                                                           |
| 2. Gather and store context/state         | Get context efficiently for what's needed to complete the task. This could include context from the environment the agent is operating in and expand beyond that.                                                                     | Good system prompts that include progressive disclosure settings (e.g., Claude skills) of how to do things.                                                                                                                                                                                                                                                                                                                                       |
| 3. Decompose tasks and generate a plan    | Agents efficiently break the task down into smaller parts and come up with a plan to complete it.                                                                                                                                     | 1. Currently this still require humans to handle, but various frontier models are already doing well (e.g. Claude Code's planning mode). We should have agents break down tasks into smaller parts in an agent-friendly manner to allow agents to handle them efficiently.<br>2. The master plan should be stored properly and shared with all agents in the loop.                                                                                |
| 4. Execute plan in an iterative loop      | Agent executes according to plan. Decides what tools to use or even creates new tools on the fly, observes results, and updates plan iteratively.                                                                                     | 1. Should measure results by tasks per intervention—human intervention should be minimal.<br>2. Each agent (if not one master agent) should properly share context among themselves.<br>3. Should efficiently route requests to different models to ensure best quality output at lowest cost.<br>4. Should efficiently decide which tool to use and switch tools after observation.<br>5. Independent sub-tasks should be processed in parallel. |
| 5. Self-evaluate and re-plan when needed  | After near-final result, agent should self-reflect on its work and update plan where needed.                                                                                                                                          | Reviewing agent should know what the ideal result for the task is, perhaps trained with benchmarks. Review the work and help modify the source prompt or give specific instructions on how to improve.                                                                                                                                                                                                                                            |

>- Interesting paths:
>	- Orchestrator: Dynamically designs workflows for various tasks, decides routing and tool use.
>	- Workflow manager: Has good context management to manage multiple agents.
>	- Review agent: How to grade output efficiently and provide feedback to planner on how to adjust the plan or tell orchestrator how to do it better.
>- I think the next billion-dollar idea is in the planning layer, which is the 'platform business' for AI. The orchestration agent has the power to decide which apps and tools to use, essentially the traffic gateway. 

9\. How do you think about planning in agentic systems (e.g., CoT/ToT, ReAct, code-based planning, multi-agent setups), and what failure modes have you actually seen or worry most about?

10\. What are the most important missing infrastructure pieces for agents (e.g., memory, eval, guardrails, orchestration, trust/safety, simulation), and which of these do you think are attractive for venture investment?
> LL: 
>- Model performance is good enough today. Generally, if users know the right prompts and the most robust best practices, model performance is quite good. 
>
>What's missing:
>- Easier implementation of best practices: Every model/system has different best practices, and it's hard to keep track of everything.
>- Context engineering: Current context engineering is very inefficient. Users have to manually configure many things for agents to generate expected results. It is not good enough for general users.
>- Efficient user intent understanding: Users still need to write long plans to get good outcomes. Models also don't progressively learn what the user wants.
>- Autonomy decisions: Users need to find a sweet spot in the low-to-high autonomy spectrum and determine how much human intervention should be in the loop.
>- Evaluation: Lack of systematic evaluation methods—how do we quantify agent performance so we know which agent to call for a specific task?
> - Memory: LLMs are very poor at long-term memory. Context windows are very limited. The current best solution is to pair LLMs with RAG, but RAG is just like a database where the LLM tries to find relevant information that's not loaded in its current context window. How do we allow LLMs to synthesize new information and make decisions/suggestions based on continued learning? This is important.
> - Agentic context sharing and communication: How LLMs communicate with each other and with apps is very important. Anthropic has done a great job defining some industry standards, e.g., MCP—very clever ways of telling agents what to do, when to do it, and how to do it. But it's still not at a level where apps and agents can speak with each other and collaborate on tasks efficiently. Dominant app players are definitely reluctant to embrace this infrastructure, as their platform dominance will be diluted by LLMs, since orchestration agents will decide which app gets called to execute tasks going forward. But whoever is reluctant to evolve will be replaced by agent-native products.
> - Modality: Text-based interaction is highly inefficient. Going forward, we should be able to prompt with speech (already many breakthroughs) and camera.
> - Agentic coding: Although agentic coding tools (like Cursor, Claude Code) are already very good at generating code, there are still significant pain points in how to manage the codebase to keep it clean and scalable, as well as deployment.

11\. Will agentic systems start with niche applications, or will development happen directly on general use cases? What trends have you observed?

### 1.3 Evaluation and Hands-On Depth
12\. How do you evaluate an AI product's performance in practice
	- objective vs. subjective evals
	- temporal consistency, robustness
	- “real” data advantage vs. storytelling)
> LL: There are objective vs. subjective evals.
>- Objective means code-checkable, right vs. wrong (correct answer, correct SQL, etc.). Objective eval is easier because we just need a sample and correct-answer checking.
>- Subjective means something that can be graded (e.g., a deal memo). Subjective eval is harder because it's difficult to score accurately.

13\. What models, tools, or agents do you personally use day-to-day, and what recent experiment has materially changed how you work?
> LL:
> - Project management: Notion (superior visualization)
> - General tasks (writing notes, thoughts, etc.): Obsidian + Claude Code (direct access to local files)
> - Database: SQLite (for personal usage of deal tracking)
> - General knowledge queries: GPT-5.1 + Gemini 3 Pro
> - Learning: NotebookLM + Obsidian + Excalidraw
> - Search for nuanced info: Perplexity

14\. What's the most recent LLM/agent paper or technical resource you read that changed your thinking, and how did it change your view?

---

# 2. Business capability

### 2.1 Segment Focus
15\. Given your endgame view and what’s technically hard vs. easy for LLMs, which categories of software are you most focused on investing in, and which “hot” areas are you intentionally avoiding? Why?
> LL:
>- Should focus:
>	- The durable opportunity lies in applications with these characteristics:
>		(1) correctness matters, requires low hallucination
>		(2) multi-system integration
>		(3) data is private or domain-specific
>		(4) workflows demand long-horizon coordination
>	- As well as the agentic workflow infrastructure that is still missing as 
>- Should avoid:
>	- General agents: Model providers will push hard to become general agents themselves. The problem with general agents is that they're good at delivering say 80%, but that's not good enough. They will be disrupted by (1) vertical/niche agents that can complete tasks efficiently most of the time, (2) orchestrating agents (e.g., embedded in OS).
>	- LLM-easy tasks: Image/photo/content generation are examples. These high-TAM, LLM-easy tasks are going to be captured by model providers. Google's NotebookLM and Nano Banana recent updates are crushing Gamma for slide generation and other image-generating apps.

### 2.2 Ideal Team Profile
16\. What are the non-negotiable characteristics of an AI founding team, and how do you practically test for them?
> LL: The team should have both strong technical capability (so they can adapt to model changes and iterate very quickly) and product management experience (so they can build apps that actually solve problems with good user experience).

17\. How do you assess whether a founder and team can survive rapid changes in the model/provider landscape over the next 5–10 years?
> LL: The founder doesn't necessarily need ML experience, but must have a strong fundamental understanding of how LLMs work and scientific research capability so they know how to build products on top of them.

18\. Would you prefer AI-native startups or incumbent fast-learners adding AI?

19\. What are the biggest red flags in AI founders or "AI products" that non-technical or generalist VCs often miss?

### 2.3 Economics in AI Era
20\. How will open source model providers monetize?

21\. SaaS pricing (per seat) is dying for AI. Do you believe in 'consumption-based' (tokens) or 'outcome-based' (dollars per task)? How do we underwrite the quality and durability of that 'outcome-based' revenue?

22\. What is the current gross margin level of applications? What do you expect the future trend to be?

23\. In a world where core model intelligence becomes cheaper and more available, what do you believe becomes the most important driver of long-term value (distribution, proprietary data, workflow lock-in, something else)?

### 2.4 Investment Strategy
24\. At which stage (seed, A, growth) do you think the risk/reward is best for AI software, and how does that shape your fund's strategy?

25\. How do you underwrite a company at early stage / growth stage?
> LL: Need deep understanding to (1) evaluate how quickly the startup can adapt and iterate, (2) what is defensible vs. not, and (3) what larger TAM use cases exist.

26\. What's your exit strategy? Have there been any examples of M&A or secondary transactions of AI startups?
> LL: No one knows how to exit AI apps (yet), and it's very hard to gauge the upside. Better to take money off the table aggressively.

27\. Walk me through your process for evaluating an AI deal from first meeting to conviction: what do you do differently from a generalist VC, especially around technical diligence and "fast no's"?

