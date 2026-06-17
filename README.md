# GlobTek Engineering — GitHub Guidelines

This guide covers everything you need to know to use Git and GitHub as part of the GlobTek EE team.

---

## 1. What is Git and GitHub?

- **Git** is a version control system that tracks changes to files over time on your local machine.
- **GitHub** is a cloud platform that hosts Git repositories so teams can collaborate, review, and share work.

---

## 2. Why Are We Using It?

We are replacing email chains with real version control. GitHub gives us:

- A single source of truth for engineering files
- A full history of every change and who made it
- Structured collaboration without the confusion of emailed attachments

---

## 3. How Do I Use It?

### a) Make a GitHub Account and Join the Org

1. Create a free account at [github.com](https://github.com)
2. Ask your team lead to add you to the [GlobTek-Engineering](https://github.com/GlobTek-Engineering) organization

### b) Set Up Git on Your Local Machine

#### Install Git for Windows (with posh-git for a better terminal experience)

1. Download and install [Git for Windows](https://git-scm.com/download/win)
2. Open **PowerShell** and install the `posh-git` module:
   ```powershell
   Install-Module posh-git -Scope CurrentUser
   ```
3. Sign into your GitHub account when prompted
4. Add `posh-git` to your PowerShell profile so it loads automatically:
   ```powershell
   notepad $PROFILE
   ```
   Add this line to the file that opens, then save it:
   ```powershell
   Import-Module posh-git
   ```

> After this, your terminal will show your current Git branch and status in the prompt automatically.

### c) What Will I Use It For?

- Storing engineering design files
- Maintaining organized version control for documents, ECRs, and more
- Managing test data and project tracking with GitHub Projects instead of email chains

---

## 4. Practicing Version Control Concepts

### ① Clone a Repository

Before you can work on a project, you need a local copy of it.

| Concept | What it means |
|---|---|
| **Repository (repo)** | A folder tracked by Git — contains all files, history, and branches |
| **Branch** | A parallel version of the repo where you can make changes safely |
| **Cloning** | Downloading a copy of a remote GitHub repo to your local machine |

**What you can see on GitHub:**
- Files & folders
- Releases
- Branches
- Projects
- Downloading the repo as a ZIP

---

### ② Being Conscious of Your Git Repo

> You are no longer working on a project by yourself. This is a **shared repository** that needs special consideration.

If you want to work on files as if they are your own, **create your own branch** first. Name the branch after whatever the reason for branching is — you can always change it later.

**Branch naming examples:**
```
tims-branch
ECR-evt1-to-evt2
pcb-changes
updating-transformer-footprint
```

To create and switch to your new branch:
```bash
git checkout -b <branch-name>
```

---

### ③ Make Your Changes

Once you're on your own branch, make your edits freely.

If you ever want to see what the original files looked like, you can switch back to `main` at any time:
```bash
git checkout main
```

---

### ④ Save and Share Your Work

When you're ready to save your progress and push it to GitHub:

```bash
git add .
git commit -m "describe what you changed here"
git push origin <branch-name>
```

---

### ⑤ What If Main Changed While You Were Working?

While you were on your branch, someone else may have pushed updates to `main`. Here's how to check and sync:

```bash
git checkout main   # switch back to main
git fetch           # download any updates from GitHub (doesn't change your files yet)
git status          # see what changed and what's different
git pull --rebase   # apply those changes to your local machine
```

> `git pull --rebase` replays your local changes on top of the updated `main`, keeping the history clean.

---

## 5. Quick Reference

| Command | What it does |
|---|---|
| `git checkout -b <name>` | Create and switch to a new branch |
| `git checkout main` | Switch back to the main branch |
| `git add .` | Stage all changed files |
| `git commit -m "message"` | Save a snapshot with a description |
| `git push origin <branch>` | Upload your branch to GitHub |
| `git fetch` | Check for remote updates (safe, no changes yet) |
| `git status` | See what files have changed |
| `git pull --rebase` | Sync your local copy with the latest from GitHub |

---

*Questions? Reach out to your team lead or open an issue in this repository.*
