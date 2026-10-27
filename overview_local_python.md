---
title: Local Python Overview
parent: Overview
layout: default
nav_order: 1
permalink: /overview/python/
---

# Local Python Overview

This page describes the three main components of a local Python installation. Understanding these pieces can be helpful if there are problems in your configuration.

---

## The interpreter

Python itself: the program that reads the code and executes it. The base version of Python has a lot of capabilities like arithmetic, loops, and creating text, but it doesn't have many capabilities for data analysis.

We will set up and use **Python 3.12**. There are new versions of Python each year, but a slightly vintage one will be more compatible with packages we may want to install.

## The packages

For doing data analysis and other tasks, we will want to use a number of packages like pandas, NumPy, statsmodels, and matplotlib. This is code written outside of the base Python code. These also have versions that get periodic updates for corrections and improvements.

## The environment

A Python environment is the collection of which Python version and which packages (and their versions) you are using for your project. It is often stored in a folder, like `.venv`, inside the project.

In Colab, we didn't have to worry about this. Essentially Google did all the work for us: the VM Colab provided was only running one project and the environment was already set up.

---

## Managing the environment with pip

In some ways the simplest (and in other ways the worst) way of managing packages is `pip`, which stands for "pip installs packages." If you download Python 3.12 from python.org, it comes with pip, and you can run `python3 -m pip install pandas numpy`. Now your computer has a single Python 3.12 environment with pandas and numpy in it.

So why not just do this? If you, and every program or piece of code you ever download, are happy sharing that one environment, it works. The problem creeps in when two things want different versions. Installing a package for one project can upgrade or downgrade it for everything else using that Python, and something that used to work breaks. Python can make separate environments (with `venv`), but you have to create them, activate them, and remember which is which yourself, and pip may install into the wrong one if you forget.

For something more robust (and still pretty simple) we will use `uv`.

## Managing the environment (and installing) with uv

`uv` downloads the interpreter, creates the environment, and installs packages.

To create an environment we can use in our fbe506 folder (and any subfolder), we can use:

```bash
cd ~/fbe506                            # in VS Code, the terminal starts in the project already
uv init --python 3.12 --no-package     # initialize a project (once, at the top)
uv add pandas                         # create the environment and add pandas
uv add ipykernel                      # let notebooks use .venv
```

The first time we add a package, `uv` downloads it to a shared cache and installs it into the project's `.venv`. When the file system supports it, uv uses copy-on-write clones or hardlinks to reduce duplicate disk use. When we run `uv add` the first time, it creates the virtual environment (i.e., it creates a `.venv` folder). Also, if we don't `uv add` a package first, we'll get an error when we try to import it. `uv` also installs whatever our packages depend on (e.g., pandas requires NumPy), but if our own code imports something, we should `uv add` it ourselves.

After setup, work inside VS Code and use the project's `.venv` for notebook and terminal commands.

---


## Next

[Mac Setup]({{ site.baseurl }}/install/mac/) or [PC Setup]({{ site.baseurl }}/install/windows/).
