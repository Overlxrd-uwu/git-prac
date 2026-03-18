# Git Learning Notes

## 1. What Git is
Git is a version control system. It helps you track file changes, save checkpoints, go back to older versions, and collaborate more safely.

A simple way to think about Git:
- **Working directory** = your current files
- **Staging area** = changes you want included in the next save
- **Commit** = a saved snapshot of staged changes
- **Remote repository** = an online copy, such as GitHub

---

## 2. Git Setup and Init
Before making commits, set your identity. This name and email are written into your commits.

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

To start Git in a project folder:

```bash
git init
```

This creates a hidden `.git` folder, which stores the repository history and settings.

### Notes
- `--global` means the setting applies to all repositories on your computer.
- `git init` does not upload anything to GitHub.
- After `git init`, the folder becomes a Git repository.

---

## 3. Track and Save Changes
Use `git status` often. It shows what is changed, what is staged, and what is still untracked.

```bash
git status
```

To stage changes:

```bash
git add .
```

Then save them with a commit:

```bash
git commit -m "Describe what you changed"
```

### What each command does
- `git status` checks the current repository state.
- `git add .` stages changes from the current folder downward.
- `git commit -m "..."` creates a snapshot of the staged changes.

### Good beginner reminder
- `git add .` = prepare changes
- `git commit` = save locally
- `git push` = upload to GitHub later

---

## 4. About `git add .`, `git add -A`, and `git add --all`
These are similar, but not exactly the same in intent.

```bash
git add .
git add -A
git add --all
```

### Quick explanation
- `git add .` stages changes from the current directory downward.
- `git add -A` stages all changes in the whole repository.
- `git add --all` is effectively the same as `git add -A`.

### Easy memory rule
- `.` means **from here**
- `-A` means **everything in the repo**

For beginners, `git add .` and `git add -A` are the most useful to remember.

---

## 5. Branching Made Easy
A branch is another line of development. It lets you work on something without affecting the main branch right away.

Create a new branch:

```bash
git branch feature-x
```

Switch to that branch:

```bash
git checkout feature-x
```

Merge the branch into your current branch:

```bash
git merge feature-x
```

### Better modern form
Today, many people use `git switch` instead of `git checkout` for changing branches:

```bash
git switch feature-x
```

Create and switch in one step:

```bash
git switch -c feature-x
```

### Notes
- `git branch feature-x` only creates the branch.
- `git checkout feature-x` or `git switch feature-x` moves you onto it.
- `git merge feature-x` brings that branch’s changes into the current branch.

### Simple workflow
```bash
git switch -c feature-x
# make changes
git add .
git commit -m "work on feature x"
git switch main
git merge feature-x
```

---

## 6. Revert or Reset Changes
These commands are for undoing different kinds of changes.

### Revert a file to the last commit
```bash
git restore <file>
```
This discards local unstaged changes in that file.

### Unstage a file
Older form:
```bash
git reset HEAD <file>
```

Modern form:
```bash
git restore --staged <file>
```

This removes the file from the staging area but keeps your work in the folder.

### Revert a commit with a new commit
```bash
git revert <commit-id>
```
This does **not** erase history. Instead, it creates a new commit that reverses an earlier one.

### Important difference
- `restore` = undo local file changes
- `restore --staged` = unstage changes
- `revert` = undo a past commit safely with a new commit
- `reset` can rewrite history, so use it carefully

---

## 7. Connect to a Remote Repository
A remote repository is an online copy of your repo, usually on GitHub.

Link your local repo to GitHub:

```bash
git remote add origin <repo-url>
```

Push your branch to GitHub:

```bash
git push -u origin main
```

Get the latest changes from GitHub:

```bash
git pull origin main
```

### Notes
- `origin` is the usual default name for the remote.
- `main` is the usual default branch name now.
- `git push` uploads local commits.
- `git pull` downloads and merges remote changes.

### Very important reminder
```bash
git commit
```
does **not** upload to GitHub.

You must still run:

```bash
git push
```

---

## 8. Local vs Remote
This is one of the most important beginner ideas.

### Local actions
```bash
git init
git add .
git commit -m "message"
```
These only affect your computer.

### Remote actions
```bash
git push
git pull
```
These interact with GitHub or another remote server.

---

## 9. Beginner Command Summary

### Setup
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init
```

### Daily work
```bash
git status
git add .
git commit -m "message"
```

### Branches
```bash
git branch feature-x
git checkout feature-x
git switch -c feature-x
git merge feature-x
```

### Undo
```bash
git restore <file>
git restore --staged <file>
git reset HEAD <file>
git revert <commit-id>
```

### Remote
```bash
git remote add origin <repo-url>
git push -u origin main
git pull origin main
```

---

## 10. Best Practices for Beginners
- Run `git status` often.
- Write clear commit messages.
- Use branches for new features or experiments.
- Be careful with undo commands.
- Remember that `commit` is local and `push` is remote.
- Prefer `git restore --staged <file>` over the older `git reset HEAD <file>` when learning.

---

## 11. Simple Real Workflow Example
```bash
# first time setup
git init
git status

# after creating or editing files
git add .
git commit -m "first commit"

# connect to GitHub
git remote add origin <repo-url>
git push -u origin main
```

---

## 12. Final Memory Trick
Think of Git in this order:

**change files -> check status -> add -> commit -> push**

or even shorter:

**edit -> stage -> save -> upload**
