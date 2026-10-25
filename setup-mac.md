---
title: Mac Setup
layout: default
nav_order: 1
permalink: /mac/
---

# Setting Up Your Mac

By the end of this page you'll have Python, an editor, and an AI coding agent, all working together. About twenty minutes, most of it waiting for downloads.

You don't need to understand what each command does. If you'd like to, [Python and uv]({{ site.baseurl }}/python/) explains the Python half, and it's worth reading the first time something breaks.

Open **Terminal** (`Cmd+Space`, type "Terminal") and work down the page. Each step ends with a check. If a check fails, stop there rather than carrying on.

---

## 0. Homebrew

Homebrew installs software from the command line, so you don't go hunting for download pages.

```bash
# Download and run Homebrew's installer.
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Tell your shell where Homebrew put itself, now and in future sessions.
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

On a new Mac this first downloads Apple's Command Line Tools: a few minutes, and it asks for your password.

**Check:** `brew --version` prints a version number.

---

## 1. Python

```bash
# uv manages Python itself, this project's packages, and the folder
# that keeps them separate from everything else on your Mac.
brew install uv

# The folder all your course work will live in.
mkdir ~/fbe506
cd ~/fbe506

# Mark this folder as a project, using Python 3.12.
uv init --python 3.12

# Install the packages this course uses. A minute or so the first time.
uv add pandas numpy matplotlib statsmodels scikit-learn \
       yfinance pandas-datareader jupyter openpyxl
```

**Check:** `uv run python -c "print('hello world')"`

Everything landed in `~/fbe506`. Nothing was installed system-wide, so none of this can break anything else on your Mac, and deleting that folder undoes all of it.

[What just happened]({{ site.baseurl }}/python/)

---

## 2. VS Code

The editor. It runs your notebooks, and it's where the AI agent lives.

```bash
brew install --cask visual-studio-code
```

**Check:** `code --version` prints a version number.

---

## 3. Extensions

```bash
code --install-extension ms-python.python        # Python support
code --install-extension ms-toolsai.jupyter      # notebooks in the editor
code --install-extension ms-toolsai.datawrangler # point-and-click data cleaning
code --install-extension charliermarsh.ruff      # flags mistakes as you type
```

**Data Wrangler** is the one you won't expect to like. Click any DataFrame and you get a spreadsheet view with a distribution and a missing-value count for every column. Clean it by clicking, and it writes the pandas code for what you did.

**Check:** the Extensions panel (`Cmd+Shift+X`) lists all four under Installed.

---

## 4. Codex

```bash
# The agent itself, and its panel inside VS Code.
brew install --cask codex
code --install-extension openai.chatgpt

# Its settings file.
mkdir -p ~/.codex
cat > ~/.codex/config.toml <<'TOML'
sandbox_mode    = "workspace-write"
approval_policy = "never"

[sandbox_workspace_write]
network_access = true
TOML

# Sign in.
codex login
```

`codex login` opens a browser. **Choose the USC workspace, not a personal account.** USC's plan gives you 6,500 credits a month. A personal account gives you a free-tier trickle that runs out around week three.

Those three settings are the important part of this page:

- **`workspace-write`**: Codex can read anything, but can only *write* inside the folder you have open. It can't touch the rest of your computer.
- **`approval_policy = "never"`**: it won't interrupt you to ask permission, because the line above already answered the question.
- **`network_access = true`**: it can reach the internet, which it needs for every data download in this course.

**Check:** the Codex icon appears in VS Code's left sidebar.

---

## 5. Your first notebook

```bash
code ~/fbe506
```

By hand, once, so you know what the pieces are:

1. `Cmd+Shift+P`, then **Create: New Jupyter Notebook**
2. Top right, the kernel should already say **.venv**. If it doesn't, click it and choose the one ending in `.venv/bin/python`.
3. First cell: `import pandas as pd` then `print(pd.__version__)`. Press `Shift+Enter`.
4. Save it as `hello.ipynb`.

Then the same job with the agent. In the **Codex** panel:

> make a new notebook that downloads the last year of SPY prices and plots the closing price

It writes the file, runs it, and shows you the result. It never stops to ask permission, and it can't write anywhere outside `~/fbe506`.

That's the setup. You're done.

---

## When something breaks

**`command not found: brew`**: you skipped the two lines after the installer in step 0, or this Terminal window was open before you ran them. Open a new one.

**A notebook says pandas isn't installed**: it's running the wrong Python. Click the kernel name in the top right and choose the one ending in `.venv/bin/python`. ([why]({{ site.baseurl }}/python/#which-python-am-i-running))

**`python` doesn't work in Terminal**: use VS Code's built-in terminal rather than a Terminal window. ([why]({{ site.baseurl }}/python/#which-python-am-i-running))

**Codex stops to ask permission**: `~/.codex/config.toml` didn't load. Check the path and spelling, then quit and reopen VS Code.

**Codex writes files but can't download anything**: `network_access = true` is missing from that file.

**You need a package that isn't installed**: `uv add <name>` in Terminal, from inside `~/fbe506`. Then restart the notebook's kernel.

---

Later in the course: [running the agent in a container]({{ site.baseurl }}/containers/), once we want to take the guardrails off.
