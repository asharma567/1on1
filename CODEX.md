---
name: 1on1
description: "Close a Codex session when Ajay invokes /1:1 or /1on1, requests a wrap-up or closeout, or says he is done for the day. Commit and push identifiable session work by default in private repositories, verify GitHub attribution and branch eligibility, then evaluate collaboration and propose memory after a reply. Do not use for mid-task requests."
---

# 1on1 End-of-Session Bookend

Run a deliberate session closeout in three ordered passes. Keep the workflow conservative because the user may have multiple Codex tasks or agents working in the same tree.

## Required order

1. Commit and push pass
2. Collaboration evaluation
3. Memory pass, after at least one user response to the evaluation

Do not emit the evaluation before checking repository state and push status unless Codex touched no repository.

## 1. Commit and push pass

Run at a requested session closeout, including "done for the day", without waiting for a clock schedule. This skill cannot detect quitting the app or execute while the computer is off. Ordinary task completion does not end the whole session.

Inspect every repository touched in this conversation, even when session changes are already committed: they may still be unpushed. Use the files actually edited this session as the ownership boundary; preserve pre-existing and other sessions' changes.

Before committing, check the effective Git author email. Ajay's GitHub profile is `asharma567`; its GitHub noreply address is `3334296+asharma567@users.noreply.github.com`. Accept another email only if GitHub links it to that account. `ajay@datashop.ai` credited `datashopai` in the October 2026 audit; verify its current association before using it. Do not silently override author configuration or rewrite history; report mismatches for repair.

Ajay authorizes this closeout workflow to commit and push clearly identifiable session work by default in private repositories:

- Stage explicitly named session files only. Never use broad staging, empty commits, fabricated work, or modified dates to fill the graph.
- Use a concise multi-line commit message explaining the change. Include a co-author footer only if applicable instructions specify the exact footer.
- Verify the intended origin, upstream, and remote state. Integrate remote changes only when ownership and working-tree state are safe; abort a conflicting rebase and report it. Never force-push.
- Push the current branch to its existing upstream, or establish the corresponding branch on the verified origin if needed. Respect any instruction to skip commits or pushes.
- For public repositories, make changes concrete and reviewable, then ask for explicit publishing permission unless this session already authorizes the particular push.

If session work is entangled with foreign changes, offer Mine / Bundle / Skip with the files named. If an operation fails, report the specific blocker; do not claim completion.

After pushing, verify the remote tip and the commit's GitHub author login. Check the actual default branch and fork status. Feature-branch pushes alone do not earn commit contribution credit: flag the review/merge needed, but do not merge or change defaults just to increase counts. Private work is publicly counted only when anonymized private contributions are enabled; never make private repositories public for this purpose. Allow up to 24 hours for graph updates.

When available, `/Users/ajay/job_search/tools/github_contribution_check.py --live <repo-path>...` provides a read-only identity, remote-tip, and branch check. Without `--live`, upstream information is cached and does not prove a successful push. Verify GitHub commit author attribution separately.

Finish with a short receipt per repository: commit SHA, push status, attributed GitHub account, and eligible-branch status. Say when nothing changed. Skip committing already-committed work, but still check whether it was pushed. Only claim the graph updated when actually verified.

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
