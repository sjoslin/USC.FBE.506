---
title: VS Code Overview
parent: Installing Local Python and Local AI
layout: default
nav_order: 2
permalink: /install/vscode/
---

# VS Code Overview

> **Optional.** The setup pages tell you what to install. This explains what you're getting.

VS Code is a text editor that knows about code. You'll spend more time in it than in anything else this semester, so it's worth five minutes understanding the parts rather than discovering them by accident.

---

## Why not just use Colab?

Colab is a notebook in a browser tab, and for a single self-contained exercise it's excellent. Three things run out as the work gets bigger.

**Nothing persists.** The machine is thrown away when your session ends, so your files and your installed packages go with it. That's fine for one notebook and painful for a project you return to across weeks.

**It's one file at a time.** Real analysis spreads across a notebook, a data file, a script of helper functions and a spreadsheet of results. Colab shows you one of those.

**An agent can't reach your work.** This is the one that decides it. An AI agent is useful in proportion to what it can see and change. In Colab it can suggest code you paste; in an editor it reads your actual files, edits them, runs them, and shows you exactly what changed.

Colab still works, and nothing here takes it away. It's a fine place to try something in thirty seconds.

---

## The parts of the window

**Explorer**, down the left: the files in the folder you opened. VS Code is always pointed at one folder, and that folder is the project. This matters more than it sounds, because it's also the boundary we give the AI agent.

**Editor**, the middle: your files, in tabs. Notebooks open here and run cell by cell, the same as Colab.

**Terminal**, along the bottom (`Ctrl-` backtick): a command line already pointed at your project, with the right Python active. Use this one rather than the Terminal app, and a whole category of problem never happens.

**Activity bar**, far left: the icons that switch what the sidebar shows. Files, search, source control, extensions, and Codex.

---

## Extensions

VS Code on its own is a plain editor. Extensions teach it specific languages and tools, and the three we install do this:

**Python** gives you the interpreter picker, the debugger, and autocomplete that knows what a DataFrame is. It pulls in Pylance for you, so don't install that separately.

**Jupyter** runs `.ipynb` notebooks inside the editor, so you get your notebooks without the browser tab.

**Data Wrangler** is the one you won't expect to like. Click a DataFrame and you get a spreadsheet view with a distribution and a missing-value count for every column. Filter, drop, convert types by clicking, and it writes the pandas code for what you did. For a course where half the work is finding out what's actually in the data, it earns its place.


---

## The one thing that goes wrong

VS Code has to be told which Python to use, and if it picks the wrong one your notebook will insist pandas isn't installed when you can see that it is.

The interpreter shows in the bottom-right for a script, and in the top-right for a notebook, where it's called the **kernel**. It should read `.venv`. If it reads something else, click it and choose the one with `.venv` in the path.

That's the single most common problem in this course, it has one fix, and it's that. ([the full explanation]({{ site.baseurl }}/optional/environments/#which-python-am-i-running))

---

## Worth learning early

Three things that pay for themselves in the first week:

- **`⌘-Shift-P`** (`Ctrl-Shift-P` on Windows) opens the Command Palette, which can run anything VS Code does. If you can't find a menu item, it's in there.
- **`⌘-P`** jumps to a file by typing part of its name.
- **Save triggers everything.** Formatting, error checking, and the agent seeing your current file all key off a save.
