---
title: PC Setup
parent: Setup
layout: default
nav_order: 2
permalink: /install/windows/
---

# Setting Up Your PC

**Disclaimer:** I use a Mac, so this is an AI translation of the Mac instructions to Windows.

Open **PowerShell** (open the Start menu and type "PowerShell"). Click in the upper right of each box to select and copy the text. Then paste it into PowerShell and press Enter.

There is a check at the end of each step. If a check fails, stop and paste the error message and the command into an AI, and have it help you solve it.

[Overview]({{ site.baseurl }}/overview/) describes what we are installing and why.

---

## 0. Check winget

Windows installs software from the command line with `winget`, which is normally already on your PC.

```powershell
winget --version
```

**Check:** `winget --version` prints a version number. If it does not, install **App Installer** from the Microsoft Store and try again.

---

## 1. Python

First, install uv:

```powershell
winget install --id astral-sh.uv -e # uv manages Python and its libraries
```

Close PowerShell and open a new PowerShell window so that Windows can find uv. Then run the commands below, replacing `~\fbe506` with whatever directory you want to use.

```powershell
mkdir ~\fbe506                    # create the folder for your work
cd ~\fbe506

uv init --python 3.12 --no-package # mark the folder as a Python project (once)

uv add pandas numpy              # tables and numerical calculations; creates .venv
uv add matplotlib                # charts and plots
uv add statsmodels scikit-learn  # statistics and machine learning
uv add yfinance pandas-datareader # download financial and economic data
uv add openpyxl                  # read and write Excel .xlsx files
uv add jupyter ipykernel         # Jupyter tools and the kernel for VS Code notebooks
```

Running `uv add` also creates the virtual environment (the `.venv` folder) that contains your project's Python interpreter and installed packages. The `.python-version` file records which Python version the project should use.

**Check:** `Get-ChildItem -Force` should show `.venv`. Then `uv run python -c "print('hello world')"` should print `hello world`.

---

## 2. VS Code

```powershell
winget install --id Microsoft.VisualStudioCode -e
```

Close PowerShell and open a new PowerShell window.

**Check:** `code --version` prints the version number. Also open the app from the Start menu, or type `code` in PowerShell.

---

## 3. Extensions

Now we will install several VS Code extensions. You can also install these manually in VS Code by using the Extensions menu (the four-square icon with one square tilted, or `Ctrl-Shift-X`).

```powershell
code --install-extension ms-python.python        # Python support
code --install-extension ms-toolsai.jupyter      # Use Python notebooks
code --install-extension ms-toolsai.datawrangler # point-and-click data cleaning

# Optional, but nicer to look at than the default.
code --install-extension Catppuccin.catppuccin-vsc        # color theme
code --install-extension Catppuccin.catppuccin-vsc-icons  # matching file icons
```

To switch to the color theme: `Ctrl-Shift-P`, then **Preferences: Color Theme**, then **Catppuccin Latte** for light, or **Catppuccin Frappé** or **Catppuccin Mocha** for dark. For the icons, `Ctrl-Shift-P`, then **Preferences: File Icon Theme**.

**Data Wrangler** helps us view DataFrames. We can also edit them in place.

**Check:** open VS Code. The Extensions panel (`Ctrl-Shift-X`) lists all five under Installed.

---

## 4. Codex

```powershell
winget install --id Git.Git -e              # version control used by Codex
irm https://chatgpt.com/codex/install.ps1 | iex # the Codex command-line tool
code --install-extension openai.chatgpt     # its VS Code panel
```

Close PowerShell and open a new PowerShell window, then sign in:

```powershell
codex login
```

`codex login` opens a browser for you to authenticate.

Codex runs directly in PowerShell and uses the native Windows sandbox. You do not need to install WSL2. Keep **Ask for approval** selected so that Codex stays within the sandbox and asks before doing anything that needs broader access. With your approval, Codex can write outside the open project. See the [OpenAI sandbox documentation](https://learn.chatgpt.com/docs/sandboxing) for the current defaults and options.

**Check:** `codex --version` prints a version number, and the Codex icon appears in VS Code's left sidebar.

---

## When something breaks

**`uv`, `code`, or `codex` is not recognized:** close PowerShell and open a new window. Windows may not make a newly installed command available to PowerShell windows that were already open.

**Codex asks for permission:** this is normal. The sandbox is stopping Codex before it accesses something outside the project or uses a restricted resource. Read the request before approving it.

---

## Why these instructions do not use WSL2

WSL2 gives Windows a Linux environment, but this course does not need one. Python, uv, VS Code, and Codex all run directly on Windows. Codex also provides a native Windows sandbox when it runs in PowerShell.

## Next

[Using VS Code for Python]({{ site.baseurl }}/install/vscode/python/)
