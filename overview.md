---
title: Overview
layout: default
nav_order: 1
has_children: true
permalink: /overview/
---

# Overview

## What we're doing

In this section we discuss and install three pieces of software.

1. **Local Python.** So far we've been running Python in the cloud, with Google Colab. Now we install a version that runs on our own computer. That means the Python interpreter itself, and also the common libraries we use, like pandas and statsmodels.

2. **VS Code.** An editor, which can be extended with many capabilities. It helps us write and run Python code, and it also offers tight integration with coding agents such as Codex.

3. **Codex.** A local coding agent. Unlike a chat window, a local agent running on our own machine can read our files directly, write code into them, and run it.

---

## Why isn't this just a download?

The instructions are a bit complicated. Why? When we want to run other apps we just download it and it works. We don't need a bunch of instructions to install Zoom, so why do we need so many to install Python?

The key issue is that almost nothing in Python is standalone. We want Python plus a lot of libraries like pandas, numpy, etc.
So the installation procedure must track not only Python but also the libraries. Another complication is all of these have different versions. With multiple versions of Python and multiple versions of libraries, we might want a way to choose which combination we want. For example, I might prefer Windows 7 to Windows 8 (and some of my apps might only work with Windows 7).

So we might want a method to install Python 3.12 with pandas 3.1.0 and numpy 2.5.4.

The steps are not hard, but it helps to see how things are laid out.


## Pages in this section

Start with the overviews, then follow the setup instructions for your computer and continue to the shared VS Code workflow.

| Page | What it covers |
|---|---|
| [Local Python Overview]({{ site.baseurl }}/overview/python/) | Python, packages, environments, and uv |
| [VS Code Overview]({{ site.baseurl }}/overview/vscode/) | the editor and its extensions |
| [Codex Overview]({{ site.baseurl }}/overview/codex/) | coding agents and their permissions |
| [Mac Setup]({{ site.baseurl }}/install/mac/) | installation on macOS |
| [PC Setup]({{ site.baseurl }}/install/windows/) | installation on Windows |
| [Using VS Code for Python]({{ site.baseurl }}/install/vscode/python/) | the shared workflow after installation |

<!-- Move shared preparation and installation overview from overview_mac_draft.md here. -->
