---
title: Repository Memory
description: Durable facts and conventions for AI assistants working in this repository.
---

# Repository Memory

Read this before changing anything here. It records decisions that are already
settled, so they do not get relitigated or silently reversed.

## What This Repository Is

Five reusable agent skills for AI-native engineering, covering business case
through discovery, requirements, and delivery. It is documentation, not code.
There is no build, no test suite, and no runtime. The markdown is the product.

`new-method` is a placeholder name, not the agreed one. Treat every occurrence
as pending a rename. See [docs/design.md](docs/design.md#naming).

## Always Use gh skill

`gh skill` is the only supported way to install and update these skills. Do not
write, propose, or resurrect a bespoke installer, and do not document raw
`gh api` calls as the install path.

```bash
gh skill install <owner>/<repo> rpi --pin 0.2.0     # always pin
gh skill preview <owner>/<repo> rpi                 # read before installing
gh skill list                                       # what is installed here
```

An earlier plan specified repository-owned Bash and PowerShell installers with
their own allowlist, manifest, and verification flags. That plan is withdrawn.
`gh skill` covers the same surface, and a first-party command a customer's
security team already trusts beats a script of ours doing the same job.

### It Is Not GA

`gh skill` is in public preview and requires GitHub CLI v2.90.0 or later.

Two consequences that matter when writing about it:

* The command surface can change before it stabilizes. Anything this repository
  documents about flags or behavior is accurate as of preview and needs
  rechecking at GA. Verify against `gh skill <command> --help` or the CLI source
  rather than from memory.
* Say so where it is relevant. A customer or course audience deciding to depend
  on this is entitled to know it is preview software, and that a delivery
  standing on it carries that risk.

Preview status is a caveat, not a reason to route around the command.

## Layout Is the Public API

```text
skills/<name>/SKILL.md          # discovered by the skills/*/SKILL.md convention
skills/<name>/assets/           # bundled templates, copied on install
```

`gh skill` discovers skills by this convention, and `gh skill install <repo>
<name>` resolves against the directory name. Renaming or moving a skill
directory breaks every pinned install command in circulation, so treat it as a
breaking change requiring a major version.

## Skills Must Not Reference the Install Mechanism

No `SKILL.md` may mention `gh skill`, install profiles, pinning, or any other
distribution detail. [docs/design.md](docs/design.md) claims content and
distribution are separable and states that the claim is checkable. Keep it true:

```bash
grep -rniE "gh skill|--pin|profile|install" skills/    # must return nothing
```

A skill describes a way of working. How it arrived on disk is not its concern.

## Writing Conventions

The documentation has a deliberate voice. Match it rather than defaulting to
generic technical writing.

| Convention | Rule |
|------------|------|
| Emphasis | No bold. Lead a bullet with a short phrase and a period instead |
| Bullets | `*`, never `-` |
| Line width | Wrap prose at roughly 80 characters |
| Tables | Preferred over long lists for anything comparative |
| Frontmatter | Docs and `README.md` use `title` and `description`; each `SKILL.md` uses `name` and `description` as the Agent Skills specification requires; asset templates carry none |
| Tone | State the position and the reason. No hedging, no marketing register |

Claims should be checkable. When the documentation asserts something about the
repository, prefer an assertion a reader can verify with a command.

## Never Commit to main

Every change lands on a branch first, including documentation-only changes,
which is nearly all of them here. A docs repository invites the "it is just a
wording fix" exception. There is no such exception.

The branch name carries no meaning. Name it for the work and delete it on merge.

Close as the `sessions` skill prescribes: fast-forward merge, then tag the
dot-release. See [The Close Ritual](skills/sessions/SKILL.md).

```bash
git switch -c <name-for-the-work>
# commit
git push -u origin <name-for-the-work>
```

## Releases

Consumers pin, so tags are the contract.

* Signed `0.x.y` tags, immutable once pushed. A wrong tag is fixed by the next
  patch, never by moving it.
* Version the set, not each skill.
* Every release needs a changelog entry naming which sections of a skill
  changed, not only which files.

The full update policy is in
[docs/design.md](docs/design.md#updating-installed-skills).
