---
name: prd
description: 'Turn existing written notes into a structured Product Requirements Document. Use when converting stream-of-consciousness notes, brain dumps, meeting transcripts, design scratch files, an idea doc, or research output into a PRD or spec, and when updating a PRD after new notes are written. Reads the source files and drafts the document with cited provenance and an explicit gap list, rather than interviewing the author question by question.'
---

# PRD

Builds a Product Requirements Document from written source material. The input is one or more stream-of-consciousness markdown files. The output is a completed PRD plus a gap report naming everything the notes did not settle.

## Overview

Most PRD tooling interrogates the author: a question, an answer, another question, repeated until a document exists. That works, but it is slow, it loses fidelity when the author is describing something they already wrote down, and it produces answers shaped by the question order rather than by the thinking.

This skill inverts that. The author writes freely, in whatever structure they think in, across as many files as they like. The skill reads all of it, extracts what is actually there, maps it onto a fixed template, and marks honestly what is missing. Questions still get asked, but in writing, at the end, batched into the document itself.

The loop is: write notes, generate PRD, read the gap list, add to the notes, regenerate. The notes stay the source of truth.

## When to Use

| Situation                                                        | Use this skill        |
|------------------------------------------------------------------|-----------------------|
| Notes, transcripts, or a brain dump exist and need structure       | Yes                   |
| A PRD needs updating after new notes were written                  | Yes, regenerate        |
| Discovery output needs to become buildable requirements            | Yes                   |
| Nothing is written down and the problem is unvalidated             | No, run discovery first |
| Requirements are settled and the next step is building             | No, go to research      |

## Prerequisites

* At least one markdown source file. Anything counts: freeform notes, a meeting transcript, an architecture ramble, a chat export, a bulleted idea list, or prior research output.
* A destination path for the PRD, commonly `docs/prd.md` or `docs/spec.md`.
* The template at [assets/prd-template.md](assets/prd-template.md).

More sources produce a better draft. Fewer sources produce a shorter draft with a longer gap list, which is the correct behavior rather than a failure.

## Quick Start

Point the skill at the notes and the destination.

```text
Draft a PRD from notes/*.md into docs/prd.md
```

The skill reads every source, drafts the PRD against the template, labels anything not directly stated, and finishes with the open questions collected in section 15.

## What Counts as a Source

Sources are not expected to be organized, complete, or consistent. Handle each of these:

| Source type              | Typical contribution                              |
|--------------------------|---------------------------------------------------|
| Stream-of-consciousness  | Intent, constraints, and strong opinions          |
| Meeting notes            | Decisions, disagreements, and owners              |
| Transcripts              | Rationale and rejected alternatives               |
| Architecture scratch     | Components, data shape, and interfaces            |
| Research output          | Evidence, benchmarks, and prior art               |
| Existing PRD or spec     | The baseline being revised                        |

## Required Steps

### Step 1: Inventory the sources

List every input file with its date. Read all of them in full before writing anything. Order matters later for conflicts, so record which notes are most recent.

### Step 2: Extract claims with provenance

Pull every candidate requirement, constraint, decision, exclusion, and open question into a working list. Each entry records the claim and the file and heading it came from. Do not paraphrase away specifics such as numbers, formats, names, and bounds.

### Step 3: Classify every claim

| Label        | Meaning                                                        | Handling in the PRD                       |
|--------------|----------------------------------------------------------------|-------------------------------------------|
| `stated`     | Directly supported by a source note                            | Write it plainly, cite the source         |
| `derived`    | Inferred from the notes but never said outright                | Write it and label it for confirmation    |
| `open`       | No source addresses it                                         | Send it to section 15, do not invent it   |
| `deliberate` | Intentionally left to the implementer                          | Record it in section 1.1 with the reason  |

The distinction between `open` and `deliberate` is the important one. An `open` item is a gap in the thinking. A `deliberate` item is a decision to leave room. Never quietly convert one into the other.

### Step 4: Resolve conflicts

When sources disagree, do not silently pick one. Prefer the most recent note, then record the conflict as an open question naming both positions and both sources. Contradictions that affect the interface contract or acceptance criteria are blocking.

### Step 5: Draft the PRD

Fill the template section by section. Keep every heading. When a section has no material, write "Not applicable" with a reason, or leave it `open`, so the document's shape stays comparable to other PRDs.

Write acceptance criteria in section 14 that are checkable without interpretation. Anything not checkable is not a requirement, so either sharpen it or move it to goals.

### Step 6: Report the gaps

Populate section 15 with every `open` item, marking which are blocking. Populate section 16 with the provenance table. Then stop and report:

* Where the PRD is written.
* Count of items by label.
* The blocking open questions, listed first.
* Any conflicts found across sources.

## The No-Interview Rule

Do not interview the author to fill gaps. Do not ask a question, wait, and ask another.

When information is missing, write it into section 15 as a specific answerable question with an owner, and continue drafting. A written gap list is reviewable, durable, and answerable in the author's own order. An interview is none of those things.

The author closes gaps by adding to the notes and regenerating. If the author explicitly asks to be walked through the gaps conversationally, do that, since the rule protects their attention rather than restricting them.

## Fidelity Rules

* Never invent a requirement. An unsupported statement is `open`, not a guess.
* Preserve specifics exactly. Numbers, formats, identifiers, and bounds carry meaning.
* Preserve rejected alternatives and the reasons, since they prevent the decision being relitigated.
* Keep the author's terminology. Renaming their concepts makes the PRD harder for them to verify.
* Do not smooth over disagreement between sources into agreeable prose.
* Deciding what to leave unspecified is part of the work, not a shortcut. Justify each entry in section 1.1.

## Updating an Existing PRD

Regenerating is the normal path. When a PRD already exists:

1. Treat the current PRD as one more source, and the most authoritative for decisions already made.
2. Apply new notes on top of it.
3. Preserve section 1.1 entries unless a note explicitly closes one.
4. Report what changed: newly closed questions, new opens, and any decision a note reversed.
5. Bump the status and date in the header.

## Handoff

The finished PRD is the input to implementation. Sections 6, 10, and 14 carry the contract, the verification approach, and the definition of done into a research phase. Blocking items in section 15 are research targets, and unresolved conflicts block planning that depends on them.

When the problem itself is unvalidated rather than merely unwritten, the notes will show it: no users, no evidence, and a solution asserted from the start. Say so plainly and recommend discovery before treating this document as requirements.

## Troubleshooting

| Symptom                                     | Response                                                                             |
|---------------------------------------------|--------------------------------------------------------------------------------------|
| Draft is mostly `open`                      | Correct outcome for thin notes. Deliver it, since the gap list shows what to write next |
| Sources contradict each other               | Prefer the most recent, record both positions as a blocking question                   |
| Notes describe a solution with no problem    | Draft what is there and flag that discovery, not a PRD, is the missing step            |
| Section 1.1 is empty                        | Ask what should be left to the implementer, or state plainly that everything is fixed  |
| Acceptance criteria are vague               | Rewrite as checkable statements, or demote them to goals                               |
| The PRD keeps growing on regeneration       | Notes are accumulating rather than deciding. Close open questions in the notes first    |

## Credits

The template structure, and the deliberate underspecification discipline in section 1.1, are derived from the specification in [context-first/movies-template](https://github.com/context-first/movies-template), MIT licensed.

> Brought to you by bartr/skills
