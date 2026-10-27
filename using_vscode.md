---
title: Using VS Code for Python
layout: default
nav_order: 3
permalink: /install/vscode/python/
---

# Using VS Code for Python

After [Mac Setup]({{ site.baseurl }}/install/mac/) or [PC Setup]({{ site.baseurl }}/install/windows/), continue here. These are the steps you will use as you work, on either platform.

## Open your project

Choose **File → Open Folder** and open your course folder (`fbe506` if you used the setup instructions). Open the folder rather than just a notebook so you can see all of the project's files.

## The parts of the window

<div class="vscode-window-figure">
  <img src="{{ site.baseurl }}/assets/images/vscode-window-annotated.png" alt="Annotated VS Code window: 1 Activity bar, 2 Explorer, 3 editor, 4 terminal, 5 Codex panel, 6 status bar, and 7 notebook kernel picker.">
  <span class="vscode-kernel-outline" aria-hidden="true"></span>
  <span class="vscode-kernel-label" aria-hidden="true">7</span>
</div>

- <span class="ui-key ui-key--activity">1</span> **Activity bar:** the strip of icons at the far left. Use to switch between files, search, source control, and add extensions.
- <span class="ui-key ui-key--explorer">2</span> **Explorer:** the file list on the left (if open).
- <span class="ui-key ui-key--editor">3</span> **Editor:** the main area in the center. Files open in tabs. You can run cells in a Python notebook.
- <span class="ui-key ui-key--terminal">4</span> **Terminal:** the panel below the editor (if open). Open it with **Terminal → New Terminal**.
- <span class="ui-key ui-key--codex">5</span> **Codex panel:** the coding assistant shown on the right.
- <span class="ui-key ui-key--status">6</span> **Status bar:** the strip along the bottom with information about the current state.
- <span class="ui-key ui-key--kernel">7</span> **Notebook kernel picker:** the control at the top right of a notebook. It says **Select Kernel** until you choose one, then shows the selected Python environment.

## Creating a notebook

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

Press `Shift-Enter` to run the cell. The new notebook may initially be named `Untitled-1.ipynb`. The first time you save it with `⌘-S` on Mac or `Ctrl-S` on Windows, VS Code asks you for a filename. Choose your project folder, enter `hello.ipynb`, and click **Save**.

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

The printed path should point inside your project's `.venv`.

## Add packages

Open **Terminal → New Terminal**, check that you are in the project folder, and run `uv add` with the package name. For example:

```bash
uv add seaborn
```

Restart the notebook kernel using **Restart** in the notebook toolbar, then run your cells again. Restarting clears variables from the previous session.

## Use the coding assistant

Open the **Codex** panel and try a small task:

> Create a Python notebook that prints "hello world!" and explain how I can run it.

Open the resulting file, check the selected kernel, and run the cells yourself. The [Codex Overview]({{ site.baseurl }}/overview/codex/) explains the assistant in more detail.

## Useful shortcuts

| Action | Mac | Windows |
|---|---|---|
| Command Palette | `⌘-Shift-P` | `Ctrl-Shift-P` |
| Open a file by name | `⌘-P` | `Ctrl-P` |
| Show or hide the Explorer sidebar | `⌘-B` | `Ctrl-B` |
| Show or hide the terminal | `` Ctrl-` `` | `` Ctrl-` `` |
| Run a notebook cell | `Shift-Enter` | `Shift-Enter` |

## When something breaks

**A notebook says pandas isn't installed:** check the kernel at the top right. Choose your project's `.venv`, then rerun the cell. Installing pandas in a different Python will not make it available to this notebook.

**A command uses the wrong Python:** run it with `uv run` from the project folder. The notebook kernel and terminal environment are separate.

**A newly installed package still cannot be imported:** confirm that `uv add` ran in the correct project, then restart the notebook kernel.
