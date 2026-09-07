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

