---
title: PC Setup
layout: default
nav_order: 2
permalink: /windows/
---

# Setting Up Your PC

By the end of this page you'll have Python, an editor, and an AI coding agent, all working together. About twenty minutes, most of it waiting for downloads.

You don't need to understand what each command does. If you'd like to, [Python and uv]({{ site.baseurl }}/python/) explains the Python half.

Open **PowerShell** (Start menu, type "PowerShell") and work down the page.

> **After every install, close PowerShell and open a new one.** Windows only notices a newly installed command in a fresh window. This is the single most common reason a step appears not to work.

---

## 0. Check winget

Windows installs software from the command line with `winget`, which is already on your PC.

```powershell
winget --version
```

If that fails, install **App Installer** from the Microsoft Store and try again.

---

## 1. Python

```powershell
# uv manages Python itself, this project's packages, and the folder
# that keeps them separate from everything else on your PC.
winget install --id astral-sh.uv -e
```

**Close PowerShell and open a new one.** Then:

```powershell
# The folder all your course work will live in.
mkdir ~\fbe506
cd ~\fbe506

# Mark this folder as a project, using Python 3.12.
uv init --python 3.12

# Install the packages this course uses. The backtick continues the line.
uv add pandas numpy matplotlib statsmodels scikit-learn `
       yfinance pandas-datareader jupyter openpyxl
```

**Check:** `uv run python -c "print('hello world')"`

Everything landed in `~\fbe506`. Nothing was installed system-wide, so none of this can break anything else, and deleting that folder undoes all of it.

[What just happened]({{ site.baseurl }}/python/)

---

## 2. VS Code

```powershell
winget install --id Microsoft.VisualStudioCode -e
```

**Close PowerShell and open a new one.**

**Check:** `code --version`

---

## 3. Extensions

```powershell
code --install-extension ms-python.python        # Python support
code --install-extension ms-toolsai.jupyter      # notebooks in the editor
code --install-extension ms-toolsai.datawrangler # point-and-click data cleaning
code --install-extension charliermarsh.ruff      # flags mistakes as you type
```

**Data Wrangler** is the one you won't expect to like. Click any DataFrame and you get a spreadsheet view with a distribution and a missing-value count for every column. Clean it by clicking, and it writes the pandas code for what you did.

---

## 4. Codex

```powershell
winget install --id OpenAI.Codex -e
code --install-extension openai.chatgpt
```

**Close PowerShell and open a new one.** Then write its settings file. Paste the whole block at once, and make sure the closing `'@` sits at the very start of its line with no spaces before it:

```powershell
New-Item -ItemType Directory -Force -Path "$HOME\.codex" | Out-Null

@'
sandbox_mode    = "workspace-write"
approval_policy = "never"

[sandbox_workspace_write]
network_access = true
'@ | Set-Content -Encoding utf8 "$HOME\.codex\config.toml"
```

Then sign in:

```powershell
codex login
```

This opens a browser. **Choose the USC workspace, not a personal account.** USC's plan gives you 6,500 credits a month. A personal account gives you a free-tier trickle that runs out around week three.

Those three settings are the important part of this page:

- **`workspace-write`**: Codex can read anything, but can only *write* inside the folder you have open. It can't touch the rest of your PC.
- **`approval_policy = "never"`**: it won't interrupt you to ask permission, because the line above already answered the question.
- **`network_access = true`**: it can reach the internet, which it needs for every data download in this course.

---

## 5. Your first notebook

```powershell
code ~\fbe506
```

By hand, once, so you know what the pieces are:

1. `Ctrl+Shift+P`, then **Create: New Jupyter Notebook**
2. Top right, the kernel should already say **.venv**. If it doesn't, click it and choose the one ending in `.venv\Scripts\python.exe`.
3. First cell: `import pandas as pd` then `print(pd.__version__)`. Press `Shift+Enter`.
4. Save it as `hello.ipynb`.

Then the same job with the agent. In the **Codex** panel:

> make a new notebook that downloads the last year of SPY prices and plots the closing price

It writes the file, runs it, and shows you the result. It never stops to ask permission, and it can't write anywhere outside `~\fbe506`.

That's the setup. You're done.

---

## When something breaks

**`'uv' is not recognized`** (or `code`, or `codex`): you're in the PowerShell window you had open before installing it. Close it and open a new one.

**A notebook says pandas isn't installed**: it's running the wrong Python. Click the kernel name in the top right and choose the one ending in `.venv\Scripts\python.exe`. ([why]({{ site.baseurl }}/python/#which-python-am-i-running))

**The `@'` block gave an error**: the closing `'@` has to be at the very beginning of a line, with nothing before it. Re-paste the whole block.

**Codex stops to ask permission**: the settings file didn't load. Confirm it exists with `type $HOME\.codex\config.toml`, then quit and reopen VS Code.

**Codex writes files but can't download anything**: `network_access = true` is missing from that file.

**You need a package that isn't installed**: `uv add <name>` in PowerShell, from inside `~\fbe506`. Then restart the notebook's kernel.

---

## A note on WSL

Older guides tell you to install the Windows Subsystem for Linux first. You don't need it. Codex runs natively on Windows with a real sandbox, and everything in this course works in plain PowerShell.
