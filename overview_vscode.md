---
title: VS Code Overview
parent: Overview
layout: default
nav_order: 2
permalink: /overview/vscode/
---

# VS Code Overview

Visual Studio Code, usually called **VS Code**, is a free text editor from Microsoft for Windows, Mac, and Linux. It lets us work with code, notebooks, Markdown, and other text files in one application.

## A short history

Microsoft [released the first preview in 2015](https://code.visualstudio.com/blogs/2016/04/14/vscode-1.0/).

Microsoft develops VS Code in the [**Visual Studio Code - Open Source** repository](https://github.com/microsoft/vscode) on GitHub. Other developers can fork this repository and adapt the code to create their own editors and distributions. Examples include [Cursor](https://www.cursor.com/security), [Google Antigravity](https://antigravity.google/product/antigravity-ide), and [VSCodium](https://vscodium.com/) (a version of VS Code without Microsoft telemetry).

## Adding capabilities with extensions

Extensions add tools to VS Code without requiring a different editor. They can provide support for programming languages, run notebooks, help inspect data, connect an AI assistant, or change the appearance of the application. You find and install them through the [Extensions Marketplace](https://code.visualstudio.com/docs/configure/extensions/extension-marketplace).

For this course, we use:

| Extension | What it adds |
|---|---|
| **Python** | Python language support, interpreter selection, and debugging |
| **Jupyter** | Editing and running `.ipynb` notebooks inside VS Code |
| **Data Wrangler** | Exploring tables and generating pandas code for data cleaning |
| **Codex** | An AI coding assistant alongside your files |
| **Catppuccin** (optional) | Color themes and file icons |

Installing an extension adds capabilities to the editor. Python itself and the packages your code imports are installed separately, using uv. The [Local Python Overview]({{ site.baseurl }}/overview/python/) explains that part of the setup.

## Why we use it

VS Code brings our project files, notebooks, terminal, and coding assistant into one workspace. We can inspect and edit the same files that the agent works on, run the analysis, and save the results in our project folder.

Once the software is installed, continue with [Using VS Code for Python]({{ site.baseurl }}/install/vscode/python/) for a tour of the window and your first notebook.
