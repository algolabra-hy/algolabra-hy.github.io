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

#### Windows Installation

Install Poetry by running the following command in the terminal:

```powershell
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
```

After installation, the Poetry binary path must be added to the `PATH` variable. Follow [this guide](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/) to add the path `%APPDATA%\Python\Scripts` to the `PATH` variable.

Restart the terminal and verify that the installation was successful by running the command `poetry --version`. The command should output the installed version.

### Initializing a Project

Let's practice using Poetry by creating a small example project. Create a directory named _poetry-test_ in a location of your choice. The directory does not need to be in a repository registered with Labtool. Open the directory in a terminal and run the following command:

```bash
poetry init --python "^3.10"
```

The `--python "^3.10"` option specifies that the project requires at least Python version 3.10. Running the command will start an interactive setup process, asking you various questions. You can answer them as you prefer, and all responses can be modified later. Therefore, skipping questions by pressing the Enter key is a good option.

Once you have answered the last question, check the contents of the directory. A _pyproject.toml_ file should appear, containing something like the following:
```
[tool.poetry]
name = "poetry-test"
version = "0.1.0"
description = ""
authors = ["Matti Luukkainen <matti.luukkainen@helsinki.fi>"]
readme = "README.md"

[tool.poetry.dependencies]
python = "^3.10"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```
The `[tool.poetry]` section of the file contains general information about the project, such as its name, description, and maintainers. Below this section, there are sections listing the project's dependencies. In the `[tool.poetry.dependencies]` section, we can see the Python version requirement we specified during the `poetry init` command, which is written as `python = "^3.10"`. The `^3.10` notation means the project requires at least Python version 3.10.

Once you are familiar with the _pyproject.toml_ file, finalize the project initialization by running the following command:

```bash
poetry install
```

Running this command performs the necessary setup for the project, such as initializing a virtual environment and installing dependencies. Therefore, this command should always be executed before starting to use a new project.

