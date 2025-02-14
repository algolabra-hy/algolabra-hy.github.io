---
layout: page
permalink: /git-en
title: Git 
title_long: Using Git 
lang: en # fi or en
ref: git # same as the markdown filename
---
_Original instructions by Mika Huttunen and Silja Polvi. Jeremias Berg has updated the instructions._

# Getting Started
DO NOT use the Git plugin provided by NetBeans or any graphical programs. So far, all problems in this course where students have lost a day's coding work have been caused by these. Always use the terminal in Linux/OSX or Git Bash in Windows, and perform commits and pushes manually.

First, check if Git has been installed on your computer by running the command "git -v" in the terminal. The output should look something like this:
```  
jezberg@LM2-500-27156 ~ % git -v 
git version 2.39.3 (Apple Git-145)
```
If you receive an error message (e.g., "command not found"), first install Git by following the instructions on [this page](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

After installing Git, create a [GitHub](https://github.com/) account (personal, not enterprise).
Once your account is created, you can create a new repository by clicking the "+" symbol in the top right corner and selecting "Create repository."

![]({{ "/images/git-0.png" | absolute_url }})

Name the repository according to the topic of your project. **Select "Public"**.
If you want to complete all the repository management exercises on this page, check the box "Add a README file".
You can also choose a ".gitignore" file suitable for your programming language (more about .gitignore below).

![]({{ "/images/git-1.png" | absolute_url }})

## Generating an SSH Key on Your Computer
Follow the instructions [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

## Preparing the Repository for Use
**NOTE:** In this guide, "command line" refers to the terminal on Linux and Mac, and Git Bash on Windows! Windows' own command prompts do not recognize Git commands.

Navigate to the repository you created on GitHub. You can access it from the homepage after logging in by clicking on the repository name.

![]({{ "/images/git-2.png" | absolute_url }})

Click the "Code" button, and select "SSH" in the pop-up window.

![]({{ "/images/git-3.png" | absolute_url }})

Copy the repository URL that appears, which should be in the format:
git@github.com:your-username/project-name.git
You can copy the address by clicking the symbol next to it.

Open the command line and clone the repository to your computer using the command: git clone "repository-url".
```
jezberg@LM2-500-27156 Documents % git clone git@github.com:jezberg/harjoitustyo.git
Cloning into 'harjoitustyo'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
jezberg@LM2-500-27156 Documents % 
```





{% include typo_instructions_en.md %}
