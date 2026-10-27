---
title: Codex Overview
parent: Overview
layout: default
nav_order: 3
permalink: /overview/codex/
---

# Codex Overview


Codex is an AI coding agent from OpenAI. It is included in USC's enterprise ChatGPT.

---

## Agent vs. chat

An agent is able to use tools to do things like read and write files, connect to the internet, and execute code. This lets the agent take much longer turns as it uses the results of the tool calls. This lets us give prompts that can be both more specific and more long-running. For example, rather than "write me code that downloads SPY prices," you can say, "This notebook throws a KeyError in the last cell. Fix it."

---

## A few ways to run agents

**A web app.** Easiest to get started, but we need connectors to be able to access our files. Likely for security reasons, USC's enterprise ChatGPT disables the Google Drive connector.

**A desktop app.** The desktop app can be very convenient, but is not the best for editing files.

**A terminal interface.** This is a very powerful interface, but has a slight learning curve to use the terminal.

**An editor extension.** This is what we will use. The agent sits in VS Code's sidebar and works in the folder of our project. We can see the changes it makes to our code (diffs). Using an editor extension makes it easy for us to make changes directly to any code or reports we are writing.

---

## Next

[Mac Setup]({{ site.baseurl }}/install/mac/) or [PC Setup]({{ site.baseurl }}/install/windows/).
