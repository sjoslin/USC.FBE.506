---
title: Mac Setup
parent: Setup
layout: default
nav_order: 1
permalink: /install/mac/
---

# Mac Setup

Open **Terminal** (`⌘-Space`, type "Terminal"). Click in the upper right of each box to select and copy the text. Then paste it into terminal and hit enter.

Mac's default shell, zsh, needs this setting to accept the explanatory `#` comments in the commands below. Run it once in each new terminal before pasting commands with comments:

```zsh
setopt interactivecomments
```

There is a check at the end of each step. If a check fails, stop and paste the error message and the command into an AI, and have it help you solve it.

[Setup Overview]({{ site.baseurl }}/install/) describes what we are installing and why.

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

First, install uv:

```bash
brew install uv                  # uv manages Python and its libraries
```

Then run the commands below, replacing `~/fbe506` with whatever directory you want to use.

```bash
mkdir -p ~/fbe506                # create the folder for your work
cd ~/fbe506

uv init --python 3.12 --no-package # mark the folder as a Python project (once)

uv add pandas numpy             # tables and numerical calculations; creates .venv
uv add matplotlib               # charts and plots
uv add statsmodels scikit-learn # statistics and machine learning
uv add yfinance pandas-datareader # download financial and economic data
uv add openpyxl                 # read and write Excel .xlsx files
uv add jupyter ipykernel        # Jupyter tools and the kernel for VS Code notebooks
```

Running `uv add` also creates the virtual environment (the `.venv` folder) that contains your project's Python interpreter and installed packages. The `.python-version` file records which Python version the project should use.

**Check:** `ls -a` should show `.venv`. Then `uv run python -c "print('hello world')"` should print `hello world`.

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

Out of the box Codex can only _write_ inside the folder you have open, which the operating system enforces. But it can _read_ anything on your computer. That is a fairly weak sandbox. [Better Sandboxing]({{ site.baseurl }}/optional/sandboxing/) shows how to run the agent inside a container instead, where the rest of your files are not there to be read.

**Check:** the Codex icon appears in VS Code's left sidebar.

---

## Next

[Using VS Code for Python]({{ site.baseurl }}/install/vscode/python/)
