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

#### **Linux and macOS Installation**

To install Poetry, run the following command in the terminal:

```bash
curl -sSL https://install.python-poetry.org | POETRY_HOME=$HOME/.local python3 -
```

**NOTE:** If the `python3` command is not found, use the `python` command at the end instead. However, make sure the Python version is correct.

**NOTE:** If you encounter the error `SSL: CERTIFICATE_VERIFY_FAILED` on macOS, open the Python installation directory with the command:

```bash
open /Applications/Python\ 3.9
```

(Replace "3.9" with the Python version you are using) and click on the _Install Certificates.command_ file. Wait for the operation to finish, and then run the installation command again.

After installation, the path to the Poetry binary must be added to the `PATH` variable. You can do this by adding the following line to the end of your home directory's _.bashrc_ file:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

You can add it using a text editor like nano, or by running the following command:

```bash
echo "export PATH=\"\$HOME/.local/bin:\$PATH\"" >> $HOME/.bashrc
```
**NOTE:** If you use the zsh shell, the correct configuration file is _.zshrc_ instead of _.bashrc_. You can check the shell you are using with the command `echo $SHELL`. In this case, replace the `$HOME/.bashrc` path in the previous command with `$HOME/.zshrc`.

**NOTE:** If you use macOS and the bash shell, use `$HOME/.bash_profile` instead of `$HOME/.bashrc` in the previous command.

**NOTE:** On the melkki server, use `$HOME/.profile` instead of `$HOME/.bashrc` in the previous command.

Restart the terminal and verify that the installation was successful by running the command `poetry --version`. The command should output the installed version.

{% include typo_instructions_en.md %}
