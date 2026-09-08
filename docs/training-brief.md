---
title: Copilot Training Brief
description: Raw stakeholder request for three Copilot training offerings, kept as source input for a business requirements document.
---

Unedited stakeholder request. This is source material, not an agreed plan. It is
the input for a BRD, which is where audiences, objectives, success measures, and
scope get settled. See the `brd` skill.

## I would like you to consider three sets of content / courses

1. Deep dive (3-4 hours recording). Target audience: GSIs. The goal is to teach what you covered the first morning of the HVE Workshop (What is it? Why? Our methodology approach & design thinking, best practices (e.g. shifting security and governance to the left / early stages), how to install it? how to use it?

2. Rapid Prototyping (2-3 hours). Target audience: SI in multi-partner events. I have been told Judson is looking for ways to make our sellers and partners more effective on delivering business value faster to customers. Sales teams are creating Technical Workshop and proposing the Windows Whiteboard app to identify and capture requirements then use screen shots to ask GitHub Copilot to generate a prototype. Here HVE will provide a better way to solve the right problem and capture/communicate/share requirements (e.g. PRD)

3. Full course delivery (8-12 hours). Target audience: GSI requesting private deliveries beyond your scope. We have instructors that can deliver the materias you use for HVE workshops. If needed our suppliers can hire MVPs to ensure the instructor delivering the workshop has real-world experience and they are not theoretical educators.

## Thoughts on delivering this training

In the world of AI SWE, Docker has become a de facto standard for reusing a number of different components. As such, this training should include some Docker familiarity, as many of the devs will be "Windows devs".

Docker only runs on Linux, which means that for Windows and Mac users (95%+ of the audience) you need WSL or Docker Desktop. We have a strong preference for WSL on Windows.

Conducting a class with the requirement to install and configure a Docker VM is a non-starter. You will spend the entire time debugging the environment, particularly when it is locked down by the enterprise.

We therefore recommend the initial classes be held using GitHub Codespaces. Either insure that the audience has access to GitHub Codespaces (and GitHub Copilot with enough tokens) or create (and fund) a GitHub tenant for the class.

## Two versions of the training

It is conceivable, and probably desirable, that there are two versions of this training:

* Business users. The goal is to get to a PRD.
* Software engineers. The goal is to implement a PRD.

This affects prerequisites. Docker and WSL familiarity matters for the engineering track. It is likely out of place for the business track, where the outcome is a PRD rather than a running container.

Software engineers probably want to attend both, getting to a PRD as well as implementing one. One way to schedule that for a mixed audience is to cover PRDs with everyone, then break the group in two: business users create more PRDs, while engineers work on implementing.

## Mixed-audience scheduling

Two options for what the engineers implement after the split:

* Design a PRD together. The whole group works one PRD end to end.
* Implement a known PRD first. Engineers start on a prepared PRD, everyone regroups, and the group then does the session breakdown and implements the new PRD the business group wrote.

The feedback loop in the second option is the valuable part. Authors watch someone build from their document and discover exactly what was ambiguous. That is probably the most memorable moment available in the whole course.

The cost is coupling. The breakouts now depend on each other's pace, and a business group still debating scope leaves the engineers idle. Pre-written PRDs remove that risk and remove the lesson with it.

The hedge: give engineers one known-good PRD to start on, then hand over a fresh one from the business group when it is ready. They implement the prepared PRD first and the live one second, so nobody is blocked and the feedback loop still happens.

The regroup is also the natural place to run joint framing. Pair a business author with an engineer and co-frame the first session against a real PRD. That teaches the co-framing seam by doing it rather than describing it, and it answers the question of who plans the sessions in practice rather than in theory.

## Who plans the sessions

Not sure who plans the sessions. It is likely the PM and the dev team jointly, much like Agile t-shirt sizing, where the value is in the conversation rather than in the number. Both training versions should cover this, since it is the seam where the two audiences meet.

## Course 2 refined

Rapid Prototyping has become: use Design Thinking to get to a PRD. Then use Sessions to break the work into manageable releases, and RPI to implement each one, shipped in 90 to 120 minutes by an SWE or by a pair of SWEs doing paired development.

Note on pairing: the session model is defined around one engineer plus an AI assistant. A pair should be expected to finish faster than a solo engineer, but not twice as fast. For a scope framed at 90 to 120 minutes, expect roughly 60 to 90 minutes. Finishing early is a healthy outcome and not a sign the frame was wrong.

## Teach language-scoped instructions

GitHub Copilot applies instructions by file pattern, such as `*.go`, `*.ts`, or `*.cs`. This is distinctive to Copilot, it is underused, and the engineering track should teach it and use it.

HVE Core has language-specific content, but it reads as dated and verbose for current models. The part worth writing is what a model still gets wrong without being told: house conventions and the traps in a given codebase, rather than a general tutorial for the language.

## Delivery coverage

Course 2 has a delivery design. Courses 1 and 3 have content intent but no delivery design yet.

| Course | Delivery documented | What exists today |
|--------|---------------------|-------------------|
| 1. Deep dive, 3-4 hours, recorded, GSIs | No | Content list only |
| 2. Rapid Prototyping, 2-3 hours, SI events | Yes | Environment, track split, scheduling, hedge, joint framing, pairing, skill flow |
| 3. Full course, 8-12 hours, private GSI | No | Instructor staffing statement only |

### Course 1 open questions

Course 1 is a recording, so most of the delivery thinking above does not apply to it. There are no breakouts, no live environment to debug, and no feedback loop between groups.

* Purely recorded, or a recorded live delivery?
* Do viewers need a working environment, or do they only watch?
* What are the module breakpoints across 3 to 4 hours?
* Who re-records it when the skills change, and how often?
* Content gap: the brief calls for shifting security and governance to the left. Nothing in the current skill set covers that. Either the topic gets built or course 1 promises something we cannot deliver.

### Course 3 open questions

* Is 8 to 12 hours one day, two days, or spread over time?
* Is it courses 1 and 2 expanded, or distinct material?
* Train the trainer. Suppliers may hire MVPs, so people who did not build this will teach it. What ships in the instructor kit: run sheet with timings, lab repo, known-good PRD, worked solutions, and common failure modes?
* Who funds Codespaces for a private client delivery?

### Course 2 timing check

The design is sound but the clock is tight. A PRD block, a session a pair finishes in 60 to 90 minutes, a regroup, and joint framing all have to fit inside 2 to 3 hours. That works only if the PRD block is firmly timeboxed and the implementation scope is deliberately small. There is no slack for a Codespaces problem or a business group that keeps debating scope.

### Missing for all three

* A run sheet with timings.
* The prepared lab repo and known-good PRD as real assets.
* Success measures.
* Who builds the materials, and by when.
* An update cadence as the skills change.

## Recommended next step

Run `design-thinking` with the business owner to agree on which recording and which classes we create and deliver. Most of the input that conversation needs is already captured here.

Once those questions are answered, generate a BRD from this brief and implement the BRD using `sessions`.

Two things that make this work in practice:

* The conversation has to write back into this brief. `brd` builds from notes with cited provenance, so decisions made out loud and never recorded return as open questions rather than as requirements.
* Discovery should decide scope, not just confirm it. Courses 1 and 3 are unbuilt, so cutting or sequencing may be a better outcome than committing to all three at once.

This also makes the training program its own worked example. Discovery to BRD to sessions is the chain the courses teach, so the artifacts produced along the way can double as course material.
