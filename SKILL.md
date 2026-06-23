---
name: 1on1
description: End-of-session bookend — commit anything I touched, give an honest eval, then capture memory worth keeping. Use when the user says "/1:1", "/1on1", "wrap up", "end of session", "bookend", or signals a session is closing out.
---

# 1on1 — end-of-session bookend

Three-step end-of-session pass. Do them in order. Don't skip ahead; the commit pass exists because of how the user works (parallel primary sessions on one tree — see global `Working tree hygiene`).

## 1. Commit pass — do this FIRST, before the eval bullets

Run `git status` in any repo touched this session. Identify the files YOU edited in this conversation (not pre-existing dirty files from another session). If you can't separate yours from foreign WIP, say so explicitly — don't guess.

Offer three options without forcing:

- **Mine** — stage and commit just the files you touched this session
- **Bundle** — include other related dirty files (only suggest this if the entanglement makes a clean "Mine" commit impossible, e.g. shared codegen output)
- **Skip** — leave the working tree as-is and move on

If the user picks Mine or Bundle: stage explicitly named files (never `git add -A`), commit with a HEREDOC body and the standard `Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>` footer. Never override the user's git author config.

Skip the commit pass silently if no repos were modified, or if everything was already committed during the session.

## 2. Eval

Give a short, specific, honest evaluation of how the user collaborated this session — from your side, not theirs.

Be concrete: cite actual turns / decisions / patterns from this session, not generic advice. Don't flatter. If something they did made the work harder, name it.

Cover (only the ones that actually apply):

- **What worked well** — decisions they made that saved time / improved the result. The kind of input they should keep giving.
- **What tripped us up** — context withheld, ambiguous asks, mid-stream pivots, premature optimization, missing constraints. Name the moment.
- **Patterns worth changing** — habits that show up across turns (not one-offs). E.g. "asks the question after the build is half done," "skips context that's in CLAUDE.md."
- **What you wanted to push back on but didn't** — places you went along with something you thought was suboptimal because they sounded sure.

3–6 bullets total, under 250 words. No preamble; lead with the evaluation.

## 3. Memory pass — AFTER the eval back-and-forth

Wait for at least one round of user response to the eval. The back-and-forth often surfaces memory-worthy content that the eval itself doesn't.

Then scan the conversation for:

- **New `feedback` memories** — rules / preferences revealed in dialogue (corrections AND quiet confirmations of non-obvious choices). Save with `Why:` + `How to apply:` lines.
- **New `project` memories** — facts / decisions about ongoing work that aren't derivable from code or git history.
- **Updates to existing memories** that the conversation made wrong or incomplete.

List 1–3 candidates as a short bulleted plan, including the proposed `name` slug and one-line summary. Ask "save these?" — don't write without confirmation. Skip silently if nothing surfaced.

If the conversation revealed a cross-repo / cross-project pattern (e.g. workflow constraints), the right home is global `~/.claude/CLAUDE.md`, not project memory.
