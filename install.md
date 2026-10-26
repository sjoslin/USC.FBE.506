---
title: Installing Local Python and Local AI
layout: default
nav_order: 1
has_children: true
permalink: /install/
---

# Installing Local Python and Local AI

## What we're doing

In this section we discuss and install three pieces of software.

1. **Local Python.** So far we've been running Python in the cloud, with Google Colab. Now we install a version that runs on our own computer. That means the Python interpreter itself, and also the common libraries we use, like pandas and statsmodels.

2. **VS Code.** An editor, which can be extended with many capabilities. It helps us write and run Python code, and it also offers tight integration with coding agents such as Codex.

3. **Codex.** A coding agent. Unlike a chat window, an agent running on our own machine can read our files directly, write code into them, and run it.

---

## Why isn't this just a download?

The instructions are a bit complicated. Why? When we want to run other apps we just download it and it works.  
We don't need a bunch of instructions to install Zoom, so why do we need so many to install Python?

The key issue is that almost nothing in Python is standalone. We want Python plus a lot of libraries like pandas, numpy, etc.
So the installation procedure must track not only Python but also the libraries. Another complication is all of these have different versions.  
With multiple versions of Python and multiple versions of libraries, we might want a way to choose which combination we want. For example, I might prefer Windows 7 to Windows 8 (and some of my apps might only work with Windows 7).

One more thing makes this fiddly rather than hard. Your computer already has a Python you didn't install, several years old, with none of the libraries you need. So from the moment you start there are at least two on the machine, and running code with the wrong one is the most common problem in this course.

None of it is difficult. It's just genuinely confusing until someone draws you the map.

---

## Python 2 and Python 3

Python 3.0 arrived in December 2008 and deliberately broke things. The language had accumulated awkward corners, and rather than keep them forever, the maintainers fixed them all at once knowing old code would stop working.

The changes you'd notice: `print "hello"` became `print("hello")`, text became Unicode by default so non-English characters stopped being a nightmare, and `1/2` started giving `0.5` instead of `0`. Small on their own, fatal in combination. Essentially every program had to be edited.

The transition took twelve years. Python 2 wasn't retired until January 2020, and for most of that time the internet was full of answers written for a version that no longer ran. That's why you'll occasionally find a Stack Overflow post whose code fails on the first line.

That split is over. Everything is Python 3 now, and nothing like it is planned.

---

## The 3.x releases

Since then a new version has come out every October: 3.11, 3.12, 3.13, and so on. These are nothing like the 2-to-3 break. Most are faster under the hood, add some convenience, and run your existing code unchanged.

"Most" is doing real work in that sentence. Features do get removed after long deprecation, and behaviour occasionally shifts in ways that change an answer rather than raising an error, which is the worse kind. So the version isn't something to be careless about.

**We use 3.12**, deliberately a version or two behind the newest. Library authors need time to publish builds for each new Python, and being first in line mostly buys you packages that won't install.

---

## The packages have versions too

This is where most real trouble lives.

pandas alone has had many releases, and across them the default behaviour of common operations has changed. Run the same notebook against two different pandas versions and you can get two different numbers, with no error to tell you something moved. Not often. Often enough that when your answer disagrees with the solution, "are we even running the same pandas" is a real question rather than a dodge.

So "which Python am I running" is really two questions: which interpreter, and which set of library versions alongside it. The setup on the next page answers both, and pins them, so that everyone in the class is running the same thing and a number that reproduces for one person reproduces for everyone.

---

## The pages in this section

|                                                             |                                                    |
| ----------------------------------------------------------- | -------------------------------------------------- |
| [Local Python Overview]({{ site.baseurl }}/install/python/) | how Python, packages and environments fit together |
| [VS Code Overview]({{ site.baseurl }}/install/vscode/)      | the editor, and what the extensions add            |
| [Codex Overview]({{ site.baseurl }}/install/codex/)         | what an agent is, and what we let it do            |
| [Mac Setup (Overview)]({{ site.baseurl }}/install/mac/)     | what's particular to a Mac                         |
| [Mac Setup (Steps)]({{ site.baseurl }}/install/mac/steps/)  | the commands, for macOS                            |
| [PC Setup]({{ site.baseurl }}/install/windows/)             | the commands, for Windows                          |

In a hurry? Go straight to [Mac Setup (Steps)]({{ site.baseurl }}/install/mac/steps/) or [PC Setup]({{ site.baseurl }}/install/windows/). The overviews keep.
