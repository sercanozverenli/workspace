# Git Rebase Guide

This documentation explains the `git rebase` mechanism, one of the most powerful and debated commands in the Git version control system. It covers its architecture, best practices, and interactive rebase processes in detail.

---

## 1. Basic Command Structure and Execution

When working on a `feature` branch, to put the latest changes from the `main` branch behind your branch, the basic rebase command sequence is:

```bash
# 1. Pull the latest changes from the main branch to your local computer
git checkout main
git pull origin main

# 2. Switch to your feature branch
git checkout feature-branch

# 3. Start the rebase process
git rebase main
```

**Alternative (Single Line):**
```bash
git rebase main feature-branch
```
*This command tells Git to rebase the `feature-branch` directly based on the `main` branch.*

---

## 2. What is Git Rebase? Architectural Analysis

`git rebase` is the process of **relocating** the starting point (base) of a working branch to the most recent tip of another commit or branch.

### Working Mechanism:
1. Git finds the last common commit (ancestor commit) between the target branch (`main`) and your current branch (`feature`).
2. It saves all the commits you made after that common commit in your current branch to a temporary area (`.git/rebase-merge/`).
3. It resets your current branch to the latest commit of the target branch.
4. It **applies** the saved commits from the temporary area one by one onto the new starting point.

> **Critical Information:** The rebase process does not physically move existing commits. It copies their content and creates **brand new commits with new hash values (SHA-1)**. The old commits stay in the background until Git's Garbage Collection mechanism deletes them.

---

## 3. Git Rebase vs. Git Merge

| Feature | Git Merge | Git Rebase |
| :--- | :--- | :--- |
| **History Structure** | Branching, real-time chronological history. | Linear (a straight line), clean, and ordered history. |
| **Commit Structure** | Creates a new "Merge Commit". | Rewrites existing commits, does not create a new merge commit. |
| **Traceability** | It is clear where the branch separated and merged. | Branches look as if they never separated and were always written on the main line. |
| **Conflict Resolution**| All conflicts are resolved at once. | Conflicts are resolved commit by commit (interactive process). |

---

## 4. Is it Mandatory to Use?

**No, it is not mandatory.** How a project's history is managed depends entirely on the team's or project's architectural standards.

* **Those who choose Rebase flow:** Teams that do not want to see thousands of meaningless *"Merge branch 'main' into..."* commits in the project history and aim for a clean, linearly traceable history.
* **Those who choose Merge flow:** Teams that do not want the project history manipulated and want to keep the exact original hash values and timestamps of when things merged.

---

## 5. Best Use Cases (Do's)

### A. Updating Local Branch
It is the safest approach to use rebase when updating a feature that you have only developed on your own computer and have not yet pushed to the remote server, with the changes in the main project branch.

### B. Cleaning History Before Pull Request (PR)
Used to organize your local commit history before completing a feature and requesting it to be merged into the main project. It allows you to present a perfectly clean commit sequence to the project manager.

---

## 6. Scenarios Where It Should NEVER Be Used (Don'ts)

### 🚨 The Golden Rule of Rebasing
> **"NEVER rebase on a public branch that has been sent to a remote server and is being used by others."**

* **Scenario:** You pushed `main`, `develop`, or a shared `feature-xyz` branch to the remote server. Then, you rebased this branch locally, changed the history, and pushed it to the server using `git push --force`.
* **Result:** When your teammates run `git pull` on their local computers, Git will see that the history on the server and the local history are completely broken. You will cause identical commits to duplicate with different hashes, massive conflicts, and data loss.

---

## 7. History Manipulation with Interactive Rebase (`git rebase -i`)

Interactive rebase is a powerful management tool that allows you to edit your unpublished local commit history from top to bottom with an editor before publishing it.

### Triggering the Command:
To edit the last 3 commits:
```bash
git rebase -i HEAD~3
```

When this command is run, Git opens a file in your default text editor (e.g., Vim, VS Code) listing the relevant commits from oldest to newest:

```text
pick a1b2c3d Initial draft created
pick e5f6g7h Typos fixed
pick j9k0l1m Test scenarios added

# Commands:
# p, pick <commit> = use commit as it is
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# d, drop <commit> = remove commit entirely
```

### Practical Interactive Rebase Scenarios:

#### 1. Fixing a Commit Message (`reword`)
If you made a typo in a commit message or want to write it more clearly:
* Change the word `pick` at the beginning of the relevant commit in the editor to `reword` (or just `r`).
* Save and close the file.
* Git will open a new editor window where you can rewrite only the message of that commit. Fix the message and save.

#### 2. Combining Multiple Commits into a Single Commit (`squash` / `fixup`)
If you made many small and meaningless commits like *"small fix"*, *"test"* during development and want to gather them under one meaningful commit:
```text
pick a1b2c3d Main feature developed
squash e5f6g7h Minor bug fix applied
fixup j9k0l1m Code style formatted
```
* **`squash`:** Combines the changes of the `e5f6g7h` commit with the `a1b2c3d` commit above it and allows you to combine both commit messages to write a new one.
* **`fixup`:** Also combines the changes of the `j9k0l1m` commit but throws away this commit's message, keeping the main title clean.

#### 3. Changing the Commit Order
If you want to change the logical order of the commits:
* You just need to change the order of the lines in the text editor (cut and paste).
* Git will reapply the commits in order from top to bottom according to the new sequence.

#### 4. Completely Deleting a Commit (`drop`)
* Change the `pick` phrase at the beginning of the relevant line to `drop` (or `d`), or completely delete that line from the file. When you save the file, that commit is completely cleared from the history.

---

## 8. Conflict Management During Rebase

Because the rebase process applies commits one by one, conflicts also appear at the commit step. When a conflict occurs, the rebase process pauses.

1. Identify the conflicting files using the `git status` command.
2. Resolve the conflicts manually in your code editor.
3. Add the resolved files to the staging area:
   ```bash
   git add <file-name>
   ```
4. **WARNING:** You never make a new commit (`git commit`) during a rebase. To continue the process:
   ```bash
   git rebase --continue
   ```
5. If things get too complicated and you want to completely cancel the rebase process and return to the previous state as if nothing happened:
   ```bash
   git rebase --abort
   ```
