# 📚 Git & GitHub — Learning Guide

> Personal documentation for learning Git, GitHub and basic Git Flow.

---

##  1. Initial Configuration

```bash
git config --global user.email "your@email.com"
git config --global user.name "Your Name"
git config --global core.autocrlf true
```

* `user.email` → Email associated with your commits.
* `user.name` → Name associated with your commits.
* `core.autocrlf true` → Helps manage line endings when working across different operating systems.

---

##  2. Create & Clone Repositories

```bash
git init
```

Initializes Git in the current folder and creates the hidden `.git` directory.

```bash
git clone <URL>
```

Clones an existing remote repository to your computer.

```bash
git clone <URL> --depth=1
```

Creates a shallow clone containing only the latest commit history, useful for large repositories when full history is unnecessary.

---

## 3. Check Changes

```bash
git status
git status -s
```

Shows the current state of the working directory.

```bash
git diff
```

Shows changes that have **not** been added to staging.

```bash
git diff --staged
```

Shows changes that are **already in staging**, before creating the commit.

---

## 4. Stage & Commit

```bash
git add <file>
git add .
```

Moves changes to the **Staging Area**, where you select what will be included in the next commit.

```bash
git commit -m "message"
```

Creates a snapshot of the staged changes in the **local repository**.

### Git's basic flow

```text
Working Directory
       │
    git add
       ▼
 Staging Area
       │
  git commit
       ▼
Local Repository
       │
   git push
       ▼
     GitHub
```

>  `commit` saves the version locally. `push` sends it to GitHub.

---

##  5. Branches

Branches allow you to work on features without directly modifying `main`.

```bash
git branch
```

Lists local branches.

```bash
git switch -c feature/login
```

Creates and switches to a new branch.

```bash
git switch main
```

Switches to another branch.

```bash
git merge feature/login
```

Integrates `feature/login` into the branch you are currently on.

```bash
git branch -d feature/login
```

Deletes a merged branch.

### Recommended naming

```text
feature/ → New functionality
fix/     → Bug correction
docs/    → Documentation
refactor/→ Code restructuring
test/    → Tests
```

---

##  6. Remote Repositories

```bash
git remote -v
```

Shows the remote repositories connected to the local project.

```bash
git remote add origin <URL>
```

Connects the local repository to a remote repository.

### `origin` vs `upstream`

When working with your own repository or a fork:

```text
Original Repository
        │
       fork
        ▼
 Your GitHub Repository
        │
      clone
        ▼
 Local Repository
```

Usually:

```text
origin   → Your GitHub repository
upstream → Original repository
```

Configure them with:

```bash
git remote add origin <YOUR_REPOSITORY_URL>
git remote add upstream <ORIGINAL_REPOSITORY_URL>
```

>  `origin` and `upstream` are conventional names, not special Git keywords.

---

##  7. Push, Pull & Fetch

### Push

```bash
git push -u origin main
git push -u origin feature/login
```

Uploads local commits to the remote repository.

The `-u` establishes the branch relationship, allowing future commands to use simply:

```bash
git push
```

### Pull

```bash
git pull origin main
```
Downloads remote changes and integrates them into the current branch.

```bash
git pull origin main --rebase
```
Download the new changes and commits that your colleagues (or you, from another machine) have pushed to the `main` branch on GitHub.


### Fetch

To have branches on your machine without mixing or merging them, you need to synchronize the server data and create a local copy of the other branch.
```bash
git fetch --all
```
Download all branches from the server gitHub 

```bash
git fetch name_rama
```
Downloads the other branch locally to review it.

```bash
git fetch upstream
```

Downloads information about remote changes **without automatically merging them**.

```text
git fetch → Download changes
git pull  → Download + integrate changes
```

---

##  8. Restore, Remove & Rename

```bash
git restore <file>
```

Discards unstaged changes and restores the file to its last committed state.

```bash
git restore --staged <file>
```

Removes a file from staging while keeping its modifications.

```bash
git rm <file>
```

Removes a file and stages the deletion.

```bash
git mv <old> <new>
```

Moves or renames a file while Git tracks the change.

```bash
git reset --hard origin/main
git clean -fd
```
Discard your local changes and overwrite everything with the version from GitHub.

---

##  9. Commit History

```bash
git log
```

Shows the complete commit history.

```bash
git log --oneline
```

Shows a compact version of the history.

Example:

```text
a81f92d Add login functionality
52bd231 Fix navigation bug
1f83a92 Initial commit
```

---

#  10. Basic Git Flow

A simple workflow for developing a feature:

```text
                  ┌───────────┐
                  │   main    │
                  └─────┬─────┘
                        │
                git switch -c
                        │
                        ▼
               ┌────────────────┐
               │ feature/login  │
               └───────┬────────┘
                       │
                Develop / Modify
                       │
                    git add
                       │
                  git commit
                       │
                   git push
                       │
                       ▼
                 ┌───────────┐
                 │  GitHub   │
                 └─────┬─────┘
                       │
                 Pull Request
                       |  
                  Code Review
                       │
                       ▼
                  Merge → main
```

### Typical commands

```bash
# Create feature branch
git switch -c feature/login

# Work on the project
# ...

# Prepare changes
git add .

# Create version
git commit -m "Add login functionality"

# Upload branch
git push -u origin feature/login

# Create Pull Request on GitHub
# Review → Merge → main
```

---

#  Quick Reference

| Command             | Purpose                      |
| ------------------- | ---------------------------- |
| `git init`          | Initialize repository        |
| `git clone`         | Clone repository             |
| `git status`        | Check changes                |
| `git diff`          | View unstaged changes        |
| `git diff --staged` | View staged changes          |
| `git add`           | Stage changes                |
| `git commit`        | Create local version         |
| `git push`          | Send changes to remote       |
| `git pull`          | Download + integrate changes |
| `git fetch`         | Download remote information  |
| `git branch`        | List branches                |
| `git switch`        | Change branch                |
| `git merge`         | Integrate branches           |
| `git restore`       | Restore changes              |
| `git rm`            | Remove files                 |
| `git mv`            | Move / rename files          |
| `git remote -v`     | View remotes                 |
| `git log --oneline` | View commit history          |

---

##  The Core Idea

The basic Git workflow can be remembered as:

        MODIFY
           │
           ▼
    Working Directory
           │
        git add
           │
           ▼
     STAGING AREA
           │
       git commit
           │
           ▼
   LOCAL REPOSITORY
           │
        git push
           │
           ▼
         GITHUB

> **Git manages versions. GitHub hosts and shares repositories.**
>
> **The goal is not to memorize commands, but to understand where your changes are and where they are going.**
