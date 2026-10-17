---
description: Interview the user and scaffold this freshly-cloned starter into a real project
---

This repo was cloned from the agentic starter template and is not yet set up.

**The procedure is [docs/scaffold.md](../../docs/scaffold.md).** Read it, then run it in two
phases: an interview that settles every decision the checklist needs, then a build that works its
sections in order and ticks each box as you complete it so the state survives an interrupted
session. Do not restate its steps here — this file holds only how to conduct the interview.

## The interview

Settle every decision before writing to any file. The interview ends at a confirmed playback
(the last item below), and the build starts only after it.

- **Open with one broad question: what are we building?** Ask it alone, before anything in the
  checklist. Invite the user to describe it in their own words: what it does, who uses it, where
  it runs (web app, CLI, library, service, mobile…), and any constraints they already know about,
  such as an existing team language, hosting target, or integrations. Play back a two-line summary
  and confirm it before moving on.
- **Let that answer shape every later question.** Draft the name and one-sentence description
  for section 1 from it. Tailor each recommendation to it: the stack, the tiers in `docs/map.md`,
  the boundaries, and whether secrets or CI are needed at all. Skip questions it already answered
  (confirm them in one line instead), and leave out options that don't fit. Say *why* each
  recommendation fits what they described.
- **Ask in rounds.** The checklist's decisions depend on each other: the language comes before the
  package manager, the tiers before commit scopes, "does it need secrets" before the vault. Each
  round asks every question whose prerequisites are settled, and none whose answer depends on
  another question still open. After each round, work out the next one from the answers. A typical
  run:
  1. What are we building (alone)
  2. Name and description, language and version, framework, license, remote and host, whether it
     needs secrets
  3. Package manager, test framework, formatter and linter, tier names, the 1Password vault (only
     if it needs secrets)
  4. Boundaries, naming conventions, the dependency-direction tool, the permission allowlist
  5. Voice and commits — kept to their own round because each question needs examples shown
- **Format every round the same way,** so the user can answer it by number
  ("1 yes, 2 pnpm, 3 no — private"):

  ```
  ❓ **Q1 - <title>**: <question, with the options that fit>

  ➡️ <recommended answer, and why it fits what they described>
  ```

  Word each question so "yes" accepts the recommendation.
- **Decisions are asked; facts are looked up.** Don't scan an empty repo to guess the stack — that
  is a decision, and the repo has no signal for it. Do check what the machine can tell you, and
  never ask the user for it: `git remote -v`, whether `op` and `gh` are installed and signed in,
  which toolchain versions are installed, the current stable release of the chosen language.
  Only the questions that depend on a lookup wait for it; ask the rest of the round now.
- **Voice and commit style are taste, not facts about the project.** Show short examples for
  them rather than describing options in the abstract. People can pick a tone when they see it
  far more easily than they can name one.
- If the user says something that contradicts an earlier answer, follow the new answer and reopen
  the questions that depended on the old one in the next round.
- **End with a playback.** When no question is left open, list every decision in one block. Below
  it, list each default you would apply that the user hasn't seen — a `.gitignore` section you'd
  delete, a deny rule you'd leave alone. Wait for an explicit confirmation before building.

## The build

- Work the checklist in order with the confirmed decisions. If a step raises a decision the
  interview missed, ask it in the same format. Don't decide it yourself.
- **Stop at the gate.** Do not proceed past the "The gate" section until `./scripts/check` actually
  exits 0 on the empty project. Everything after it depends on that being real.
- Prefer editing the files that exist over adding new ones. This starter is deliberately small; a
  scaffolded project should gain a lockfile, tool configs, and a source tree — not a docs sprawl.
