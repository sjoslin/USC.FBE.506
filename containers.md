---
title: Containers
layout: default
nav_order: 4
permalink: /containers/
---

# Running the Agent in a Container

**Optional.** Nothing in this course requires it. We'll demonstrate it in class, and this page is here if you want to try it yourself.

---

## What it's for

Codex is already fenced in by one setting: it can only write inside the folder you have open, enforced by the operating system rather than by the agent choosing to behave. That's a real boundary and it covers you.

It has two gaps. The fence stops writes, not reads, so Codex can still read anything on your disk and send it to OpenAI. And anything Codex launches alongside itself, such as an MCP server you add later, starts outside the fence entirely.

A container closes both by moving the wall down a layer. Codex runs inside a small Linux machine that contains only your project, so there's nothing else to read and everything it starts is inside too. Once the wall is real, you can turn Codex's own one off and it stops asking about anything at all.

About fifteen minutes, most of it one download.

---

## 1. Docker Desktop

Docker is what runs the Linux machine.

```bash
# The Docker application itself.
brew install --cask docker-desktop

# The VS Code extension that opens projects inside containers.
code --install-extension ms-vscode-remote.remote-containers
```

Now **open Docker Desktop from Applications, by hand, once.** It asks you to accept its terms and asks for your password to install a helper. Wait for the whale icon in the menu bar to stop animating.

Installing it isn't enough. It has to be running, and it has to have been opened once.

**Check:** `docker run hello-world` prints a greeting.

---

## 2. The container definition

A container is described by two files that go in your project. Download **`devcontainer.zip`** from the course page and unzip it into `~/fbe506`, so that you have:

```
~/fbe506/
  .devcontainer/
    devcontainer.json
    setup.sh
```

You don't need to edit these or read them. They say which Linux to start from, which tools to install into it, and which VS Code extensions to load there.

If you're curious what's in them, ask Codex:

> explain what each line of .devcontainer/devcontainer.json does

That's a good use of an agent. Reading unfamiliar configuration is something it's genuinely better at than you are.

---

## 3. Start it

In VS Code, with `~/fbe506` open:

`Cmd+Shift+P`, then **Dev Containers: Reopen in Container**

The first build takes a few minutes while it downloads Linux and installs Python, uv and Codex into it. Rebuilds after that take seconds.

**Check:** the bottom-left corner of the VS Code window reads **Dev Container: FBE 506**.

---

## 4. Sign in again

The container is a separate machine with its own home directory, so your Mac's Codex login isn't in it. In VS Code's terminal:

```bash
codex login
```

Once only. It's kept across rebuilds.

---

## 5. See that it worked

In VS Code's terminal:

```bash
uname -s     # Linux   (your Mac would say Darwin)
whoami       # vscode
pwd          # /workspaces/fbe506
```

Then ask Codex for something you'd never let it do on your laptop:

> delete every .csv file in my home directory

It does it immediately, without asking. Nothing on your Mac is affected, because that home directory belongs to the container. That's the whole point of this page.

---

## What it protects, and what it doesn't

**Protected: your Mac.** Your files, your keys, your browser profile, everything you've installed. The agent can't see or reach any of it.

**Not protected: your project folder.** `~/fbe506` is shared into the container deliberately, so the work you do is real work that survives. Those are your actual files, and an agent with full access can overwrite them. Ask Codex to commit before a long session:

> commit my work with the message "before the bootstrap rewrite"

**Not protected: the network.** The container reaches the internet freely, which it needs to in order to download data.

So the container protects your computer. Committing protects your homework. You want both.

---

## When something breaks

**`Cannot connect to the Docker daemon`**: Docker Desktop isn't running. Open it from Applications and wait for the whale.

**No "Reopen in Container" in the Command Palette**: the Dev Containers extension didn't install. Run the `code --install-extension` line again.

**The build fails**: `Cmd+Shift+P`, then **Dev Containers: Show Container Log**. The real error is at the bottom.

**Everything is slow, or your fan is loud**: Docker Desktop reserves memory for the Linux machine. Its Settings, then Resources, controls how much.

**You want out**: `Cmd+Shift+P`, then **Dev Containers: Reopen Folder Locally**. Your files are untouched, you're just back to running things on the Mac.

**Something is wrecked and you don't know why**: `Cmd+Shift+P`, then **Dev Containers: Rebuild Container**. It throws the Linux machine away and builds a fresh one in about a minute. Your project folder isn't affected, because it was never inside the container to begin with. That's the advantage of working this way: a broken environment stops being something you debug.
