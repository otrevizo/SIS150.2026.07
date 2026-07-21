# Running Python & Jupyter on Your Own Computer (Optional) — SIS150

Oscar A. Trevizo, Visiting Professor
College of Engineering and Information Science, DeVry University
SIS150 — Fundamentals of Programming | Session 2026.07

**You don't need this.** Everything for this course works fine in
**Google Colab**, which runs in your browser with nothing to install.
This guide is for anyone who *wants* the option of running Python on
their own Mac or Windows machine too — useful if you want code that
works without internet access, or you're starting to build your own
projects outside of class.

---

## Colab vs. running locally — what's actually different

- **Colab**: Google runs Python for you, in the cloud. Nothing to
  install, nothing to maintain, works the moment you open a link.
- **Running locally**: the exact same Jupyter notebook interface, but
  Python runs *on your computer*. Same language, same notebooks, same
  code. The tradeoff is that **you're now responsible for keeping it
  working** — installing Python itself, installing JupyterLab, and
  installing any library a notebook needs (more on that below).

If that maintenance doesn't sound appealing, stick with Colab — nothing
in this course requires the local setup.

---

## Step 1 — Install Python

### On Mac
1. Go to [python.org/downloads](https://www.python.org/downloads/) and
   download the latest Python 3 installer for macOS.
2. Run the installer, following the prompts.
3. After installing, open the **Python 3.x** folder in your
   **Applications** folder and double-click **Install Certificates.command**.
   (This step is easy to miss and easy to forget — skipping it causes
   confusing network errors later, so don't skip it.)

### On Windows
1. Go to [python.org/downloads](https://www.python.org/downloads/) and
   download the latest Python 3 installer for Windows.
2. Run the installer. On the very first screen, check the box
   **"Add python.exe to PATH"** before clicking Install — this is the
   step people most often miss, and without it your computer won't know
   where to find Python afterward.

### Verify it worked (both platforms)
Open **Terminal** (Mac) or **Command Prompt / PowerShell** (Windows) and run:
```bash
python3 --version
```
(On Windows, if that doesn't work, try `python --version` instead.)
You should see something like `Python 3.13.x`.

---

## Step 2 — Create a Virtual Environment

Colab quietly gives every notebook its own clean, isolated copy of
Python. Running locally, that isolation doesn't happen automatically —
if you skip this step, every library you ever install for any project
piles into the same global Python, and eventually two projects will want
different, conflicting versions of the same library. A **virtual
environment** ("venv") is Python's own built-in fix: a self-contained
folder holding its own private copy of Python and libraries, one per
project.

This is standard professional practice, not a SIS150 quirk — every
Python job you'd ever apply for assumes you already do this.

```bash
# Inside your project folder, create the environment (name it "venv" --
# this is the standard name, not something specific to this course):
python3 -m venv venv

# Activate it -- Mac:
source venv/bin/activate

# Activate it -- Windows, using Git Bash (same command as Mac, since
# Git Bash behaves like a Unix terminal even on Windows):
source venv/Scripts/activate
```

Once activated, your prompt will show `(venv)` at the start of the
line — that's your confirmation it's active. **You'll need to activate
it every time** you open a new Terminal / Git Bash window to work on
this project; it doesn't stay active permanently. To turn it off:
```bash
deactivate
```

---

## Step 3 — Install and Launch JupyterLab

With your `venv` activated (you should see `(venv)` in your prompt):
```bash
pip3 install jupyterlab
```
(On Windows, if `pip3` isn't recognized, try `pip install jupyterlab`.)

Then launch it any time with:
```bash
jupyter lab
```
This opens JupyterLab in your browser — same notebook interface as
Colab, just talking to Python on your own machine instead of Google's.

---

## Your Daily Routine (Every Time You Come Back)

Steps 1 and 2 above are **one-time setup**. From now on, every time you
sit down to work, it's just this:

```bash
cd path/to/your/project     # go to your project folder
source venv/bin/activate    # Mac (Windows Git Bash: source venv/Scripts/activate)
jupyter lab                 # start it up
```

**What actually happens when you run `jupyter lab`:** it starts a small
program (a "server") running quietly in that Terminal window, then opens
a tab in your regular web browser pointing at something like
`http://localhost:8888/lab?token=...`. That odd-looking address just
means "the Jupyter server running on *this* computer" — `localhost`
always means "me, right here," not the internet. **The browser is just
a window into it, not the thing actually running your code** — the real
work happens in the Terminal, in the background.

A few things that trip people up the first time:

- **Leave that Terminal window open** while you work. It looks like
  nothing is happening in it, but closing it shuts the server down and
  your notebook disconnects.
- **If you accidentally close the browser tab** (not the Terminal),
  nothing is lost — just look at the Terminal window, find that
  `http://localhost:8888/...` address it printed, and open it in a new
  browser tab to reconnect.
- **When you're done for the day:** close the browser tab, click back
  into the Terminal, and press `Ctrl + C` (you may need to confirm) to
  stop the server. Then `deactivate` to exit the `venv`.
- **Next time:** you're not starting over — just repeat the three
  commands above.

---

## The "babysitting" part — installing libraries

Colab comes with most common libraries already installed. Running
locally, you install them yourself, one at a time, only when a notebook
actually needs one you don't have -- and always with your `venv`
activated, so the library lands in this project's environment and
nowhere else.

If you run a cell and see an error like:
```
ModuleNotFoundError: No module named 'pandas'
```
that means the library named in the error (`pandas`, in this example)
isn't installed yet. Fix it from Terminal / Command Prompt:
```bash
pip3 install pandas
```
Then go back and re-run the cell — it'll work now. This is the ongoing
maintenance cost of running locally: every new library a notebook uses,
you install once, and you're set for good on that machine.

---

## Quick decision guide

| Situation | Use |
|---|---|
| Doing coursework, following along in class | **Colab** |
| Want Python available without internet | Local install |
| Starting your own project outside this course | Local install |
| Not sure / don't want to think about it | **Colab** — it just works |
