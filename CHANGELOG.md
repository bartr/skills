---
title: Changelog
description: Released versions of the skill set, with the sections of each skill that changed.
---

# Changelog

Versions apply to the skill set as a whole, not to individual skills. Patch is
wording, minor is a new skill or a new optional step, major is a renamed skill,
a moved path, or a changed template structure.

Consumers pin to these tags. Entries name which sections of a skill changed, not
only which files, so a team that edited a skill locally knows what to re-read
before merging an update.

## 0.1.0

First release. Establishes the five skills and the tag consumers pin to.

Skills:

* `brd`. Builds a Business Requirements Document from written notes with cited
  provenance and an explicit gap list.
* `design-thinking`. Six-activity discovery pass ending in an evidence-backed
  PRD handoff.
* `prd`. Builds a Product Requirements Document from stream-of-consciousness
  notes, with deliberate underspecification marked rather than guessed.
* `rpi`. Research, Plan, Implement, Review inner loop, each phase constrained
  against the next and ending in a durable artifact.
* `sessions`. Outer loop of 90 to 120 minute sessions, each closing in green
  tests, a fast-forward merge, a tag, and updated repo memory.

Bundled assets: `brd-template.md`, `prd-template.md`, and
`session-log-template.md`.

Install with `gh skill`, which discovers these by the `skills/*/SKILL.md`
convention with no repackaging:

```bash
gh skill install <owner>/<repo> --all --pin 0.1.0
```

Notes on this release:

* `gh skill` is in public preview and requires GitHub CLI v2.90.0 or later. A
  delivery standing on it carries that risk.
* The tag is signed with the key available to the automation that cut it, which
  is not yet an owner key. Verified-publisher provenance starts when releases
  are cut with a maintainer key.
* No skill content changed between this tag and the branch history preceding it.
  The work leading up to 0.1.0 was documentation.
