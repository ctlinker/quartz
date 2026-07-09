---
publish: true
title: Git Cheatsheet
tags:
  - cheatsheet
  - git
  - tooling
---
# Git Cheat Sheet

> **Git** is a distributed version control system that tracks changes to files, allowing multiple people to collaborate on a project safely.

---

# Configuration

Set your identity.

```bash
git config --global user.name "John Doe"
git config --global user.email "john@example.com"
```

View your configuration.

```bash
git config --list
```

Edit the configuration manually.

```bash
git config --global --edit
```

---

# Create a Repository

Initialize a new repository.

```bash
git init
```

Clone an existing repository.

```bash
git clone <repository-url>
```

Clone into a specific directory.

```bash
git clone <repository-url> my-project
```

---

# Repository Status

See modified, staged, and untracked files.

```bash
git status
```

Short version.

```bash
git status -s
```

---

# Staging Files

Stage one file.

```bash
git add file.txt
```

Stage multiple files.

```bash
git add file1 file2
```

Stage everything.

```bash
git add .
```

Stage modified and deleted files.

```bash
git add -u
```

Interactively choose changes.

```bash
git add -p
```

---

# Committing

Create a commit.

```bash
git commit -m "Add login page"
```

Commit staged changes using your editor.

```bash
git commit
```

Stage and commit tracked files.

```bash
git commit -am "Fix bug"
```

Amend the last commit.

```bash
git commit --amend
```

---

# Viewing History

Compact history.

```bash
git log --oneline
```

Graph view.

```bash
git log --graph --oneline --all
```

Show commit details.

```bash
git show <commit>
```

See who modified each line.

```bash
git blame file.txt
```

---

# Branches

List branches.

```bash
git branch
```

Create a branch.

```bash
git branch feature
```

Switch branches.

```bash
git switch feature
```

Create and switch.

```bash
git switch -c feature
```

Old equivalent.

```bash
git checkout feature
```

Delete a merged branch.

```bash
git branch -d feature
```

Force delete.

```bash
git branch -D feature
```

Rename current branch.

```bash
git branch -m new-name
```

---

# Merging

Merge another branch.

```bash
git merge feature
```

Abort a conflicted merge.

```bash
git merge --abort
```

---

# Rebasing

Rebase onto another branch.

```bash
git rebase main
```

Interactive rebase.

```bash
git rebase -i HEAD~5
```

Abort.

```bash
git rebase --abort
```

Continue after conflicts.

```bash
git rebase --continue
```

---

# Remote Repositories

List remotes.

```bash
git remote -v
```

Add a remote.

```bash
git remote add origin <url>
```

Change remote URL.

```bash
git remote set-url origin <url>
```

Remove a remote.

```bash
git remote remove origin
```

---

# Fetch & Pull

Download remote changes.

```bash
git fetch
```

Download and merge.

```bash
git pull
```

Rebase instead of merge.

```bash
git pull --rebase
```

---

# Push

Push current branch.

```bash
git push
```

Push and set upstream.

```bash
git push -u origin main
```

Force push (use carefully).

```bash
git push --force-with-lease
```

---

# Undo Changes

Discard unstaged changes.

```bash
git restore file.txt
```

Unstage a file.

```bash
git restore --staged file.txt
```

Restore both.

```bash
git restore --source=HEAD --staged --worktree file.txt
```

Reset last commit (keep files).

```bash
git reset --soft HEAD~1
```

Reset and unstage.

```bash
git reset HEAD~1
```

Delete last commit completely.

```bash
git reset --hard HEAD~1
```

---

# Stashing

Save work temporarily.

```bash
git stash
```

List stashes.

```bash
git stash list
```

Restore latest stash.

```bash
git stash pop
```

Restore without deleting.

```bash
git stash apply
```

Delete stash.

```bash
git stash drop
```

---

# Tags

Create a lightweight tag.

```bash
git tag v1.0
```

Annotated tag.

```bash
git tag -a v1.0 -m "Version 1.0"
```

List tags.

```bash
git tag
```

Push tags.

```bash
git push --tags
```

---

# Comparing Changes

Working tree vs staged.

```bash
git diff
```

Staged vs last commit.

```bash
git diff --cached
```

Compare two commits.

```bash
git diff commit1 commit2
```

---

# Cleaning

Remove untracked files.

```bash
git clean -f
```

Remove directories too.

```bash
git clean -fd
```

Preview before deleting.

```bash
git clean -n
```

---

# Ignore Files

Create a `.gitignore`.

Example:

```gitignore
node_modules/
dist/
.env
*.log
*.tmp
```

---

# Useful Inspection Commands

Current branch.

```bash
git branch --show-current
```

Repository root.

```bash
git rev-parse --show-toplevel
```

Tracked files.

```bash
git ls-files
```

Recent commits.

```bash
git reflog
```

---

# Common Workflows

## Create a New Feature

```bash
git switch -c feature/navbar

git add .

git commit -m "Implement navigation bar"

git push -u origin feature/navbar
```

---

## Update From Main

```bash
git switch main

git pull

git switch feature/navbar

git rebase main
```

---

## Resolve a Conflict

```bash
git status

# Edit conflicting files

git add .

git rebase --continue
```

or

```bash
git merge --continue
```

---

# Git Areas

```text
Working Directory
       │
       │ git add
       ▼
Staging Area (Index)
       │
       │ git commit
       ▼
Local Repository
       │
       │ git push
       ▼
Remote Repository
```

---

# Most Useful Commands

```text
git init

git clone

git status

git add

git commit

git log

git diff

git switch

git branch

git merge

git rebase

git fetch

git pull

git push

git stash

git restore

git reset

git tag

git remote

git clean
```

---

# Git Lifecycle

```text
Create file
     │
     ▼
Modified
     │
git add
     ▼
Staged
     │
git commit
     ▼
Committed
     │
git push
     ▼
Remote Repository
```

---

# Golden Rule

Before making major changes, remember this sequence:

```bash
git status

git pull --rebase

# Work on your code

git add .

git commit -m "Describe your changes"

git push
```

Checking `git status` frequently is one of the best habits you can develop—it tells you exactly where your files are in Git's workflow.