Executing the command will likely result in the following message:
```
Installing the current project: poetry-test (0.1.0)
The current project could not be installed: [Errno 2] No such file or directory: '~/poetry-test/README.md'
If you do not want to install the current project use --no-root
```
This happens because Poetry attempts to install the current project as well, but there is no module named _poetry-test_ in the project. Despite how the message might look, this is [not an error](https://github.com/python-poetry/poetry/pull/8369) but rather a warning. The project initialization has been completed successfully. However, if you want to avoid the warning, you can use the following command instead:

```bash
poetry install --no-root
```

In addition to setting up the virtual environment, this command installs only the project's dependencies, not the project itself.

After running the command, a file named _poetry.lock_ should appear in the directory. This file contains version information for all installed dependencies. Thanks to this file, Poetry can always install the exact dependency versions specified when running the `poetry install` command. For this reason, the file should be added to version control.

### Installing Dependencies

{% include no_pip.md %}

Next, let's install the first dependency for our project. The easiest way to find dependencies is by searching on Google and looking for relevant GitHub repositories or PyPI pages. As an example, let's install the [cowsay](https://pypi.org/project/cowsay/) library. This can be done from the project's root directory (the same directory where the _pyproject.toml_ file is located) with the following command:

```bash
poetry add cowsay
```

The installation command follows the format `poetry add <library>`. After executing the command, you will notice that new content has been added under the `[tool.poetry.dependencies]` section of the _pyproject.toml_ file:

```
[tool.poetry.dependencies]
python = "^3.10"
cowsay = "^2.0.3"
```
The `poetry add` command installs the latest version of a library by default, which, at the time of execution, was `2.0.3`. This is often exactly what we want to do. However, if we wanted to install a specific version of the cowsay library, such as version `1.0`, we could do so with the following command:

```bash
poetry add cowsay==1.0
```

If we wanted to remove the library from our project's dependencies, we could do so with the command:

```bash
poetry remove cowsay
```

However, let's keep the cowsay library installed for now.

### Running Commands in the Virtual Environment

Next, let's add a folder named _src_ to the _poetry-test_ directory and create a file named _index.py_ inside it. Add the following code to the file:

```python
import cowsay

cowsay.tux("Poetry is awesome!")
```

In the code, we use the `import` statement to access the cowsay library. If we try to run the file in the terminal with the command:

```bash
python3 src/index.py
```

We will get the following error message:

```
ModuleNotFoundError: No module named 'cowsay'
```

This happens because we are not inside the project's virtual environment, and Python cannot find our project's dependencies. This can be fixed by using the [run](https://python-poetry.org/docs/cli/#run) command:

```bash
poetry run python3 src/index.py
```
The `poetry run` command executes the given command within the virtual environment, where Python can find our dependencies.

When actively developing a project and running commands in the terminal continuously, it is most convenient to stay inside the virtual environment. We can enter the virtual environment with the following command [shell](https://python-poetry.org/docs/cli/#shell):

```bash
poetry shell
```

Once inside the virtual environment, the prompt will display the virtual environment's name in parentheses:

```bash
$ (poetry-test-IhtScY6W-py3.9)
```

While inside the virtual environment, we can run commands "normally," without needing to use the `run` command:

```bash
python3 src/index.py
```

To exit the virtual environment, we can use the `exit` command.

Poetry's imported dependencies are only available within the virtual environment, and VS Code's built-in "debugging mode" (F5 by default) may not work as expected. Try first using `poetry shell` and only then launch VS Code with the `code /path/to/project` command.

### Development Dependencies

With Poetry, you can group dependencies based on their intended use. A common way to group dependencies is to separate them into _development_ and _runtime_ dependencies. Development dependencies are required during software development but are not necessary for running the application.

Running the `poetry add` command by default installs dependencies under the `[tool.poetry.dependencies]` section. In addition to these runtime dependencies, we can install dependencies that are needed only during development. These are dependencies that are not required for running the application itself (for example, running the `python3 src/index.py` command).

To install development dependencies, you can use the `--group dev` flag with the `poetry add` command. For example, the [pytest](https://pytest.org/) library, which we will become familiar with soon, can be installed as a development dependency with the following command:

```bash
poetry add pytest --group dev
```

Running this command adds the `pytest` library as a development dependency under the `[tool.poetry.group.dev.dependencies]` section:

```
[tool.poetry.group.dev.dependencies]
pytest = "^7.4.2"
```

Defining development dependencies is useful because it reduces the number of dependencies that need to be installed when we only want to run the application. In this case, dependencies can be installed with the command `poetry install --without dev`.

{% include no_pip.md %}

### Solutions to Common Issues

Often, Poetry issues can be resolved with the following steps:

1. Make sure you have the latest version of Poetry installed by running the command `poetry self update`.
2. Ensure the correct Python version requirement is specified in the _pyproject.toml_ file:

   ```
   [tool.poetry.dependencies]
   python = "^3.10"
   ```

   **If the version is incorrect**, change it to the correct one and run the command `poetry update`.

3. Clear the cache by running the following commands:
   ```bash
   poetry cache clear pypi --all
   poetry cache clear PyPi --all
   ```

4. List the virtual environments used in the project with the command `poetry env list`, and remove them one by one with the command `poetry env remove <name>`. For example:

   ```bash
   $ poetry env list
   unicafe-jLeQYxxf-py3.9 (Activated)
   $ poetry env remove unicafe-jLeQYxxf-py3.9
   Deleted virtualenv: /Users/kalleilv/Library/Caches/pypoetry/virtualenvs/unicafe-jLeQYxxf-py3.9
   ```
Once the virtual environments have been removed, run the command `poetry install`.

After completing all the steps, try running the failed Poetry command again.

### Keyring Issue

If the `poetry install` command prompts for a keyring password, the issue can be resolved by running the following in the terminal:
```bash
export PYTHON_KEYRING_BACKEND=keyring.backends.fail.Keyring
```
Then, run the `poetry install` command again. 

You can add this line to your _.bashrc_ (or equivalent) file so that it doesn’t need to be run at the start of every terminal session.

{% include typo_instructions_en.md %}
