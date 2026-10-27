---
title: Mac Setup
parent: Setup
layout: default
nav_order: 1
permalink: /install/mac/
---

# Mac Setup

Open **Terminal** (`⌘-Space`, type "Terminal"). Click in the upper right of each box to select and copy the text. Then paste it into Terminal and press Enter.

Mac's default shell, zsh, needs this setting to accept the explanatory `#` comments in the commands below. Run it once in each new terminal before pasting commands with comments:

```zsh
setopt interactivecomments
```

There is a check at the end of each step. If a check fails, stop and paste the error message and the command into an AI, and have it help you solve it.

[Overview]({{ site.baseurl }}/overview/) describes what we are installing and why.

---

## 0. Homebrew

Homebrew is a package manager that helps install software for Mac. Brew makes it much easier than downloading and installing a bunch of `.dmg` files (and works for things not in the App Store).

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

---

## 2. VS Code

```bash
brew install --cask visual-studio-code
```

**Check:** `code --version` prints the version number. Also open the app from its icon, or type `code` in the terminal.

---

## 3. Extensions

Now we will install several VS Code extensions. You can also install these manually in VS Code by using the Extensions menu (the four-square icon with one square tilted, or `⌘-Shift-X`).

```bash
code --install-extension ms-python.python        # Python support
code --install-extension ms-toolsai.jupyter      # Use Python notebooks
code --install-extension ms-toolsai.datawrangler # point-and-click data cleaning

# Optional, but nicer to look at than the default.
code --install-extension Catppuccin.catppuccin-vsc        # color theme
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

Codex normally writes only inside the folder you have open. With approvals enabled, it can ask for permission to write outside that folder and can do so only if you approve. The active permissions profile also determines what Codex can read and whether commands can use the network. See the [OpenAI sandbox documentation](https://learn.chatgpt.com/docs/sandboxing) for the current defaults and options. [Better Sandboxing]({{ site.baseurl }}/optional/sandboxing/) will describe how to isolate the agent further.

**Check:** the Codex icon appears in VS Code's left sidebar.

---

## Next

[Using VS Code for Python]({{ site.baseurl }}/install/vscode/python/)
