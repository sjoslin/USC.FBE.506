---
title: Codex Overview
parent: Installing Local Python and Local AI
layout: default
nav_order: 3
permalink: /install/codex/
---

# Codex Overview

> **Optional.** The setup pages tell you what to install. This explains what you're getting, and what the settings in step 4 actually do.

Codex is an AI coding agent from OpenAI. USC's ChatGPT plan includes it, so you already have access.

---

## An agent isn't a chat window

The difference is what it can touch. A chat window produces text that you copy somewhere. An agent reads the files in your project, writes changes into them, runs the code, reads the error, and tries again.

That changes the kind of request that's reasonable. Rather than "write me code that downloads SPY prices", you can say "this notebook throws a KeyError on the last cell, fix it", and it goes and looks.

The copy-paste loop is also where students lose track of which version of the code produced which number. Letting the agent edit files directly removes that entire failure mode.

---

## Three ways to run one

You'll see all of these mentioned online. We use the third.

**A desktop or web app.** Easiest to start, weakest access. It can't see your files unless you paste them in, so you're back to copy-paste.

**A terminal command.** The most capable, and you see every command before it runs. Also the least friendly if you don't already live in a terminal.

**An editor extension**, which is what we install. The agent sits in VS Code's sidebar, sees the folder you have open, and shows every change as a diff you accept or reject. You get the file access of the terminal with the reviewability of an editor, in the window you're already working in.

---

## What we let it do

Step 4 writes a small settings file. Those three lines are the most considered part of the whole setup.

**`sandbox_mode = "workspace-write"`** — Codex can read widely, but can only *write* inside the folder you have open in VS Code. Not a promise the agent makes: your operating system enforces it. This is why it matters which folder you open.

**`approval_policy = "never"`** — it doesn't stop to ask before each step.

That second one surprises people, so here's the reasoning. The alternative is a permission prompt on every action. Asked forty times an hour, anyone learns to click Allow without reading, and that's a worse habit to carry to a machine where it matters. A boundary you can state in one sentence beats a stream of prompts nobody reads.

**`network_access = true`** — it can reach the internet. This is off by default, and without it every data download in this course fails.

---

## What it still can't protect you from

The fence stops Codex writing outside your project. It doesn't stop it writing *inside* your project, which is the whole point, and also the risk.

An agent can rewrite a working notebook, and the old version is gone. So take snapshots. You don't need to learn git to do this; just ask:

> initialise a git repo here

and before a long session,

> commit my work with the message "before the bootstrap rewrite"

Thirty seconds, and the version you had is recoverable by name.

---

## Credits

USC's plan gives you 6,500 credits a month, which is far more than this course will use. A personal account gives you a free-tier trickle that runs out around week three, so when you sign in, **choose the USC workspace**. If you pick wrong, sign out from the Codex panel and do it again.

---

## Next

[Mac Setup]({{ site.baseurl }}/install/mac/) or [PC Setup]({{ site.baseurl }}/install/windows/).

If you want the agent fenced in harder than `workspace-write` manages, [Better Sandboxing]({{ site.baseurl }}/optional/sandboxing/) runs it inside a container.
