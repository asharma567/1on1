---
name: 1on1
description: "Run an end-of-session bookend for Codex when the user explicitly asks for /1:1, /1on1, a wrap-up, closeout, bookend, commit-and-eval, or durable memory capture. Perform three ordered passes: inspect repositories touched this session and offer commit options for Codex-edited files, give a candid collaboration evaluation, then after at least one user reply propose durable AGENTS.md memory updates. Do not use for mid-task phrases such as closing a file or wrapping a function unless the user clearly intends to end the session."
---

# 1on1 End-of-Session Bookend

Run a deliberate session closeout in three ordered passes. Keep the workflow conservative because the user may have multiple Codex tasks or agents working in the same tree.

## Required order

1. Commit pass
2. Collaboration evaluation
3. Memory pass, after at least one user response to the evaluation

Do not emit the evaluation before checking repository state unless Codex modified no repository or its changes were already committed.

## 1. Commit pass

Run `git status --short` in every repository Codex touched during this conversation. Use the files edited by Codex in this session as the source of truth. Do not claim ownership of pre-existing changes from the user, another Codex task, another agent, or unrelated generated output.

If Codex can separate its changes cleanly, offer:

- **Mine** - stage and commit only files Codex touched this session.
- **Skip** - leave the working tree unchanged and continue to the evaluation.

If clean separation is impossible because the changes are entangled with related dirty files or shared generated output, explain why and offer:

- **Mine** - stage only clearly identifiable Codex-touched files, if possible.
- **Bundle** - include the explicitly named related files needed for a coherent commit.
- **Skip** - leave the working tree unchanged and continue.

Do not suggest **Bundle** when a clean **Mine** commit is possible.

If the user chooses **Mine** or **Bundle**:

- Stage explicitly named files only. Never use `git add -A`, `git add .`, or broad path staging.
- Never override the user's Git author configuration.
- Use a concise multi-line commit message that explains the change.
- Include a co-author footer only when project or global instructions specify the exact footer. Otherwise omit model-specific attribution.
- Report a failed commit and let the user choose whether to retry, adjust scope, or skip.

Skip this pass silently if no repository was modified, Codex touched no files, or Codex's changes were already committed.

## 2. Collaboration evaluation

Give a short, specific, honest evaluation of the user's collaboration during this session from Codex's perspective. Do not flatter or give generic advice.

Use 3-6 bullets and stay under 250 words. Lead directly with the bullets. Cover only categories supported by the conversation:

- **What worked well** - decisions, constraints, examples, approvals, or corrections that improved the result.
- **What tripped us up** - missing context, ambiguity, mid-stream pivots, premature optimization, or unclear ownership.
- **Patterns worth changing** - habits visible across multiple turns rather than isolated mistakes.
- **What I wanted to push back on but didn't** - moments Codex accepted a suboptimal direction because the user sounded certain.

Cite actual turns, decisions, or artifacts. Then stop and wait for at least one user response before starting the memory pass. If the user declines memory capture, do not write memory.

## 3. Memory pass

After at least one user response to the evaluation, scan the full conversation for durable information worth preserving:

- Stable feedback or preferences revealed by corrections, approvals, quiet confirmation of non-obvious choices, or workflow constraints.
- Project facts or decisions that cannot be reconstructed from code, Git history, tickets, or documentation.
- Updates that make existing `AGENTS.md` guidance wrong, incomplete, or stale.

Choose the narrowest appropriate memory home:

- Use the nearest project `AGENTS.md` for project-specific facts, rules, and workflow constraints.
- Use global `~/.codex/AGENTS.md` for cross-repository or cross-project patterns.
- Follow a more specific memory mechanism when the active environment provides one.

Propose 1-3 candidates as a short list. Include a `name` slug and one-line summary. For feedback-style candidates, include `Why:` and `How to apply:` lines. Ask `save these?` and wait for explicit confirmation before writing.

Skip the memory pass silently if nothing durable surfaced. Do not convert evaluation criticism into memory unless the follow-up reveals a stable rule, preference, or project fact.
