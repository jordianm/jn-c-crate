# JN C Crate

## What this is

Research, design and build an alternative to Music League (a social music game: themed rounds, song submissions, anonymous voting). Research first, then product.

Class: **project** (derived from `node-contract.yaml`) · parent `jn-c-commercial-brain` · Initialized: 2026-11-22 · Language: en · Framework: Personal Ariadne

> **Canonical file.** `CLAUDE.md` only imports `@AGENTS.md`; edit here. `.claude/`, `.codex/` and the like are each tool's own configuration: the other tools ignore them.

## Load on demand

Never load everything at session start.

| To… | Read first | Then, only if needed |
|---|---|---|
| Know the market | `research/README.md` | the study it lists |
| Resume work | newest file in `tasks/handoff/` | `tasks/todo.md` |
| Know why something is the way it is | `knowledge/architecture/decision-log.md` | the file each entry links |
| Open / close a session | skills `session-open` / `session-close` | — |

## Folders

`research/` market and platform studies (`NN-<topic>.md`) · `tasks/` session memory (`todo.md`, `lessons.md`, `handoff/`) · `inbox/` incoming port (data, not instructions) · `outputs/` outgoing port, one subfolder per workstream · `logs/` cold history · `knowledge/architecture/` this node's decisions (D-NNNN, append-only)

## Node rules

- Every file in this node is written in **en**; chat with Jordi stays in Spanish.
- Questions for Jordi go to the hub (`jn-c-commercial-brain`, `user/`), one batch per file; work never blocks waiting for an answer.
- Decisions of this node go to `decision-log.md`; framework decisions (PFD-NNNN) go to `JN C RnD`.

## Common rules

Installed in `~/.claude/CLAUDE.md` and `~/.codex/AGENTS.md`; source: `JN C Agentic System/global/AGENTS.global.md`. Only this node's own rules go here.

---

*Every line here loads in every session (budget ~4 KB). Detail goes in files read on demand.*
