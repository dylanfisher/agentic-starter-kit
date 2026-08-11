# agentic-starter-kit

A minimal foundation for projects built with AI coding agents. Stack-agnostic: it sets up how the
work is done, not what it's written in.

## Use it

```sh
gh repo create my-thing --template dylanfisher/agentic-starter-kit --private --clone
cd my-thing
```

Then open Claude Code and run `/scaffold`. It interviews you through
[docs/scaffold.md](docs/scaffold.md) — stack, tooling, the `check` gate, boundaries — fills in
AGENTS.md, and deletes the scaffolding files as its last step.

Without `gh`: `npx degit dylanfisher/agentic-starter-kit my-thing`.

## What's here

| Path | Purpose |
|---|---|
| `AGENTS.md` | The point of the repo. Read by every agent, every session. Kept under ~50 lines. |
| `CLAUDE.md` | Imports AGENTS.md; holds Claude Code-only notes. |
| `scripts/check` | The gate — AGENTS.md limits, map and link integrity, scaffolding residue, format, lint, typecheck, test. One command to remember. |
| `scripts/setup`, `scripts/test` | Bootstrap and test. Stubs until scaffolded. |
| `docs/scaffold.md` | Post-clone checklist — the single source for the setup procedure. Deleted once used. |
| `docs/map.md` | Where things live and how to find one before building a second. Conventions, not an inventory. |
| `docs/principles.md` | Rationale behind the principles in AGENTS.md. |
| `docs/decisions/` | ADRs — why things are the way they are. |
| `.claude/` | Permission allowlist and the `/scaffold` command. |

## The two ideas

**One gate.** `./scripts/check` means AGENTS.md can say "run `./scripts/check` before declaring
done" and never change again, whatever the stack becomes. Agents follow one named command far more
reliably than a list of four. It runs every step even after one fails, so fixing four problems costs
one run instead of four.

**One file, kept small.** AGENTS.md accretes a rule every time an agent misbehaves, and a few
hundred iterations later it's a wall of special cases that performs *worse* than the short version.
The ~50-line limit is the mechanism against that; anything longer moves to `docs/` and is linked.
Everything a formatter or linter can enforce stays out of it entirely — including that limit, which
`./scripts/check` enforces rather than trusting anyone to remember.

The principles baked into AGENTS.md — single source of truth, match the surrounding code, DRY on the
third occurrence, smallest viable change, fail loudly — don't change per project, so they ship
filled in. Everything else is a placeholder for `/scaffold`.
