---
title: Home
layout: home
---

# FBE 506 - Setting Up Your Own Machine

Colab has carried us this far. It stops being enough once the work gets longer than a session: you can't keep a project across weeks, you can't point an AI agent at a folder of files, and you reinstall your packages every time you open it.

So we move the work onto your own laptop. Python, a real editor, and a coding agent that can read and write your files directly.

## Start here

[**Setup Overview**]({{ site.baseurl }}/install/) explains what we're installing and why it takes more than one download. Read it first, then pick your machine:

| | |
|---|---|
| [Mac Setup]({{ site.baseurl }}/install/mac/) | Homebrew, Python, VS Code, Codex |
| [PC Setup]({{ site.baseurl }}/install/windows/) | the same, with winget and PowerShell |

Twenty minutes, mostly waiting for downloads. Do it before the first class that needs it, not during.

## Then

| | |
|---|---|
| [Python Environments]({{ site.baseurl }}/optional/environments/) | what the setup actually did, and how to debug it |
| [Better Sandboxing]({{ site.baseurl }}/optional/sandboxing/) | optional: running the agent inside a container |

## What you'll end up with

A folder that holds your work, its own copy of Python, and every package this course uses. An editor that runs notebooks, shows you your data, and hosts an AI agent in the sidebar.

That agent can read your files, write code, and run it, without asking permission each time. It also can't write anywhere outside the folder you've opened. Both of those are settings you'll make deliberately in step 4, and knowing why they're set that way is part of the point.

Colab still works. Nothing here takes it away.
