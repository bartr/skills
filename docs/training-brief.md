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

We therefore recommend the initial classes be held using GitHub Codespaces.

## Two versions of the training

It is conceivable, and probably desirable, that there are two versions of this training:

* Business users. The goal is to get to a PRD.
* Software engineers. The goal is to implement a PRD.

This affects prerequisites. Docker and WSL familiarity matters for the engineering track. It is likely out of place for the business track, where the outcome is a PRD rather than a running container.

Software engineers probably want to attend both, getting to a PRD as well as implementing one. One way to schedule that for a mixed audience is to cover PRDs with everyone, then break the group in two: business users create more PRDs, while engineers work on implementing.

Open question: do the engineers implement the PRDs the business group just wrote, or pre-written ones? Using the fresh PRDs closes a real feedback loop, since authors see what was ambiguous once someone builds from it. It also couples the two breakouts, so a slow morning for one group stalls the other.

## Who plans the sessions

Not sure who plans the sessions. It is likely the PM and the dev team jointly, much like Agile t-shirt sizing, where the value is in the conversation rather than in the number. Both training versions should cover this, since it is the seam where the two audiences meet.
