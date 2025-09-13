## Setup & Configuration
- `git config --global user.name "[firstname lastname]"` — Set your name for commit history.
- `git config --global user.email "[valid-email]"` — Set your email for commits.
- `git config --global color.ui auto` — Enable colorized Git output.

---

## Repository Initialization
- `git init` — Initialize a new repository in the current directory.
- `git clone [url]` — Clone an existing repository from a remote source.

---

## Staging & Snapshots
- `git status` — Show modified/staged files.
- `git add [file]` — Stage a file for commit.
- `git reset [file]` — Unstage a file (keep changes).
- `git diff` — View unstaged changes.
- `git diff --staged` — View staged changes.
- `git commit -m "[message]"` — Commit staged changes.

---

## Branching & Merging
- `git branch` — List branches.
- `git branch [name]` — Create a new branch.
- `git checkout [name]` — Switch to another branch.
- `git merge [branch]` — Merge a branch into the current one.
- `git log` — Show commit history.

---

## Sharing & Updating
- `git remote add [alias] [url]` — Add a remote alias.
- `git fetch [alias]` — Download remote branches.
- `git merge [alias]/[branch]` — Merge a remote branch.
- `git push [alias] [branch]` — Push commits to remote.
- `git pull` — Fetch and merge from remote.

---

## Tracking File Changes
- `git rm [file]` — Remove a file and stage deletion.
- `git mv [old] [new]` — Rename/move a file.
- `git log --stat -M` — Show commits including file renames.

---

## Temporary Commits (Stash)
- `git stash` — Save uncommitted changes.
- `git stash list` — List stashes.
- `git stash pop` — Restore last stash.
- `git stash drop` — Delete last stash.

---

## Rewriting History
- `git rebase [branch]` — Reapply commits on another base branch.
- `git reset --hard [commit]` — Reset to a specific commit.

---

## Inspect & Compare
- `git log` — Show branch history.
- `git log branchB..branchA` — Show commits in branchA not in branchB.
- `git log --follow [file]` — Show history of a file (across renames).
- `git diff branchB...branchA` — Show diff between branches.
- `git show [SHA]` — Show details of a commit.

---

## Ignoring Files
- `git config --global core.excludesfile [file]` — Global ignore patterns.
- Create `.gitignore` with file/folder patterns to exclude.

---
