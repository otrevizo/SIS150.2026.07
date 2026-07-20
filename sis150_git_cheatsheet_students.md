# Git & GitHub for Beginners — SIS150 Student Guide

Oscar A. Trevizo, Visiting Professor
College of Engineering and Information Science, DeVry University
SIS150 — Fundamentals of Programming | Session 2026.07

A from-scratch guide to using **git from the Terminal** — no prior git
knowledge assumed, no GitHub Desktop required. Works the same way on
**Mac and Windows** once your terminal is set up (see Step 1).

---

## What are git and GitHub, really?

- **git** is a program on your computer that tracks changes to your files
  over time — like unlimited "save points" you can return to.
- **GitHub** is a website that stores a copy of your git project ("repository,"
  or "repo") online, so you can back it up, share it, and turn in your work.
- You'll type git commands into a **Terminal window**, not click around in an
  app. It looks intimidating at first — it becomes second nature fast.

---

## Step 1 — Install Git and Open a Terminal

### On Mac
1. Open **Terminal** (press `Cmd + Space`, type `Terminal`, hit Enter).
2. Type `git --version` and press Enter.
   - If it's already installed, you'll see a version number — skip to Step 2.
   - If not, macOS will prompt you to install the "Command Line Developer
     Tools." Click **Install** and wait a few minutes.

### On Windows
1. Download **Git for Windows**: https://git-scm.com/download/win
2. Run the installer. Accept the default options.
3. This installs **Git Bash** — open it from the Start menu.
   Use **Git Bash**, not the regular Command Prompt (CMD) or PowerShell —
   Git Bash uses the same commands as Mac Terminal, so this guide works
   for everyone without translating commands.
4. Type `git --version` and press Enter to confirm it installed.

From here on, "Terminal" means **Terminal** (Mac) or **Git Bash** (Windows) —
the commands are identical on both.

---

## Step 2 — Create a GitHub Account

1. Go to https://github.com and sign up (it's free).
2. Remember your **username** — you'll need it below.
3. If your instructor gave you an invite link to a class organization or
   repo, accept it now while logged in.

---

## Step 3 — Tell Git Who You Are (one-time setup)

Every commit records who made it. Set this once per computer:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the same email you used for your GitHub account.

Verify it worked:
```bash
git config --list
```

---

## Step 4 — Personal Access Token (PAT) — Your Password Replacement

GitHub no longer accepts your account password from the Terminal. Instead,
you create a **Personal Access Token (PAT)** — a long, random code that acts
as your password for git.

1. Go to https://github.com/settings/tokens
2. Click **Generate new token** → **Generate new token (classic)**
3. Give it a name, e.g. `My Laptop`
4. Set an expiration (90 days is fine for a course)
5. Check the box for **repo** scope
6. Click **Generate token**
7. **Copy it immediately** — GitHub only shows it once. Paste it somewhere
   safe (a notes app, a password manager) until you use it in Step 5.

> Think of the PAT like a temporary password just for git. If you lose it,
> generate a new one — it costs nothing.

---

## Step 5 — Clone Your First Repo

"Cloning" downloads a copy of a repo from GitHub to your computer.

```bash
# Pick (or create) a folder to keep your class repos in, e.g.:
cd ~
mkdir GitHub
cd GitHub

# Clone the repo (replace with your actual repo URL)
git clone https://github.com/username/repo-name.git

# Move into the repo you just downloaded
cd repo-name
```

The first time you push (Step 6), Terminal will ask for your **username**
and **password** — for password, paste the **PAT** from Step 4, not your
GitHub account password. After that, your computer remembers it and won't
ask again.

---

## Step 6 — The Daily Loop: The Only 3 Commands You Need Most Days

Every time you finish some work and want to save it to GitHub:

```bash
# 1. Stage — tell git which files to include
git add filename.py
git add .              # or: stage everything that changed

# 2. Commit — save a snapshot with a message describing what you did
git commit -m "Add loop that counts to 10"

# 3. Push — upload your commit to GitHub
git push
```

That's it. Repeat this every time you finish a chunk of work.

### Writing a good commit message
```bash
# Good — short and specific
git commit -m "Fix off-by-one error in for loop"
git commit -m "Add function to calculate average grade"

# Avoid — too vague to be useful later
git commit -m "stuff"
git commit -m "update"
```

---

## Step 7 — Checking Where You Stand

```bash
git status          # What's changed? What's staged? (use this constantly)
git log --oneline   # Your commit history, one line each
git diff filename   # Exactly what changed in a file, line by line
```

`git status` is your best friend — run it before and after every step
until the commands feel automatic.

---

## Step 8 — Getting Updates (Pull)

If your instructor updates the class repo, or you work from more than one
computer, download the latest changes before you start working:

```bash
git pull
```

Get in the habit: **pull before you start, push when you finish.**

---

## A Typical Session, Start to Finish

```bash
# 1. Open Terminal (Mac) or Git Bash (Windows)
cd ~/GitHub/repo-name

# 2. Get the latest version
git pull

# 3. Do your work — edit code, save your files

# 4. Check what changed
git status

# 5. Save your work
git add .
git commit -m "Complete Module 2 loop exercises"
git push
```

---

## Quick Reference Card

| Command | What it does |
|---|---|
| `git --version` | Check that git is installed |
| `git config --global user.name "..."` | Set your name (one-time) |
| `git clone <url>` | Download a repo to your computer |
| `git status` | Show what's changed / staged |
| `git add <file>` | Stage a file to be saved |
| `git add .` | Stage everything that changed |
| `git commit -m "message"` | Save staged changes with a description |
| `git push` | Upload your commits to GitHub |
| `git pull` | Download the latest changes from GitHub |
| `git log --oneline` | Show your commit history |
| `git diff <file>` | Show exact line-by-line changes |

---

## When Something Goes Wrong

**"Authentication failed" / "Invalid username or token" on `git push`**
Your PAT expired or was typo'd. Generate a new one (Step 4) and push again —
Terminal will prompt you for your username and the new PAT.

**"fatal: not a git repository"**
You're not inside a cloned repo folder. Run `cd repo-name` (or `cd` into the
right folder) and try again.

**`git commit` works but `git push` fails**
That's normal and fine — commits are saved locally first. Only `push` needs
internet + authentication. Fix the connection/auth issue, then `git push`
again; your commit is still there waiting.

**I'm stuck and nothing above helps**
Run `git status` and read what it says — it usually tells you exactly what
to do next. Then ask in office hours or post in Canvas.

---

*This guide intentionally covers only what you need to turn in coursework:
clone, add, commit, push, pull, status. Ask your instructor if you're
curious about branches, merging, or other git features.*
