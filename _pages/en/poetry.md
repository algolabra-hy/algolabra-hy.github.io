---
layout: page
permalink: /poetry-en
title: Poetry and Dependency Management
lang: en # fi or en
ref: poetry # same as the markdown filename
---
_These instructions are almost a direct copy from the course [Software Engineering](https://ohjelmistotuotanto-hy.github.io/poetry) website._

In large and complex software projects, writing all the code yourself is no longer practical. For example, it is inefficient for every software project to implement its own programming interface for database operations or create a framework for testing code. To avoid reinventing the wheel, software developers have created a vast number of open-source **libraries** that anyone can use in their projects.

The source code for libraries is often available on version control platforms like GitHub. These libraries are frequently updated, and these updates lead to new **versions** of the libraries. Versions of libraries are released to various repositories, from which they can be easily installed. [The Python Package Index](https://pypi.org/) (PyPI) is one such repository, specifically for Python libraries.

The versions of libraries used in a project are called the project's **dependencies**. In Python projects, dependencies are typically installed in **virtual environments** specific to the project, so there are no conflicts between the dependencies of different projects on the same computer. To make managing dependencies in virtual environments easier, we use the [Poetry](https://python-poetry.org/) command-line tool in this course.

### **Notes on Commands**

On many computers, Python version 3 commands are executed using the `python3` command instead of `python`. Check the version in use by running:

```bash
python3 --version
```

If the `python3` command is not found for some reason, check the version used by the `python` command with:

```bash
python --version
```

If the version is below 3.10 in both cases, install the **latest Python version** from [here](https://www.python.org/downloads/). After installation, make sure the correct version is in use. Otherwise, use the command that references a version of Python **at least 3.10**.

### **Installation**

Before we dive into using Poetry, first it must be installed. Follow the installation instructions below that are appropriate for your computer's operating system. It is also a good idea to check out Poetry's [official](https://python-poetry.org/docs/) installation guide.

**NOTE:** All installation methods may require closing and reopening the terminal window for Poetry commands to start functioning. In some cases, even restarting the computer may be necessary.



{% include typo_instructions_en.md %}
