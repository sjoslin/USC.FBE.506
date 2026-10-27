---
title: Mac Setup (Overview)
layout: default
published: false
---

# Mac Setup: Overview

What you're about to install, and what's particular to a Mac. Two minutes, then the [commands]({{ site.baseurl }}/install/mac/steps/).

---

## Before you start

**Time.** About twenty minutes, nearly all of it waiting for downloads. It isn't twenty minutes of typing.

**Your password.** You'll be asked for it once or twice. These are normal installs, not anything unusual.

**Disk space.** Around 5 GB, mostly Xcode's Command Line Tools and VS Code.

**A network you trust.** Campus wifi is fine. A hotel captive portal is not, and you'll get confusing half-failures.

---

## Terminal

Everything happens in **Terminal**, an app already on your Mac. Press `⌘-Space`, type "Terminal", press return.

If you've never used one: it's a window where you type a command and press return, and the program prints its answer. Nothing is hidden and nothing happens that you didn't type. You can copy each command from this site and paste it in.

One habit worth forming now: read what comes back. Most problems in this course announce themselves clearly and get ignored because people are pasting the next line.

---

## What gets installed, in order

Each step depends on the one before it, so do them top to bottom.

| | |
|---|---|
| **Homebrew** | installs other software from the command line |
| **uv** | Python itself, plus this course's packages |
| **VS Code** | the editor |
| **Extensions** | Python, notebooks, data viewing |
| **Codex** | the AI agent, and its permissions |

---

## Two things specific to a Mac

**There's no built-in way to install developer software.** Windows has `winget`; macOS has nothing equivalent. Homebrew fills that gap, which is why it's step 0 rather than something we skip. Everything after it is one short command.

**Your Mac already has a Python.** Apple ships one for its own internal use, and the Homebrew installer pulls in more of Apple's developer tools along the way. It's several years old and has none of the libraries this course needs. We don't remove it, because macOS uses it. We just make sure your work never touches it.

That second point is the source of nearly every confusing Python error you'll hit, and it's worth knowing before you meet it rather than after. ([the full story]({{ site.baseurl }}/optional/environments/#which-python-am-i-running))

---

## When you're done

A folder at `~/fbe506` holding your work, its own copy of Python, and every package the course uses. VS Code opens it, runs your notebooks, and has Codex in the sidebar able to read and write files in that folder and nowhere else.

The four tools install where any application would: Homebrew and uv under `/opt/homebrew`, VS Code in `/Applications`. uv also keeps a shared download cache in your home folder so that a second project doesn't re-download everything.

The part that matters: no package is installed into your Mac's own Python, and no two projects share a set of packages that can conflict. Deleting `~/fbe506` undoes this project completely.

---

## Next

[Mac Setup (Steps)]({{ site.baseurl }}/install/mac/steps/)
