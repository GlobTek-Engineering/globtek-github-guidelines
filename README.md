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

### The old way

```
RE: RE: RE: RE: FWD: GTM965500P_schematic_FINAL_v3_TIM_EDITED_USE_THIS_ONE.pdf
```

### The new way

```
main ──●──────────────────────────────► latest, always clean
            └─● ECR-evt1-to-evt2        Tim's change, tracked
                   └─● pcb-changes      Sarah's change, tracked
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
git checkout -b <your-branch-name>
```

<br>

### This is a Shared Repo — Be Aware

> You are **no longer working alone.** Every push affects the team.

- ✅ Always create your own branch before making changes
- ✅ Commit often with clear messages
- ❌ Never work directly on `main`

<br>

---

## 5 · Daily Workflow

### Starting Work

```bash
git checkout -b ECR-evt1-to-evt2    # create your branch and switch to it
```

<br>

### Making & Saving Changes

Make your edits to the files, then tell Git to save them:

```bash
git add .                                                # stage everything you changed
git commit -m "updated schematic for ECR evt1 to evt2"  # save a snapshot
git push origin ECR-evt1-to-evt2                        # send it up to GitHub
```

> **Commit messages matter.** Write what you actually changed — not just "update" or "fix".

<br>

### Need to See the Original Files?

You can jump back to `main` at any time — your branch is untouched:

```bash
git checkout main                  # switch back to main
# look at whatever you need...
git checkout ECR-evt1-to-evt2     # jump back to your branch
```

<br>

### What If Main Changed While You Were Working?

This happens often on a shared repo. Here's how to sync up:

```
someone pushed to main  ──►  main is now ahead of you
                                        │
bring those changes down  ◄─────────────┘
```

```bash
git checkout main      # switch to main
git fetch              # check what changed remotely (safe — doesn't touch your files yet)
git status             # see exactly what's different
git pull --rebase      # bring your machine up to date
```

> `--rebase` keeps the history clean by replaying your changes on top of the latest `main`.

<br>

---

## 6 · Quick Reference

| Command | What it does |
|---|---|
| `git checkout -b <name>` | Create a new branch and switch to it |
| `git checkout main` | Switch back to main |
| `git add .` | Stage all changed files |
| `git commit -m "message"` | Save a labeled snapshot |
| `git push origin <branch>` | Upload your branch to GitHub |
| `git fetch` | Check for remote updates (nothing changes yet) |
| `git status` | See what's changed locally |
| `git pull --rebase` | Pull latest from GitHub and sync your machine |

<br>

---

<div align="center">

**Questions?** Open an issue in this repo or ask your team lead.

*GlobTek Engineering · [globtek.com](https://www.globtek.com)*

</div>
