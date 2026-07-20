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
3. This installs **Git Bash**. To open it, either:
   - Press the **Windows key**, type `Git Bash`, and press Enter — or
   - Right-click any empty space inside a folder in File Explorer (or on
     the Desktop) and choose **Git Bash Here** from the menu.

   Use **Git Bash**, not the regular Command Prompt (CMD) or PowerShell —
   Git Bash uses the same commands as Mac Terminal, so this guide works
   for everyone without translating commands. A black/dark window will
   open with a `$` prompt — that's it, you're in.
4. Type `git --version` and press Enter to confirm it installed.

From here on, "Terminal" means **Terminal** (Mac) or **Git Bash** (Windows) —
the commands are identical on both.

---

## Step 2 — Create a GitHub Account

1. Go to https://github.com and sign up (it's free).
2. Remember your **username** — you'll need it below.

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
6. Click **Generate token** — this creates your PAT, the password you'll
   use whenever you `git push` new code to GitHub (see Step 6).
7. **Copy it immediately** — GitHub only shows it once. Paste it somewhere
   safe (a notes app, a password manager) until you use it in Step 5.

> Think of the PAT like a temporary password just for git. If you lose it,
> generate a new one — it costs nothing.

> **When it expires:** after 90 days, `git push` will suddenly fail with an
> authentication error. This is normal — you don't need to reinstall
> anything or redo Steps 1-3. Just repeat **Step 4** to generate a fresh
> PAT, then push again; your computer will ask for the new one and
> remember it going forward. See "When Something Goes Wrong" below.

---

## Step 5 — Clone Your First Repo

Open **Terminal** (Mac) or **Git Bash** (Windows) — same as Step 1 — and
run the commands below there.

"Cloning" downloads a copy of a repo from GitHub to your computer. Let's
clone the actual SIS150 class repo as your first example:

```bash
# Pick (or create) a folder to keep your class repos in, e.g.:
cd ~
mkdir GitHub
cd GitHub

# Clone the SIS150 class repo
git clone https://github.com/otrevizo/SIS150.2026.07.git

# Move into the repo you just downloaded
cd SIS150.2026.07
```

You now have a local copy of everything in the class repo — the same
notebooks and materials your instructor shares, sitting right on your own
computer. (For any *other* repo later, just swap in that repo's URL.)

> **Note on this class repo:** it's a one-way street — from the instructor
> to you. You can clone and pull it to get the latest materials, but you
> cannot push to it (you don't have write access, and you don't need it).
> Step 6 below still matters — you'll use `push` on repos you create
> yourself or collaborate on, just not this one.

---

## Step 6 — The Daily Loop: The Only 3 Commands You Need Most Days

You'll use this loop on a repo you own or collaborate on — where you have
push access. (It does **not** apply to this class repo — see the note in
Step 5.)

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

The **first time** you push to a new repo, Terminal will ask for your
**username** and **password** — for password, paste the **PAT** from
Step 4, not your GitHub account password. After that, your computer
remembers it and won't ask again.

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

## Step 8 — Checking for New Material (Pull)

`git pull` is also how you check whether anything changed. When your
instructor posts a new notebook to the class repo, your local clone
doesn't update itself — you have to ask for it:

```bash
cd ~/GitHub/SIS150.2026.07
git pull
```

Two possible results:

- **Nothing new:** `Already up to date.` — your local copy already matches
  what's on GitHub.
- **Something new:** git lists the file(s) it just downloaded, e.g.
  `sis150_module5_inheritance.ipynb | 120 +++++`. Those files now exist in
  your folder.

Since this class repo is read-only for you (Step 5), `pull` is really all
you'll ever run here. Get in the habit of running it before each class —
own/collaborative repos are where the pull-then-push loop (Step 6) applies.

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
