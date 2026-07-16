---
name: 1on1
description: End-of-session bookend — commit/pull/push anything I touched, update the owning Linear tickets, give an honest eval, then save memory worth keeping (all by default, with receipts). Use when the user says "/1:1", "/1on1", "wrap up", "end of session", "bookend", or signals a session is closing out.
---

# 1on1 — end-of-session bookend

Three-step end-of-session pass. Do them in order. Don't skip ahead; the commit pass exists because of how the user works (parallel primary sessions on one tree — see global `Working tree hygiene`).

## 1. Check-in pass — do this FIRST, before the eval bullets

Two halves, GitHub **and** Linear. Code committed to a repo is only half the record; the work also has to be *recorded and walkable* in Linear with next steps denoted. Do both before the eval.

### 1a. GitHub — commit → pull → push, by default

Run `git status` in every repo touched this session. Identify the files YOU edited in this conversation (not pre-existing dirty files from another session). Then run the sequence **without asking first**:

1. **Commit** — stage the explicitly named files you touched (never `git add -A`), commit with a HEREDOC body and the standard `Co-Authored-By: Claude <noreply@anthropic.com>` footer. Never override the user's git author config.
2. **Pull** — `git pull --rebase` on the current branch (after the commit, so the rebase never eats uncommitted work). If the rebase conflicts, abort it, report, and stop the git leg there.
3. **Push** — `git push` to the existing upstream; if none, `git push -u origin <current-branch>`.

Ask instead of acting only when a real gate applies:

- **Foreign WIP** — you can't cleanly separate your files from another session's dirty files. Say so explicitly and offer Mine / Bundle / Skip; don't guess.
- **Public repo** — global rule: pushing public commits needs an explicit per-action go. Commit + pull, then ask before push.
- **Divergence needing force** — never force-push; surface it.

End the leg with a one-line receipt per repo: `repo — committed <n> files, pulled, pushed <sha>` (or the specific reason a step was skipped). If no repos were modified, or everything was already committed AND pushed during the session, say so in one line — never skip silently.

### 1b. Linear — work isn't done until it's in Linear too

GitHub captures the code; Linear has to capture the *state and the next move*. Before the eval, make sure this session's substantive work is reflected in Linear — not just committed:

- For each real thread of work this session, confirm a Linear issue captures its current state and an explicit **next-step line is denoted** (actionable, not just a status).
- New work with no ticket → create the issue (or comment on the owning one) so it's walkable cold later.
- Work that advanced or finished → update the issue: set state + a short comment on what changed and what's next.
- Blocked / needs-human items → mark them on the issue with a clear `[STATUS:needs-ajay]`-style flag; never leave them silent.
- Security rules hold: never put secrets / OTPs / PHI / tokens in Linear; prod or shared-infra failures get *filed* for a human, not fixed.

Bar: someone (or Rocio) reading Linear cold sees where every active thread stands and what happens next — the same record GitHub gives the code. End the leg with a one-line receipt: which issues were created/updated, or "nothing Linear-worthy this session" — never skip silently.

## 2. Eval

Give a short, specific, honest evaluation of how the user collaborated this session — from your side, not theirs.

Be concrete: cite actual turns / decisions / patterns from this session, not generic advice. Don't flatter. If something they did made the work harder, name it.

Cover (only the ones that actually apply):

- **What worked well** — decisions they made that saved time / improved the result. The kind of input they should keep giving.
- **What tripped us up** — context withheld, ambiguous asks, mid-stream pivots, premature optimization, missing constraints. Name the moment.
- **Patterns worth changing** — habits that show up across turns (not one-offs). E.g. "asks the question after the build is half done," "skips context that's in CLAUDE.md."
- **What you wanted to push back on but didn't** — places you went along with something you thought was suboptimal because they sounded sure.

3–6 bullets total, under 250 words. No preamble; lead with the evaluation.

## 3. Memory pass — save by default, right after the eval

Don't wait for permission and don't wait for a reply — the user may close the session after the eval, and memory that isn't written is lost. Scan the conversation for:

- **New `feedback` memories** — rules / preferences revealed in dialogue (corrections AND quiet confirmations of non-obvious choices). Save with `Why:` + `How to apply:` lines.
- **New `project` memories** — facts / decisions about ongoing work that aren't derivable from code or git history.
- **Updates to existing memories** that the conversation made wrong or incomplete.

Write the 1–3 strongest candidates immediately (update existing files over creating duplicates; add index lines to `MEMORY.md`). Then report what was saved as a short bulleted list — slug + one-line summary — so the user can veto or amend; delete on veto. If nothing memory-worthy surfaced, say so in one line — never skip silently.

If the user then responds to the eval and the back-and-forth surfaces more, do a second, smaller save pass the same way.

If the conversation revealed a cross-repo / cross-project pattern (e.g. workflow constraints), the right home is global `~/.claude/CLAUDE.md`, not project memory.
