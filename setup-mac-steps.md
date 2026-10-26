---
title: Mac Setup (Steps)
parent: Installing Local Python and Local AI
layout: default
nav_order: 5
permalink: /install/mac/steps/
---

# Mac Setup: The Steps

Open **Terminal** (`⌘-Space`, type "Terminal"). Click in the upper right of each box to select and copy the text. Then paste it into terminal and hit enter.

Each step ends with a check. If a check fails, stop and paste the error message and the command into an AI, and have it help you solve it.

[Mac Setup (Overview)]({{ site.baseurl }}/install/mac/) describes what is going on and what we are trying to install.

---

## 0. Homebrew

Homebrew is a package manager that helps install software for Mac. Brew makes it much easier than downloading and installing a bunch of dmg files (and works for things not in the app store.)

```bash
# Download and run Homebrew's installer.
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Tell your shell where Homebrew put itself, now and in future sessions.
# On an older Intel Mac, replace /opt/homebrew with /usr/local on both lines.
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**Check:** `brew --version` prints a version number.

---

## 1. Python

Run the commands below, replacing `~/fbe506` with whatever directory you want to use.

```bash
brew install uv                  # uv manages Python and its libraries

mkdir ~/fbe506                   # create the folder for your work
cd ~/fbe506

uv init --python 3.12            # mark the folder as a Python project

# Install some packages
uv add pandas numpy matplotlib statsmodels scikit-learn \
       yfinance pandas-datareader jupyter openpyxl
```

**Check:** `uv run python -c "print('hello world')"`

[Why do we install uv and not just Python?]({{ site.baseurl }}/optional/environments/)

---

## 2. VS Code

```bash
brew install --cask visual-studio-code
```

**Check:** `code --version` prints the version number. Also open the app from its icon, or type `code` in the terminal.

---

## 3. Extensions

Now we will install several VS Code extensions. You can also install these manually in VS Code by using the extensions menu (the four-square icon with one square tilted, or `⌘-Shift-X`)

```bash
code --install-extension ms-python.python        # Python support
code --install-extension ms-toolsai.jupyter      # Use Python notebooks
code --install-extension ms-toolsai.datawrangler # point-and-click data cleaning

# Optional, but nicer to look at than the default.
code --install-extension Catppuccin.catppuccin-vsc        # colour theme
code --install-extension Catppuccin.catppuccin-vsc-icons  # matching file icons
```

To switch to the color theme: `⌘-Shift-P`, then **Preferences: Color Theme**, then **Catppuccin Latte** for light, or **Catppuccin Frappé** or **Catppuccin Mocha** for dark. For the icons, `⌘-Shift-P`, then **Preferences: File Icon Theme**.

**Data Wrangler** helps us view DataFrames. We can also edit them in place.

**Check:** open VS Code. The Extensions panel (`⌘-Shift-X`) lists all five under Installed.

---

## 4. Codex

```bash
brew install --cask codex                   # the agent itself
code --install-extension openai.chatgpt     # its VS Code panel

codex login                                 # sign in
```

`codex login` opens a browser for you to authenticate.

Out of the box Codex can only *write* inside the folder you have open, which the operating system enforces. But it can *read* anything on your computer. That is a fairly weak sandbox. [Better Sandboxing]({{ site.baseurl }}/optional/sandboxing/) shows how to run the agent inside a container instead, where the rest of your files are not there to be read.

**Check:** the Codex icon appears in VS Code's left sidebar.

---

## 5. Your first notebook

```bash
code ~/fbe506
```

By hand, once, so you know what the pieces are:

1. `⌘-Shift-P`, then **Create: New Jupyter Notebook**
2. Top right, the kernel should already say **.venv**. If it doesn't, click it and choose the one ending in `.venv/bin/python`.
3. First cell: `import pandas as pd` then `print("hello world!")`. Press `Shift+Enter`.
4. Save it as `hello.ipynb`.

Then we can write a sample file using the agent. In the **Codex** panel:

> make a new Python notebook that prints "hello world!!" then execute it.

---

## When something breaks

**A notebook says pandas isn't installed**: it's running the wrong Python. Click the kernel name in the top right and choose the one ending in `.venv/bin/python`. ([why]({{ site.baseurl }}/optional/environments/#which-python-am-i-running))

**`python` doesn't work in Terminal**: use VS Code's built-in terminal rather than a Terminal window. ([why]({{ site.baseurl }}/optional/environments/#which-python-am-i-running))

**You need a package that isn't installed**: `uv add <name>` in Terminal, from inside your directory. Then restart the kernel.
