---
name: github-project-handoff
description: Keep a GitHub-backed project synchronized across multiple PCs by checking remote state before work, preserving existing changes, validating deliverables, updating PROJECT_STATUS.md, and committing and pushing completed work when the project has explicitly adopted this workflow. Use for repository work that names multi-PC handoff, GitHub as the shared source of truth, PROJECT_STATUS.md, or a finish-and-push workflow. Stop instead of overwriting when conflicts, divergent history, or unaccounted changes exist.
---

# GitHub Project Handoff

Use GitHub as the shared source of truth for projects worked on from multiple PCs. Preserve local and remote work; never force synchronization by discarding changes.

## Start of work

1. Confirm the repository root, current branch, remote, latest commit, and worktree state.
2. Inspect `README.md`, `AGENTS.md`, and `PROJECT_STATUS.md` when present. Treat repository instructions as authoritative within their scope.
3. Fetch the remote. Compare the checked-out branch with its upstream.
4. Pull only when the worktree is clean and a fast-forward update is safe. Prefer `git pull --ff-only`.
5. Identify uncommitted, untracked, ahead/behind, or divergent work before editing.
6. If local work, remote work, or a conflict could be lost, do not reset, force-push, or overwrite. Explain the exact state and ask for direction if a safe merge is not obvious.

## During work

- Maintain existing code, files, and behavior unless the request requires changing them.
- Keep edits scoped to the requested outcome and inspect overlapping user changes before modifying them.
- Do not commit secrets, API keys, passwords, authentication data, personal information, or machine-specific credentials.
- Keep `.env` and equivalent secret-bearing files out of Git. A sanitized example file may be committed when useful.
- Use recoverable, non-destructive Git operations. Never use `git reset --hard`, destructive checkout, or force-push to resolve uncertainty.

## Finish the work

1. Verify the changed behavior in proportion to risk. Check syntax, errors, and likely regressions.
2. Create or update `PROJECT_STATUS.md` at the repository root with:
   - work completed in this session;
   - current working state;
   - unfinished work;
   - recommended next action;
   - cautions, errors, and known issues;
   - information the next PC or Codex session needs.
3. Review `git status`, the changed-file list, and the diff. Confirm that every change is intentional and no secrets are included.
4. When the user or project has explicitly adopted this finish-and-push workflow, commit the completed work with a descriptive message and push the current branch to its configured remote.
5. If push is rejected, history diverged, tests failed materially, or someone else's changes may be overwritten, stop. Do not force-push. Report the condition and the safest next step.

## Completion report

Report concisely:

- what changed;
- verification performed and its result;
- whether commit and GitHub push succeeded;
- the commit identifier and published URL when available;
- anything the next session must know.

## Authority boundary

This skill defines a workflow, not blanket permission to publish every repository. Commit and push automatically only when the user requested it or the repository instructions explicitly adopt this workflow. Otherwise, complete local verification and ask before publishing.
