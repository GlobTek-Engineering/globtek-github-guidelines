<div align="center">

# GlobTek Engineering
## GitHub & Git — Team Guide

*Everything you need to go from zero to version control in one page.*

---

**[① What is Git & GitHub?](#1--what-is-git--github) · [② Why are we using it?](#2--why-are-we-using-it) · [③ Getting Set Up](#3--getting-set-up) · [④ Core Concepts](#4--core-concepts) · [⑤ Daily Workflow](#5--daily-workflow) · [⑥ Quick Reference](#6--quick-reference)**

</div>

---

<br>

## 1 · What is Git & GitHub?

> Think of **Git** as a time machine for your files, and **GitHub** as the shared drive everyone on the team connects to.

| | Git | GitHub |
|---|---|---|
| **Lives** | On your computer | In the cloud |
| **Does** | Tracks every change you make | Hosts the shared repo for the whole team |
| **Think of it as** | Your local save history | The team's shared project folder |

<br>

---

## 2 · Why Are We Using It?

To replace confusing email chains with real version control.

### The old way

* Long email chains where information is almost impossible to recover and often forgotten
* FINAL FINAL FINAL engineering documents
* Lost test documents for reviewing old data

### The new way
```
main ──●──────────────────────────────────────────────●──────────────► 🏷️ EVT2 Release
            └─● ECR-evt1-to-evt2        Tim's change, tracked  ─────────┘
```
**With GitHub we get:**
- ✅ One place for all engineering files — no more hunting through inboxes
- ✅ Full history of every change, who made it, and why
- ✅ The ability to go back to any version at any time
- ✅ Project tracking built right into the repo

<br>

---

## 3 · Getting Set Up

### Step 1 — Create a GitHub Account & Join the Org

1. Sign up at **[github.com](https://github.com)**
2. Ask your team lead to add you to **[GlobTek-Engineering](https://github.com/GlobTek-Engineering)**

<br>

### Step 2 — Install Git + posh-git on Your Machine

> **posh-git** makes your PowerShell terminal show your current branch and status automatically — it makes Git much easier to use day-to-day.

**Open PowerShell and run these one at a time:**

```powershell
# 1. Install posh-git
Install-Module posh-git -Scope CurrentUser

# 2. Open your PowerShell profile in Notepad
notepad $PROFILE

# 3. Add this line to the file that opens, then save & close it
Import-Module posh-git
```

✅ **Done!** Restart PowerShell and your terminal will now show your branch name automatically.

<br>

### Step 3 — Clone a Repo to Your Machine

Cloning downloads a full copy of a repository so you can work on it locally.

```bash
git clone https://github.com/GlobTek-Engineering/<repo-name>
```

**What you'll see:**

```
Cloning into 'GTM965500P'...
remote: Enumerating objects: 84, done.
remote: Counting objects: 100% (84/84), done.
remote: Compressing objects: 100% (52/52), done.
Receiving objects: 100% (84/84), 2.34 MiB | 3.1 MiB/s, done.
```

| Line | What it means |
|---|---|
| `Cloning into 'GTM965500P'...` | Git is creating a new folder with that name on your machine |
| `Enumerating objects: 84` | There are 84 files/commits it needs to download |
| `2.34 MiB \| 3.1 MiB/s` | Total size downloaded and your download speed |

✅ When it finishes with no errors, you're good. A new folder will appear in your current directory.

<br>

---

## 4 · Core Concepts

### What is a Repository?

A **repository (repo)** is a project folder tracked by Git. It contains:

| What's inside | What it is |
|---|---|
| Files | Your actual engineering files |
| Branches | Parallel versions for different changes |
| History | Every commit ever made |
| Releases | Stable, tagged versions |
| Projects | Task boards for tracking work |

<br>

### What is a Branch?

> A branch lets you make changes **without touching the main files** until you're ready.

```
main ──────────────────────────────────►  always stable
         │
         └──► your-branch ──────────►  your sandbox
```

**Name your branch after what you're doing:**

```
✅  tims-branch
✅  ECR-evt1-to-evt2
✅  pcb-changes
✅  updating-transformer-footprint
```

**Create and switch to your branch:**
```bash
git checkout -b ECR-evt1-to-evt2
```

**What you'll see:**

```
Switched to a new branch 'ECR-evt1-to-evt2'
```

✅ That's it. You're now on your own branch and safe to make changes.

<br>

### This is a Shared Repo — Be Aware

> You are **no longer working alone.** Every push affects the team.

- ✅ Always create your own branch before making changes
- ✅ Commit often with clear messages
- ❌ Never work directly on `main` unless you are doing it intentionally

<br>

---

## 5 · Daily Workflow

### Starting Work

```bash
git checkout -b ECR-evt1-to-evt2    # create your branch and switch to it
```

```
Switched to a new branch 'ECR-evt1-to-evt2'
```

<br>

### Making & Saving Changes

Make your edits to the files, then tell Git to save them.

---

#### `git add .`
Stages everything you changed — tells Git "I want to include these in my next save."

```bash
git add .
```

`git add` is silent — if it works, nothing prints. That's normal. ✅

---

#### `git status`
Shows you exactly what Git is tracking before you commit. Run this often — it's your safety check.

```bash
git status
```

**What you'll see:**

```
On branch ECR-evt1-to-evt2
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   schematics/GTM965500P_main.sch
        new file:   test-data/evt1_results.csv

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   docs/BOM_rev3.xlsx
```

| Section | What it means |
|---|---|
| `On branch ECR-evt1-to-evt2` | Confirms which branch you're on |
| `Changes to be committed` | These files have been staged with `git add` and will be included in your next commit |
| `modified: schematics/...` | A file that already existed and has been changed |
| `new file: test-data/...` | A brand new file Git hasn't seen before |
| `Changes not staged for commit` | You changed this file but haven't run `git add` yet — it will **not** be included in your commit |

> If you see a file under "not staged" that you meant to include, run `git add .` again before committing.

---

#### `git commit -m "..."`
Saves a labeled snapshot of everything you staged.

```bash
git commit -m "updated schematic for ECR evt1 to evt2"
```

**What you'll see:**

```
[ECR-evt1-to-evt2 3a9f2c1] updated schematic for ECR evt1 to evt2
 2 files changed, 47 insertions(+), 12 deletions(-)
 create mode 100644 test-data/evt1_results.csv
```

| Line | What it means |
|---|---|
| `[ECR-evt1-to-evt2 3a9f2c1]` | The branch name and the short ID of this commit — every commit gets a unique ID |
| `2 files changed` | How many files were included in this save |
| `47 insertions(+), 12 deletions(-)` | Lines added and removed across all files |
| `create mode 100644 test-data/...` | A new file was added to the repo for the first time |

> **Commit messages matter.** Write what you actually changed — not just "update" or "fix".

---

#### `git push origin <branch>`
Uploads your branch and commits to GitHub so the team can see your work.

```bash
git push origin ECR-evt1-to-evt2
```

**What you'll see:**

```
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.23 KiB | 1.23 MiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/GlobTek-Engineering/GTM965500P.git
 * [new branch]      ECR-evt1-to-evt2 -> ECR-evt1-to-evt2
```

| Line | What it means |
|---|---|
| `Enumerating / Counting / Compressing` | Git is packaging your changes to send |
| `Writing objects` | Uploading to GitHub |
| `To https://github.com/...` | Confirms which repo it was pushed to |
| `* [new branch] ECR-evt1-to-evt2` | This branch didn't exist on GitHub yet — Git created it remotely |

✅ After this, your branch will be visible on GitHub and your team can review it.

<br>

### Need to See the Original Files?

You can jump back to `main` at any time — your branch is untouched:

```bash
git checkout main
```

**What you'll see:**

```
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

| Line | What it means |
|---|---|
| `Switched to branch 'main'` | You're now looking at the main branch files |
| `Your branch is up to date with 'origin/main'` | Your local main matches what's on GitHub — nothing has changed |

Then when you're ready to go back:

```bash
git checkout ECR-evt1-to-evt2
```

```
Switched to branch 'ECR-evt1-to-evt2'
```

<br>

### What If Main Changed While You Were Working?

This happens often on a shared repo. Here's how to sync up:

```
someone pushed to main  ──►  main is now ahead of you
                                        │
bring those changes down  ◄─────────────┘
```

---

#### `git fetch`
Downloads the latest information from GitHub — but doesn't change any of your files yet. Safe to run any time.

```bash
git fetch
```

**What you'll see:**

```
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
From https://github.com/GlobTek-Engineering/GTM965500P
   3a9f2c1..7bd4e10  main -> origin/main
```

| Line | What it means |
|---|---|
| `remote: Enumerating objects` | GitHub is telling you what changed |
| `3a9f2c1..7bd4e10  main -> origin/main` | Main on GitHub has new commits since you last synced — your local copy is behind |

If `git fetch` prints nothing, your local copy is already up to date. ✅

---

#### `git status` (after a fetch)

```bash
git status
```

```
On branch main
Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
```

| Line | What it means |
|---|---|
| `behind 'origin/main' by 2 commits` | Two new saves were made on GitHub that you don't have yet |
| `can be fast-forwarded` | There are no conflicts — Git can apply the changes cleanly |

---

#### `git pull --rebase`
Pulls the latest from GitHub and applies it to your local machine.

```bash
git pull --rebase
```

**What you'll see:**

```
Successfully rebased and updated refs/heads/main.
```

Or if there were several commits to apply:

```
First, rewinding head to replay your work on top of it...
Applying: updated BOM for rev3
Applying: added EVT1 test results
Successfully rebased and updated refs/heads/main.
```

| Line | What it means |
|---|---|
| `rewinding head to replay your work on top of it` | Git is temporarily setting aside your commits, applying the new ones from GitHub, then putting yours back on top — keeping history clean |
| `Applying: updated BOM for rev3` | Each of your commits being re-applied one by one |
| `Successfully rebased` | All done, no conflicts ✅ |

<br>

---

## 6 · Quick Reference

| Command | What it does |
|---|---|
| `git checkout -b <name>` | Create a new branch and switch to it |
| `git checkout main` | Switch back to main |
| `git add .` | Stage all changed files |
| `git status` | See what's changed and what's staged |
| `git commit -m "message"` | Save a labeled snapshot |
| `git push origin <branch>` | Upload your branch to GitHub |
| `git fetch` | Check for remote updates (nothing changes yet) |
| `git pull --rebase` | Pull latest from GitHub and sync your machine |

<br>

---

<div align="center">

**Questions?** Open an issue in this repo or ask your team lead.

*GlobTek Engineering · [globtek.com](https://www.globtek.com)*

</div>
