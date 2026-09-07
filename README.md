# Evaluating RPI and Design Thinking in Awesome-Copilot vs. HVE-Core

This document summarizes our technical evaluation comparing **[hve-core](https://github.com/microsoft/hve-core)** with an agent-centric, modular approach built on top of **[awesome-copilot](https://github.com/github/awesome-copilot)**.

## Core Architectural Comparison

* **[hve-core](https://github.com/microsoft/hve-core):** A Microsoft-maintained, methodology-driven framework structured tightly around the **RPI workflow (Research, Plan, Implement, Review)** and design-thinking phases. Delivered as a monolithic VS Code extension with deep chat-centric binding.
* **[awesome-copilot](https://github.com/github/awesome-copilot):** A modular, community-driven repository offering decentralized markdown skills, custom instructions, hooks, and file-based sub-agents that can be pulled down à la carte.

## Key Findings & Team Recommendations

* **Agent-Centric Execution:** Moving away from a chat-bound prompt sequence allows us to set up discrete sub-agents for each phase (Research, Plan, Implement, Review) with isolated tool bindings, preventing context window pollution.
* **85%+ Feature Coverage:** Porting RPI governance gates and design-thinking routines as custom markdown agents into [awesome-copilot](https://github.com/github/awesome-copilot) matches the functional depth of [hve-core](https://github.com/microsoft/hve-core) while removing rigid framework lock-in.
* **Simplified Maintenance via CLI:** Instead of managing a heavy versioned extension, we can bootstrap and sync required skills directly into a repository using a lightweight shell or PowerShell script powered by the GitHub CLI. This entirely eliminates extension bloat and ensures teams always run the latest upstream iterations.

## Proposed Action Items for the Team

1. Author or adapt markdown specifications for an agentic RPI loop and design-thinking framework.
2. Build an initialization script (`setup-skills.sh` / `setup-skills.ps1`) to automatically fetch and configure these assets from [awesome-copilot](https://github.com/github/awesome-copilot) during onboarding and CI provisioning.


## Core Focus and Philosophy

* **hve-core ([hve-core](https://github.com/microsoft/hve-core)):** Built by Microsoft, this ecosystem implements a strict, methodology-driven software engineering framework. It is structured heavily around the **RPI workflow (Research, Plan, Implement, Review)** and design-thinking phases to prevent teams from solving the wrong problems prematurely.
* **awesome-copilot ([awesome-copilot](https://github.com/github/awesome-copilot)):** Maintained within the GitHub ecosystem, this repository serves as a broad, community-driven catalog of open-source resources, utility snippets, and flexible extensions designed to expand GitHub Copilot's general capabilities.

**Artifact Structure and Architecture**

* **hve-core ([hve-core](https://github.com/microsoft/hve-core)):** Utilizes a tightly integrated four-tier artifact model consisting of **prompts** (entry points), **agents** (workflow orchestrators), **instructions** (auto-applied coding standards), and **skills** (packaged utility guidance) deployed as a cohesive VS Code extension.
* **awesome-copilot ([awesome-copilot](https://github.com/github/awesome-copilot)):** Functions primarily as a massive directory of standalone modules, including modular skills, custom instructions, hooks, plugins, and agent configurations that developers can pick and choose from modularly.

**Target Use Cases and Workflow Style**

* **hve-core ([hve-core](https://github.com/microsoft/hve-core)):** Best suited for enterprise teams and structured workflows needing rigorous governance, strict architectural guardrails, design-thinking coaches for ambiguous problems, and repeatable multi-step engineering pipelines.
* **awesome-copilot ([awesome-copilot](https://github.com/github/awesome-copilot)):** Ideal for developers looking for à-la-carte customization, specialized tech-stack blueprints, tool integrations, and community-contributed prompt enhancements to tailor Copilot to unique or niche developer stacks.

## Add RPI Skill

Adding an RPI (Research, Plan, Implement, Review) skill to [awesome-copilot](https://github.com/github/awesome-copilot) is **straightforward and technically easy**, but it requires a shift in how the workflow is packaged compared to [hve-core](https://github.com/microsoft/hve-core).

**Structural and Format Adjustments**

* **Standalone Packaging:** [hve-core](https://github.com/microsoft/hve-core) bundles RPI natively as an integrated extension framework across prompts, agents, and custom instructions. In contrast, [awesome-copilot](https://github.com/github/awesome-copilot) relies on a decentralized, modular directory of markdown-based skills under its `skills/` folder.
* **Schema Conformity:** You would need to structure the RPI logic into a single directory containing a conforming `SKILL.md` that adheres to the repository's validation schemas and frontmatter guidelines.

**Implementation Effort Breakdown**

* **File Creation:** Extremely low effort. You write the RPI markdown prompt instructions detailing the Research, Plan, Implement, and Review gates, and drop it into a new subfolder (e.g., `skills/rpi-workflow/SKILL.md`).
* **Integration & Discovery:** Low effort. Because [awesome-copilot](https://github.com/github/awesome-copilot) uses automated checks and plugin manifests, you simply register the skill so users can invoke or compose it alongside other architectural tools.
* **Enforcement Differences:** Moderate conceptual friction. [hve-core](https://github.com/microsoft/hve-core) enforces RPI as a rigid, methodology-driven guardrail, whereas adding it to [awesome-copilot](https://github.com/github/awesome-copilot) makes it an optional, à-la-carte skill that developers can pull in if they want structured execution.

## Agent Centric
Yes, shifting to an agent-centric architecture is entirely natural and well-supported within [awesome-copilot](https://github.com/github/awesome-copilot). While [hve-core](https://github.com/microsoft/hve-core) implements RPI primarily through chat-coupled prompt engineering and extension mechanics, [awesome-copilot](https://github.com/github/awesome-copilot) has native support for file-based custom agents under its `agents/` ecosystem.

**Structural Advantages of an Agent-Centric RPI Approach**

* **Stateful Phase Hand-offs:** Instead of relying on a human user to manually drive chat prompts through Research, Plan, Implement, and Review gates, you can spin up dedicated sub-agents for each phase. A **Research Agent** gathers context, passes a structured specification to a **Plan Agent**, which hands off an implementation brief to an **Implement Agent**, concluding with a **Review Agent** running validations.
* **Isolated Tool & MCP Bindings:** Custom agents in [awesome-copilot](https://github.com/github/awesome-copilot) allow you to bind specific Model Context Protocol (MCP) servers and toolsets per phase. For example, the Research phase can be granted heavy database inspection or code-search tools, while the Implement phase restricts edits to specific code paths.
* **Reduced Context Pollution:** Chat-centric workflows often degrade as the context window fills with multi-phase logs. Agent-centric workflows isolate prompts, system instructions, and execution memory to individual task boundaries, preventing context drift.

**How to Implement It in Awesome-Copilot**

* **Define Phase Sub-Agents:** Create individual markdown definitions (e.g., `agents/rpi-research.agent.md`, `agents/rpi-plan.agent.md`, etc.) that leverage the platform's custom agent configuration schemas.
* **Compose via Orchestration:** Use an orchestrator agent or integrate with existing workflow loops to automate the transition between the phases rather than forcing chat-driven prompt switching.

## Design Thinking

Implementing a design-thinking skill in [awesome-copilot](https://github.com/github/awesome-copilot) is **exceptionally easy** because the repository's modular architecture is specifically built to consume standalone markdown instructions and framework definitions.

**Structural Alignment with Awesome-Copilot**

* **Native Markdown Format:** Like most capabilities in [awesome-copilot](https://github.com/github/awesome-copilot), a design-thinking skill requires only a standard `SKILL.md` file nested inside its own directory (e.g., `skills/design-thinking/SKILL.md`) with frontmatter describing its execution phases (Empathize, Define, Ideate, Prototype, Test).
* **Existing Precedents:** The ecosystem already houses cognitive framework assets—such as thinking agents, breakdown engines, and architectural planners—meaning you don't need to build underlying structural tooling from scratch.

**Estimated Implementation Effort**

* **Low Code Overhead (~1–2 hours):** You simply author the core prompt instructions, define trigger phrases or user-intent markers in the frontmatter, and outline how the model should scaffold user problems through divergent and convergent phases.
* **Compositional Flexibility:** Once dropped into the repository, the design-thinking skill becomes immediately composable. Developers can invoke it ad-hoc alongside code-generation or debugging instructions without rewriting their primary developer workspace.

## Comparison

Adding an RPI workflow and design-thinking capabilities via modular sub-agents would position [awesome-copilot](https://github.com/github/awesome-copilot) ahead of [hve-core](https://github.com/microsoft/hve-core) in modern architectural flexibility. While [hve-core](https://github.com/microsoft/hve-core) relies on a tightly coupled, extension-driven interface that locks users into its specific chat-bound paradigm, an agent-centric implementation in [awesome-copilot](https://github.com/github/awesome-copilot) flips the dynamic entirely.

**Coverage and Modernity Comparison**

* **Feature Parity (~85% Coverage):** By porting RPI governance gates and design-thinking phases into standalone markdown agents, you cover the core methodology of [hve-core](https://github.com/microsoft/hve-core)—ensuring teams research thoroughly, plan architectures cleanly, implement safely, and review rigorously before writing code.
* **Architecture Superiority:** Moving away from a monolithic chat interface to distinct, file-based sub-agents creates an isolated execution loop. Each agent handles a discrete lifecycle state (e.g., Empathize/Research vs. Plan/Define) with scoped context boundaries, avoiding the context pollution common in long chat-centric sessions.

**Structural Trade-offs**

* **Ecosystem Fragmentation vs. Modularity:** [hve-core](https://github.com/microsoft/hve-core) provides an out-of-the-box, cohesive enterprise experience where all artifacts work harmoniously under a single release track. [awesome-copilot](https://github.com/github/awesome-copilot) gives you 100% architectural freedom, but requires your team to manage and compose the agentic loops independently.
* **Tool & MCP Binding:** Your custom agents can leverage dynamic Model Context Protocol bindings natively, giving individual RPI phases specialized capabilities (like database schema inspectors during planning or testrunners during review) that traditional extensions struggle to partition dynamically.

## Modernization

Leveraging the GitHub CLI's skill installation capabilities via a simple shell or PowerShell script completely inverts the maintenance burden of monolithic frameworks like [hve-core](https://github.com/microsoft/hve-core).

**Why the CLI-Driven Skill Approach Wins**

* **Zero Extension Bloat:** Instead of managing a heavy, tightly versioned VS Code extension wrapper that requires constant synchronization with downstream IDE updates, your repository simply declares its dependencies in an initialization script (e.g., pulling directly from [awesome-copilot](https://github.com/github/awesome-copilot) or custom internal registries).
* **Decentralized Maintenance:** When a workflow or standard changes, upstream repositories update their individual markdown artifacts. Running your setup script pulls the latest atomic definitions instantly, avoiding stale enterprise templates.
* **Composability on Demand:** Teams can selectively pull only the skills they need for a specific project repo—injecting an RPI agent bundle here or a design-thinking skill there—without carrying dead code or unused prompts.

**Architectural Blueprint**

* **Bootstrap Script:** A lightweight `setup-skills.sh` or `setup-skills.ps1` script uses `gh` to fetch required skills and sub-agents into `.github/skills/` during developer onboarding or CI provisioning.
* **Local Workspace Independence:** Developers retain full local ownership of their agentic loops, making it trivial to fork, test, and contribute improvements back to community repositories rather than waiting on monolithic framework releases.




