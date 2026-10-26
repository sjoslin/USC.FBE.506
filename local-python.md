---
title: Local Python Overview
parent: Installing Local Python and Local AI
layout: default
nav_order: 1
permalink: /install/python/
---

# Local Python Overview

> **Optional.** The setup pages tell you what to type. This explains what you're getting.

Three things get installed, and it's worth knowing which is which, because when something breaks the error message won't tell you.

---

## The interpreter

Python itself: the program that reads your code and runs it. One file, a few tens of megabytes, and on its own it can do arithmetic, loops and text, and almost nothing you'd call data analysis.

We use **Python 3.12**, deliberately a version or two behind the newest. New Python releases come out each October, and library authors need months to publish builds for them. Being first in line mostly buys you packages that refuse to install.

## The packages

pandas, numpy, statsmodels, matplotlib and the rest: code other people wrote that you import. This is where the actual work of the course happens, and it's also where the version trouble lives, because each package has its own release schedule and its own opinions about which versions of the others it will tolerate.

## The environment

A folder, `.venv`, inside your project. It holds a copy of the interpreter and all the packages for *this* project and nothing else.

That's the piece with no Colab equivalent, so it's the one worth understanding. In Colab the whole machine is the project, so installing into it is safe. On your laptop the machine outlives the project, and a single shared pile of packages works right up until two projects want different versions.

Keeping them separate means installing something here can't break anything else, and deleting `.venv` undoes this project completely without touching the rest of your machine.

---

## uv does all three

Rather than three tools, one. `uv` downloads the interpreter, creates the environment, installs the packages, and records exactly which versions it chose.

You'll type it twice in the whole setup and then mostly forget it exists:

```bash
uv init --python 3.12     # start a project
uv add pandas             # add a package
```

Everything else happens inside VS Code, where the environment is already active and you just write `import pandas`.

---

## Which one is it running?

The question behind nearly every Python problem, including the notebook that insists pandas isn't installed when you can see that it is.

Your Mac already has a Python that Apple put there for its own purposes. It's old and has none of your packages. Windows may have one from the Microsoft Store. So there are always at least two on the machine, and only one of them is yours.

Inside VS Code, the kernel picker in the top right of a notebook should read **`.venv`**. If it reads anything else, click it and choose the one with `.venv` in the path. That's the fix, nearly every time.

The long version, including what "activating an environment" actually does, is in [Python Environments]({{ site.baseurl }}/optional/environments/). You don't need it until something goes wrong.

---

## Next

[Mac Setup]({{ site.baseurl }}/install/mac/) or [PC Setup]({{ site.baseurl }}/install/windows/).
