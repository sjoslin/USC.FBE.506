---
title: PC Setup
parent: Setup
layout: default
nav_order: 2
permalink: /install/windows/
---

# Setting Up Your PC

By the end of this page you'll have Python, an editor, and an AI coding agent, all working together. About twenty minutes, most of it waiting for downloads.

You don't need to understand what each command does. If you'd like to, [Python Environments]({{ site.baseurl }}/optional/environments/) explains the Python half.

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

Your project is `~\fbe506`. The `.venv` folder inside it holds this project's Python and its packages, and that's what your code will use.

uv also keeps a shared download cache and its downloaded Python versions under `%LOCALAPPDATA%\uv`, outside the project. Both are shared across every project, which is why a second project costs almost no time or disk.

What matters is that no package was installed into any Python that Windows manages, and nothing here is shared between projects in a way that can conflict. Delete `~\fbe506` and this project is gone. `uv cache clean` reclaims the cache if you ever want the space.

[What just happened]({{ site.baseurl }}/optional/environments/)

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

# Optional, but nicer to look at than the default.
code --install-extension Catppuccin.catppuccin-vsc        # colour theme
code --install-extension Catppuccin.catppuccin-vsc-icons  # matching file icons
```

To switch to it: `Ctrl-Shift-P`, then **Preferences: Color Theme**, then **Catppuccin Latte** for light or **Catppuccin Mocha** for dark.

**Data Wrangler** is the one you won't expect to like. Click any DataFrame and you get a spreadsheet view with a distribution and a missing-value count for every column. Clean it by clicking, and it writes the pandas code for what you did.

---

## 4. Codex

```powershell
winget install --id OpenAI.Codex -e
code --install-extension openai.chatgpt
```

**Close PowerShell and open a new one**, then sign in:

```powershell
codex login
```

This opens a browser. **Choose the USC workspace, not a personal account.** USC's plan gives you 6,500 credits a month. A personal account gives you a free-tier trickle that runs out around week three.

Out of the box Codex can only *write* inside the folder you have open, which the operating system enforces. But it can *read* anything on your computer. That is a fairly weak sandbox. [Better Sandboxing]({{ site.baseurl }}/optional/sandboxing/) shows how to run the agent inside a container instead, where the rest of your files are not there to be read.

---

## When something breaks

**`'uv' is not recognized`** (or `code`, or `codex`): you're in the PowerShell window you had open before installing it. Close it and open a new one.

**Codex stops to ask permission**: the settings file didn't load. Confirm it exists with `type $HOME\.codex\config.toml`, then quit and reopen VS Code.

---

## A note on WSL

Older guides tell you to install the Windows Subsystem for Linux first. You don't need it. Codex runs natively on Windows with a real sandbox, and everything in this course works in plain PowerShell.

## Next

[Using VS Code for Python]({{ site.baseurl }}/install/vscode/python/)
