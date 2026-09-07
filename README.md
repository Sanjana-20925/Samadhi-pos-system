# Git Workflow Guide — Samadhi POS System

This guide explains how our team should use Git for this project. It's written for people who are new to Git, so read it fully before you start pushing code.

Repo: https://github.com/Tharu-fernando/Samadhi-pos-system.git

---

## 1. One-Time Setup (do this once per computer)

1. **Install Git**
   - Download from https://git-scm.com/downloads and install it.
   - Check it worked by opening a terminal (Command Prompt / Git Bash) and typing:
     ```
     git --version
     ```

2. **Set your identity** (so your commits are labeled with your name):
   ```
   git config --global user.name "Your Name"
   git config --global user.email "your_email@example.com"
   ```

3. **Clone the repo** — this downloads a copy of the project to your computer:
   ```
   git clone https://github.com/Tharu-fernando/Samadhi-pos-system.git
   ```
   This creates a folder called `Samadhi-pos-system`. Open this folder as your project in NetBeans (File → Open Project).

You only need to clone **once**. After that, you `pull` to get updates instead of cloning again.

---

## 2. Core Concepts (read this before doing anything else)

- **Repository (repo):** The project folder tracked by Git, containing full history of changes.
- **Commit:** A saved snapshot of your changes, with a message describing what you did.
- **Branch:** A separate line of work. `main` is our official, stable branch. Nobody should code directly on `main`.
- **Push:** Upload your commits from your computer to GitHub.
- **Pull:** Download the latest commits from GitHub to your computer.
- **Merge / Pull Request (PR):** The process of combining a branch's changes into `main`.

**Golden rule:** Always work on your own branch, never directly on `main`.

---

## 3. Daily Workflow

### Step 1 — Pull the latest changes before you start working
Always do this first, every time you sit down to code:
```
git checkout main
git pull origin main
```

### Step 2 — Create a new branch for your task
Name it after what you're doing, e.g. `feature/inventory-page`, `fix/login-bug`.
```
git checkout -b feature/inventory-page
```
This creates the branch and switches you into it.

### Step 3 — Work in NetBeans as normal
Edit code, run/test it, etc. Git doesn't do anything automatically — it only tracks changes when you tell it to.

### Step 4 — Stage and commit your changes
Check what changed:
```
git status
```
Stage the files you want to save (or `.` for everything):
```
git add .
```
Commit with a clear message:
```
git commit -m "Add inventory search feature"
```

### Step 5 — Push your branch to GitHub
```
git push origin feature/inventory-page
```
(First time pushing that branch, Git may suggest the exact command — you can just copy-paste it.)

### Step 6 — Open a Pull Request (PR) on GitHub
1. Go to the repo on GitHub — you'll see a banner suggesting your recently pushed branch.
2. Click **"Compare & pull request."**
3. Add a short description of what you changed.
4. Click **"Create pull request."**
5. Ask a teammate (or me) to review it before merging into `main`.

### Step 7 — After the PR is merged
Switch back to `main` and pull the merged changes:
```
git checkout main
git pull origin main
```
You can delete your old branch locally if you're done with it:
```
git branch -d feature/inventory-page
```

---

## 4. Handling Conflicts

If two people edit the same lines in the same file, Git will flag a **merge conflict** when pulling or merging. Don't panic:
1. Git marks the conflicting lines in the file with `<<<<<<<`, `=======`, `>>>>>>>`.
2. Open the file in NetBeans, decide which version (or combination) is correct, and remove the conflict markers.
3. Save the file, then:
   ```
   git add <filename>
   git commit -m "Resolve merge conflict"
   ```
4. Push as normal.

If you're unsure, message the team before resolving — don't just pick randomly and push.

---

## 5. Using Git Inside NetBeans (optional GUI alternative)

NetBeans has built-in Git support so you don't have to use the terminal:
- Right-click the project → **Git** → options like `Commit`, `Push`, `Pull`, `Create Branch`, `Switch Branch` appear there.
- Under the hood it runs the exact same commands as above — so understanding the terminal commands still helps when something goes wrong.

---

## 6. Rules for This Project

1. Never commit directly to `main` — always use a branch + PR.
2. Pull before you start working, every session.
3. Commit often, with clear messages (not "update" or "fix stuff").
4. Don't commit build files, `.class` files, NetBeans local settings, or database credentials. Add these to a `.gitignore` (see below).
5. If you break something and don't know how to fix it, stop and ask — don't force-push over the team's work.

---

## 7. Suggested `.gitignore`

If not already in the repo, add a file named `.gitignore` in the root with:
```
# NetBeans
nbproject/private/
build/
dist/
*.class

# OS files
.DS_Store
Thumbs.db
```

---

## 8. Quick Reference Cheat Sheet

| Task                          | Command                                      |
|-------------------------------|-----------------------------------------------|
| Clone repo                    | `git clone <url>`                            |
| Check status                  | `git status`                                 |
| Switch to main                | `git checkout main`                          |
| Pull latest changes           | `git pull origin main`                       |
| Create + switch to new branch | `git checkout -b branch-name`                |
| Switch to existing branch     | `git checkout branch-name`                   |
| Stage changes                 | `git add .`                                  |
| Commit changes                | `git commit -m "message"`                    |
| Push branch                   | `git push origin branch-name`                |
| See branch list               | `git branch`                                 |
| See commit history            | `git log --oneline`                          |

---

Questions? Ask in the group chat before force-pushing, resetting, or rebasing anything — those commands can rewrite history and are easy to get wrong as a beginner.
