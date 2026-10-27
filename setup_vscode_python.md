---
title: Using VS Code for Python
layout: default
nav_order: 3
permalink: /install/vscode/python/
---

# Using VS Code for Python

After [Mac Setup]({{ site.baseurl }}/install/mac/) or [PC Setup]({{ site.baseurl }}/install/windows/), continue here. These are the steps you will use as you work, on either platform.

## Open your project

Choose **File → Open Folder** and open your course folder (`fbe506` if you used the setup instructions). Open the folder rather than just a notebook so you can see the project's files and its `.venv` environment together.

## The parts of the window

![VS Code with the Explorer on the left, a notebook in the center, the terminal below, and Codex on the right.]({{ site.baseurl }}/assets/images/vscode-window.png)

- **Activity bar:** the strip of icons at the far left. Use these to switch between files, search, source control, and extensions.
- **Explorer:** the file list on the left. It shows the folder you opened, including your notebooks and `.venv`.
- **Editor:** the main area in the center. Files open in tabs; notebooks have cells you can run individually.
- **Terminal:** the panel below the editor. Open it with **Terminal → New Terminal** to run commands in your project folder.
- **Codex panel:** the assistant shown on the right in this screenshot. Its position can vary with your layout.
- **Status bar:** the strip along the bottom. When a Python script is active, it includes the selected interpreter. A notebook has its own kernel picker at the top right.

You can move panels and resize them by dragging their borders. Your window does not have to match this arrangement exactly.

## Create your first notebook

1. Open the **Command Palette** with `⌘-Shift-P` on Mac or `Ctrl-Shift-P` on Windows. Search for **Create: New Jupyter Notebook**.
2. Click **Select Kernel** at the top right (or click the current kernel's name). Choose **Select Another Kernel → Python Environments** if needed.
3. Select the Python inside your project's `.venv`. On Mac its path ends in `.venv/bin/python`; on Windows it ends in `.venv\Scripts\python.exe`. The displayed name may be your project's name rather than `.venv`.

![The Python environment picker, with the project's .venv/bin/python highlighted above other Python installations.]({{ site.baseurl }}/assets/images/vscode-python-environment.png)

The **kernel** is the Python process that runs your notebook. Choosing it tells the notebook which Python and installed packages to use.

Enter this in the first code cell:

```python
import pandas as pd
print("hello world!")
print(pd.__version__)
```

Press `Shift-Enter` to run the cell, then save the notebook as `hello.ipynb` in your project folder.

If `.venv` is missing from the picker, open **Terminal → New Terminal** and run this from the project folder:

```bash
uv add ipykernel
```

Then reopen the picker. If necessary, run **Developer: Reload Window** from the Command Palette and try again.

## The terminal and your Python environment

The terminal and the notebook have separate Python selections. Activating an environment in the terminal does not select the notebook's kernel.

VS Code may activate `.venv` automatically in a new terminal. To run your project's Python without relying on activation, use:

```bash
uv run python -c "import sys; print(sys.executable)"
```

The printed path should point inside your project's `.venv`. See [Python Environments]({{ site.baseurl }}/optional/environments/#which-python-am-i-running) for more detail.

## Add packages

Open **Terminal → New Terminal**, check that you are in the project folder, and run `uv add` with the package name. For example:

```bash
uv add seaborn
```

Restart the notebook kernel using **Restart** in the notebook toolbar, then run your cells again. Restarting clears variables from the previous session.

## Use the coding assistant

Open the **Codex** panel and try a small task:

> Create a Python notebook that prints "hello world!" and explain how I can run it.

Open the resulting file, check the selected kernel, and run the cells yourself. The [Codex Overview]({{ site.baseurl }}/install/codex/) explains the assistant in more detail.

## Useful shortcuts

| Action | Mac | Windows |
|---|---|---|
| Command Palette | `⌘-Shift-P` | `Ctrl-Shift-P` |
| Find a file by name | `⌘-P` | `Ctrl-P` |
| Save | `⌘-S` | `Ctrl-S` |
| Run a notebook cell | `Shift-Enter` | `Shift-Enter` |

## When something breaks

**A notebook says pandas isn't installed:** check the kernel at the top right. Choose your project's `.venv`, then rerun the cell. Installing pandas in a different Python will not make it available to this notebook.

**A command uses the wrong Python:** run it with `uv run` from the project folder. The notebook kernel and terminal environment are separate.

**A newly installed package still cannot be imported:** confirm that `uv add` ran in the correct project, then restart the notebook kernel.
