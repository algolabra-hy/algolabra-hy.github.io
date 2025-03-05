---
layout: page
permalink: /overview-en
title: Overview of the Project
title_long: Overview of the Project
lang: en # fi or en
ref: overview_full_course # same as the markdown filename
---
Here is an overview of the course structure. More detailed information on all topics covered on this page can be found in other parts of the course material.

During the course, students will develop a program that solves a given programming problem. The solution must utilize appropriate and efficient algorithms and data structures. The topic is free to choose if the solution involves sufficient algorithmic complexity. In practice, this means using literature-based algorithms to ensure the algorithms are suitable for the task and produce the desired results.
Finding and studying relevant literature—if necessary, with the help of the course staff—is a crucial and time-consuming part of the project.

### Choosing a Topic
Suggestions for suitable project topics can be found [here]({% link _pages/en/topics.md %}). In addition, students may choose own topic, provided it is approved by a supervisor.
Algorithms learned in the Data Structures and Algorithms course or earlier programming courses are considered prerequisites for this course and therefore cannot constitute the core content of the project. Additionally, the project must apply an algorithm to a practical situation, which is ensured in all topic suggestions provided in the course materials.

If you choose a completely original topic or the proposed topic lacks details, schedule a meeting with a supervisor during the first week - before submitting the specification document. This will help define the scope of the project and clarify which parts you need to implement yourself to ensure an appropriate level of complexity.

### Choosing a Programming Language
The programming language for the project is freely selectable, as long as it is suitable for the chosen topic.
For most topics, any programming language can be used. However, some topics - such as data structure comparison - are only meaningful when implemented in low-level languages like C or C++. Otherwise, the project may end up measuring differences in language-specific tools or efficiency rather than the actual differences between data structures.

Usually, you should use the language you are most proficient in. Learning a new language during the project is not recommended, as there is already enough to study about the topic.

Python is often the best choice for the project, provided you have sufficient proficiency in it. Most students complete their projects in Python, and many are not familiar with other languages. For this reason, the course instructions primarily focus on Python.
If you use Python, you will likely receive peer reviews for projects with similar or related topics. Additionally, the feedback you receive will generally come from someone familiar with both your topic and programming language.
When assigning peer reviews, students' stated programming language skills are considered. However, the general rule is that Python users review each other’s work, while those using other languages review each other regardless of the specific language used.

Note that [automated testing]({% link _pages/en/testing_frontpage.md %}) and test coverage measurement are mandatory for all projects, regardless of the programming language used. However, the [course materials]({% link _pages/en/unit_testing.md %}) provide instructions only for Python, and the course staff may not be able to offer guidance for other languages.
If you choose a language other than Python, you must take more responsibility for learning these aspects. However, as long as you are proficient with the necessary development tools in your chosen language, the course staff will support you in understanding the algorithms and debugging implementation errors.
Debugging will primarily be done together with the instructor, for example, via Zoom, rather than the instructor independently reviewing your code.

The objective of the course is to learn how to implement data structures and algorithms that are not covered in the course prerequisites. The focus is primarily on algorithm implementation, but in some smaller-scale topics, implementing custom data structures is also required.
In all projects, you may use mathematical functions for primitive types and string manipulation functions provided by the language. However, external libraries may only be used for user interfaces and testing, unless otherwise specified.

### Testing the Project
Ensuring the correctness of your program is crucial when working with complicated algorithms. You must verify that your algorithm produces the correct results and operates with the expected efficiency.
Correctness testing is done through automated unit tests, which should be written from the beginning of the project as new code is developed. General testing guidelines, including specific requirements, can be found on the [testing]({% link _pages/en/testing_requirements.md %}) page.

### User Interface
While the user interface is not the primary focus of this course, having a functional interface from the start is important. The application must produce an output (text, image, sound, or file) that makes it easy to verify whether the program works correctly.
The exact requirements depend on the project topic. In some cases, command-line parameters may be sufficient for interacting with the program. However, most projects require at least a menu-based command-line interface and ASCII graphics. In many cases, clear visualization is essential, even during development, to help verify the program's correctness.

If you are experienced with graphical UI development, creating a GUI might save time during testing, especially if the program requires frequent interaction - such as selecting points on a map or experimenting with different parameter values.
You are free to use any available tools for UI development. However, testing the UI is not required, and it does not contribute to the project’s final grade.

### Schedule and Time Management
The course [schedule]({% link _pages/en/suggested_schedule.md %}) is tight. Plan your time so that you can focus primarily on developing the [core]({% link _pages/en/documentation.md %}#specification-document) of your project.
- Do not spend more time on UI development than necessary to understand how your program functions.
- Example: If you are building a chess bot, move generation should be completed by the second week.
- 
There is little time for work that does not contribute directly to the project. Avoid tasks that do not align with your specific topic.

- Developing a 3x3 tic-tac-toe game does not help in creating a larger game, as most challenges arise in more complex boards.
- Fine-tuning a graphical UI for pathfinding does not advance your project, as the core focus is the pathfinding algorithms.
- Develop tests alongside your program - this is when they are most useful. However, the required test types depend on your topic; not all projects need performance testing.
- Ask the instructor if you are unsure about something. However, be prepared to think about the issue first. Instead of asking "What should I do now?", ask "Is developing X beneficial for my project?"

{% include typo_instructions_en.md %}
