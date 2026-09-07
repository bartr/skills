---
title: Design and Delivery Plan
description: Distribution decision, target architecture, installer requirements, and delivery status for the context-first skill set.
---

## Decision

We will use [Awesome Copilot](https://github.com/github/awesome-copilot) as
the distribution and runtime surface for our workflow. We will not make
[HVE Core](https://github.com/microsoft/hve-core) a required dependency.

We will contribute or maintain a `context-first` plugin that packages the
session loop, the Research, Plan, Implement, and Review lifecycle, and the
requirements artifacts as reusable skills. The plugin keeps the `context-first`
name as the umbrella for the methodology, while the session loop itself ships as
the `sessions` skill. Discovery and PRD authoring are separate skills so that
ambiguous customer work has an explicit route without imposing that overhead on
bounded engineering work.

The package must preserve the workflow controls that matter: evidence-based
research, explicit acceptance criteria, scoped implementation, independent
review, durable records, and clear follow-up routing. It must not copy HVE Core
verbatim or inherit its extension-specific mechanisms.

> [!IMPORTANT]
> Source artifacts must be owned, reviewed, versioned, and validated by our
> team. HVE Core may be used as a reference for patterns, not as an installation
> dependency or runtime requirement.

## Target Architecture

```mermaid
flowchart LR
    A[Request or idea] --> B{Problem validated?}
    B -- No --> C[design-thinking]
    C --> D[Notes and evidence]
    B -- Yes --> D
    D --> E[prd]
    E --> F[sessions: frame]
    F --> G[rpi: Research]
    G --> H[rpi: Plan]
    H --> I[sessions: fit check]
    I --> J[rpi: Implement]
    J --> K[rpi: Review]
    K --> L[sessions: close]
```

Each skill stands on its own and composes with the others. `rpi` runs standalone
for a single task. `sessions` wraps it with the session frame, the fit
check, and the close ritual. `prd` feeds it scope and acceptance criteria, and
`design-thinking` feeds `prd` when the problem itself is unvalidated. `brd`
sits upstream of `prd` when the business case is what needs settling. No skill
requires the others to be installed.

Discovery stays a separate install from the session loop until evidence shows
every team needs it. That keeps bounded engineering work low-friction while
giving ambiguous customer work an explicit route.

See the [skills catalog](../README.md#skills-in-this-repository) for what exists today.

## Planned Artifacts

| Artifact | Responsibility | Planned form |
|----------|----------------|--------------|
| `context-first` plugin | Groups the maintained skills for installation | `plugins/context-first/plugin.json` |

## Selective Installer

Provide a repository-owned installer at `scripts/install-awesome-copilot-rpi.sh`
and a PowerShell equivalent at `scripts/Install-AwesomeCopilotRpi.ps1`. The
installer uses the GitHub CLI to download only the allowlisted artifacts selected
by a profile, then writes them into the consuming repository's `.github/`
directory.

Supported initial profiles:

| Profile | Installed artifacts | Intended use |
|---------|---------------------|--------------|
| `rpi` | `rpi` alone | A single non-trivial task, without the session loop |
| `session` | `sessions`, `rpi`, and `prd` | Engineering teams with settled requirements |
| `discovery` | `design-thinking`, `brd`, and `prd` | Customer discovery, workshops, and ambiguous requests |
| `full` | All five skills | Discovery that continues into delivery |
| `governed` | `full` plus organization-approved instructions | Teams that require prescribed engineering or security standards |

The installer must:

1. Require `gh` and an authenticated GitHub session.
2. Require `--ref <tag-or-full-sha>` and reject an unpinned branch such as `main`.
3. Download every selected artifact with `gh api repos/<owner>/<repo>/contents/<path>?ref=<ref>`.
4. Enforce a hard-coded allowlist of paths and reject traversal or unrecognized selections.
5. Validate that each downloaded skill has a matching `name` in `SKILL.md` frontmatter.
6. Write an installation manifest containing the source repository, immutable ref,
   selected profile, artifact paths, and file hashes.
7. Support `--dry-run`, `--force`, and `--verify` so teams can review, update, and
   validate installations predictably.
8. Never execute downloaded content during installation and never use `curl | bash`.

Example consumer usage after the package is published and tagged:

```bash
gh repo clone <our-org>/copilot-rpi
cd copilot-rpi
./scripts/install-awesome-copilot-rpi.sh \
  --target ../customer-repository \
  --profile full \
  --ref v1.0.0
```

## Delivery Plan

| Step | Work | Status |
|------|------|--------|
| 1 | Author the `sessions` skill and session log template | Done |
| 2 | Author the `design-thinking` discovery skill | Done |
| 3 | Author the `prd` skill and PRD template | Done |
| 4 | Author the `rpi` skill as a standalone inner loop that other skills leverage | Done |
| 5 | Author the `brd` skill and BRD template | Done |
| 6 | Build the Bash and PowerShell selective installers with the controls above | Next |
| 7 | Test installation from a release tag into an empty fixture repository, and verify each skill is discoverable by GitHub Copilot | Not started |
| 8 | Package the artifacts as a plugin and submit through the Awesome Copilot validation and contribution workflow, or host it as an independently versioned plugin | Not started |
| 9 | Pilot with one delivery team and measure time to a validated plan, implementation rework, review findings, and installer success rate | Not started |
