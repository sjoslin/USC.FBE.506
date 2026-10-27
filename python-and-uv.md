---
title: Python Environments
parent: Optional Topics
layout: default
nav_order: 1
permalink: /optional/environments/
published: false
---

# Python Environments

What the setup actually did, and enough of a model to debug it yourself when Python does something you don't expect.

---

## The problem this solves

In Colab, `!pip install yfinance` is the right answer. The machine is destroyed when your session ends, so nothing accumulates, nothing conflicts, and nothing can break. You reinstall every session because you have to.

Your laptop keeps everything. One shared pile of packages, growing all year, shared by every project you ever touch. Eventually two things want different versions of the same package and one of them quietly stops working, months after you caused it.

So each project gets its own packages instead.

---

## A virtual environment is a folder

That's the whole idea. `~/fbe506/.venv/` holds a copy of the Python interpreter and a `site-packages` directory containing pandas, numpy and the rest. When you run *that* Python, it looks for libraries in *that* folder. No magic, just a different place to look.

Two things follow:

- Installing something for this project can't affect anything else on your machine.
- Deleting `.venv` deletes the project's packages and nothing else. `uv sync` rebuilds it in seconds. That's your escape hatch when an environment gets wedged.

---

## Which Python am I running?

This is the question behind most Python confusion, including the notebook that insists pandas isn't installed.

When you type `python`, your shell searches the `PATH` variable, left to right, for a program with that name:

```
/opt/homebrew/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```

`~/fbe506/.venv/bin` isn't on that list. **Standing in the folder makes no difference**, because the shell doesn't look at your current directory. So in a plain Terminal window the project's Python is unreachable even though it's sitting right there.

Worse, your Mac has a Python of its own. Apple ships `/usr/bin/python3` with the Command Line Tools, which the Homebrew installer pulled in during step 0. It's old, it's meant for Apple's own tooling, and it has none of your packages. So this runs, and then fails in a way that looks like a broken install:

```bash
python3 test.py
# ModuleNotFoundError: No module named 'pandas'
```

**Activating an environment is one thing: putting `.venv/bin` at the front of `PATH`.** Not a Python feature, a shell variable edit. You can watch it happen:

```bash
cd ~/fbe506
which python                 # not found
ls .venv/bin                 # python, pip, jupyter, all right there

source .venv/bin/activate
which python                 # /Users/you/fbe506/.venv/bin/python

deactivate
```

Nothing was installed in between. One variable changed.

Three ways to reach the project's Python, and you only need the first:

| | |
|---|---|
| **VS Code's terminal** | does that `source` for you when it opens the project |
| `uv run python` | skips `PATH` and runs `.venv/bin/python` directly |
| `.venv/bin/python` | the full path, always works |

Notebooks don't use `PATH` at all. They use whichever interpreter VS Code handed them, which is why the fix for a notebook is the kernel picker in the top right rather than anything in a terminal.

**The short rule: run your code from inside VS Code.**

---

## The files in your project

```
~/fbe506/
  pyproject.toml    what this project needs
  uv.lock           the exact versions it got
  .python-version   3.12
  .venv/            the Python and the packages themselves
```

`pyproject.toml` is the standard description of a Python project. It's [TOML](https://toml.io), a config format of keys, values and `[section]` headers:

```toml
[project]
name = "fbe506"
version = "0.1.0"
requires-python = ">=3.12"
dependencies = [
    "pandas>=2.3.3",
    "seaborn>=0.13.2",
]
```

You never write this by hand. `uv init` created it empty, and every `uv add` appends a line.

`uv.lock` is generated, and you never edit it. It records every package, including ones you never asked for like seaborn's own requirements, pinned to an exact version with a checksum and a download URL.

The pair is the point: **`pyproject.toml` is what you asked for, `uv.lock` is what you got.** Hand someone both and `uv sync` reproduces your environment exactly, which is how "it works on my machine" stops being a thing.

---

## Where the packages actually are

Two places.

`~/.cache/uv/` is a download store shared by every project on your machine. The first time anything needs pandas 2.3.3, it's downloaded here.

`~/fbe506/.venv/lib/python3.12/site-packages/` is what gets imported, and uv fills it with **hardlinks** to the cache rather than copies. A hardlink is a second name for the same data on disk, so both are real files and the bytes exist once. Clear the cache and your `.venv` keeps working.

That's why a second project wanting the same pandas is instant and costs no extra disk.

```bash
uv run python -c "import pandas; print(pandas.__file__)"
```

prints the real location, which is a satisfying thing to run once.

---

## Adding a package

```bash
uv add seaborn
```

From inside `~/fbe506`. It writes the line into `pyproject.toml`, updates `uv.lock`, downloads to the cache if needed, and links it into `.venv`.

If a notebook is already open, **restart its kernel** or it won't see the new package.

Don't use `uv pip install`. It exists, it works, and it installs *without* recording anything in `pyproject.toml`, so the next `uv sync` silently removes what you installed.

---

## The standard library needs no install

`math`, `random`, `datetime`, `json`, `csv`, `statistics` and a few hundred others ship inside Python itself. They always work and never appear in `pyproject.toml`.

`pandas`, `numpy`, `yfinance` and the rest are third-party. Somebody has to install them.

`ModuleNotFoundError` is almost always you hitting that distinction, or running the wrong Python.

---

## Why uv rather than pip or conda

uv isn't an alternative to pip alone. It replaces four things:

| Job | Before | uv |
|---|---|---|
| Install Python itself | pyenv, or a download page | `uv python install` |
| Isolate the project | `python3 -m venv` plus activate | automatic |
| Install packages | `pip install` | `uv add` |
| Pin exact versions | pip-tools, by hand | `uv.lock` |

The conceptual difference is in the last two rows. With pip you *do* a sequence of installs, and your environment ends up as whatever that history left behind: unreconstructable, and different for everyone who typed slightly different commands. With uv the environment is *described* in a file, and `uv sync` makes reality match the description.

pip is a list of commands you ran. uv is a statement of what the project needs.

It's also much faster, which matters more than it sounds when sixty people install at once on campus wifi.

Nothing you learned in Colab becomes invalid. `!pip install` still works inside a notebook, because the notebook is already running in the environment.
