---
layout: page
permalink: /pylint-en
title: Pylint and Static Code Analysis
lang: en # fi or en
ref: pylint # same as the markdown filename
---
_This guide is a copy of the Software Engineering course's [Pylint guide](https://ohjelmistotekniikka-hy.github.io/python/viikko4#pylint-ja-koodin-laaduun-staattinen-analyysi) with some additions._  

In addition to testing code, maintaining code quality is essential. Quality can be upheld through various manual methods, such as documenting quality requirements and conducting code reviews. However, many manual quality management methods often prove too time-consuming and error-prone in large software projects. _Static analysis_ is a method that allows code to be analyzed automatically without executing it. Static analysis is widely used in software development to detect programming errors and perform quality checks.

One widely used tool for static analysis of Python code is [Pylint](https://www.pylint.org/). With Pylint, we can define various quality requirements for our code and automatically check whether the inspected code adheres to these rules.  

> Pylint is a tool that checks for errors in Python code, tries to enforce a coding standard, and looks for code smells. It can also look for certain type errors, recommend suggestions on how specific blocks can be refactored, and provide details about the code's complexity.  

### Setting Up Pylint in a Project  

Pylint is easy to set up in a Poetry project. We start by installing Pylint as a development dependency for our project:  

```
poetry add pylint --group dev
```
A set of [rules](http://pylint.pycqa.org/en/v3.0.2/technical_reference/features.html) must be defined for Pylint to check. These rules are specified in the _.pylintrc_ file located in the project's root directory. Create this file and copy the contents from [this configuration file](https://github.com/ohjelmistotekniikka-hy/ohjelmistotekniikka-hy.github.io/blob/master/materiaali/python/.pylintrc). This file contains a slightly modified version of Pylint’s recommended configuration, which can be viewed with the command:  

```
pylint --generate-rcfile
```  

### Running Pylint Quality Checks  

You can run Pylint’s quality checks from the command line. First, activate the virtual environment using:  

```
poetry shell
```  

Then, run the following command in the project’s root directory (the same directory where _pyproject.toml_ is located):  

```
pylint src
```  

This command performs the quality checks on the _src_ directory. Pylint assigns a "score" to the code based on its quality, which can be found at the end of the output:
```
Your code has been rated at 10.00/10 (previous run: 10.00/10, +0.00)
```
### Disabling Quality Checks  

As a rule of thumb, it's best to fix any quality issues flagged by Pylint, as doing so almost always results in better code. However, in some cases, we may accept certain issues and disable specific checks. There are different ways to do this.  

Consider the following _src/index.py_ file:  

```python
x = 3
print(x)
```  

Running the command `pylint src` reveals that Pylint detects the following issue in the file:  

```
src/index.py:1:0: C0103: Constant name "x" doesn't conform to UPPER_CASE naming style (invalid-name)
```  

This means that on line 1 of _src/index.py_, there is a variable name that does not follow the UPPER_CASE naming convention. The rule being violated here is `invalid-name`.  

The best solution would be to rename the variable to `X`, but for demonstration purposes, let's see how we can disable this rule for a specific line. We add the following comment:  

```python
x = 3  # pylint: disable=invalid-name
print(x)
```
Now, running the `pylint src` command should confirm that no errors are found.  

We can also exclude entire directories and files from Pylint checks. For example, we might want to exclude UI-related code in the _src/ui_ directory and test files in _src/tests_:  

```
ignore=CVS,ui,tests
```  

### Integration with an Editor  

Many code editors have extensions that highlight quality issues directly in the code, making them easier to spot and fix.  

If you use [Visual Studio Code](https://code.visualstudio.com/), simply install the [Pylint extension](https://marketplace.visualstudio.com/items?itemName=ms-python.pylint):  

![Visual Studio Code Pylint extension]({{ "/images/vscode-pylint.png" | absolute_url }})  

Once installed (and after possibly restarting Visual Studio Code), the editor should underline quality issues in red. Hovering over the problematic code will display more details about the error:  

![Visual Studio Code Pylint error]({{ "/images/vscode-pylint-virhe.png" | absolute_url }})  

If you encounter issues with the integration, refer to the [Visual Studio Code documentation](https://code.visualstudio.com/docs/python/linting) for troubleshooting.
### Bonus: Automatic Formatting  

Fixing certain code quality issues, such as indentation and overly long lines, can sometimes be tedious and unnecessary manual work. The [autopep8](https://pypi.org/project/autopep8/) library helps with automatic code formatting, ensuring compliance with [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guidelines.  

To start using it, install the library as a development dependency:  

```bash
poetry add autopep8 --group dev
```  

Once installed, you can format all code in the _src_ directory from within the virtual environment using:  

```bash
autopep8 --in-place --recursive src
```  

Many editors also support formatting with a simple keyboard shortcut. Instructions for formatting code in Visual Studio Code can be found [here](https://code.visualstudio.com/docs/editor/codebasics#_formatting).

{% include typo_instructions_en.md %}
