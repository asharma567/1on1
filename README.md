# 1on1 — end-of-session bookend skill

One repo, two runtimes, two instruction files. **Edit your own file only — never the other runtime's.**

| Runtime | Instruction file in this repo | Live install path |
|---|---|---|
| Claude Code | `SKILL.md` | `~/.claude/skills/1on1/` (this repo, cloned) |
| OpenAI Codex | `CODEX.md` | `~/.codex/skills/1on1/SKILL.md` (plain copy — sync it from `CODEX.md` after edits) |

`agents/openai.yaml` is Codex skill-interface metadata.

## Why the split

2026-07: both runtimes treated `SKILL.md` as theirs and overwrote each other's semantics on push (Codex: ask-gated commits, AGENTS.md memory, no Linear; Claude: commit/pull/push + Linear + memory-files by default). The last writer silently broke the other runtime's bookend. History: Codex variant `f3467f1`, Claude variant `b13dfc4`, split commit thereafter.

## Rules

- Claude sessions: edit `SKILL.md` only.
- Codex sessions: edit `CODEX.md` only, then copy it over `~/.codex/skills/1on1/SKILL.md`.
- Always `git pull --rebase` before editing; this repo is public — pushes need Ajay's explicit go.
