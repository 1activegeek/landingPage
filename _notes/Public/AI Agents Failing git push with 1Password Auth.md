---
date: '2026-02-23'
feed: show
tags:
- ai
- git
- 1password
- cli
title: AI Agents Failing git push with 1Password Auth
---

**Root cause:** Claude Code's bash tool spawns non-interactive subshells. Non-interactive shells don't source `~/.zshrc` or `~/.zprofile` — only `~/.zshenv`. So `SSH_AUTH_SOCK` was staying pointed at the empty macOS launchd agent, which has no keys, causing silent auth failure.

**The fix (three layers):**

1. **`~/.zshenv`** (new file, deployed via chezmoi) — sets `SSH_AUTH_SOCK` to the 1Password socket for _every_process on the machine, interactive or not. This is the root fix.
    
2. **`~/.ssh/config`** — already had `IdentityAgent` on `Host *` as a belt-and-suspenders fallback for processes that don't inherit the env var.
    
3. **`AGENTS.md`** — documented the one-liner fix (`export SSH_AUTH_SOCK=...`) so any future session can recover immediately if the agent socket hasn't propagated yet.
    

The pushes will now work consistently without manual intervention, as long as 1Password is unlocked on your Mac.