---
layout: page
permalink: /documentation-en
title: Dokumentaatio
title_long: Työn aikana tehtävät dokumentit
lang: en # fi or en
ref: documentation # same as the markdown filename
---
All documents must be submitted either in a GitHub-supported Markdown format or as a .pdf file in your [repository]({% link _pages/en/git.md %}).
Submissions via email, for example, will not be accepted.
Place the documents in their own directory at the root of the project and link them to the repository's main page.
## Weekly Submissions
Some course points are awarded based on the weekly progress of your project.
As the weekly deadline approaches, ensure your repository is up to date and add your weekly report.
Progress will be reviewed only once a week, but you should push changes to the repository at least at the end of each development day.
### Writing the Weekly Report and Logging Hours
The report should be approximately half a page to two pages long.
It must be submitted as part of the weekly submission, placed in the same directory as other documentation, and clearly named, e.g., Weekly Report 1.

Include in your weekly report the time you spent working on the project during the week. The number of hours logged will not affect grading.
The report should be written in Markdown or submitted as a PDF.
Answer the following questions in your report:
1. What did I do this week?
2. How has the program progressed?
3. What did I learn this week/today?
4. What remains unclear or has been challenging?
- Answer this honestly, as you can receive help based on your response.
5. What will I do next?
You may also include feedback or questions for the course instructors in your weekly report. Questions will be answered as part of the weekly feedback.

**NOTE:**
Even if you haven't done any work during a particular week, you should still write a weekly report to ensure there are changes in the repository for that week. You may even earn points for it. Otherwise, you will automatically receive 0 points, even if your project would otherwise be eligible for weekly points.

A repository that remains unchanged for three consecutive weeks will be considered a course withdrawal.

## Project Documentation
The project documentation consists of the following parts:
- Code documentation
- Specification document
- Implementation document
- Testing document
- User guide
  
The significance of documentation in the course is relatively minor; the main focus is on functional and efficient code. Each document should be approximately 1–2 A4 pages long, excluding any images and tables if they are relevant to the content.

### Code Documentation
The program code and structure must be clear. Methods should be sufficiently short, and classes, variables, and methods must be descriptively named.

Write the code as clearly and understandably as possible. Comment your code thoroughly but concisely. While not every class, method, or attribute requires a comment, all essential and non-obvious aspects must be explained in comments. Method comments should include descriptions of their parameters and return values. Ideally, internal commenting within methods should not be necessary, as methods should be descriptively named, compact, simple, and easy to comprehend. However,  internal comments may be used if a method's functionality is difficult to grasp from the code and its general comment alone.

JavaDoc comments are used in all Java projects. If you are using NetBeans, it can generate JavaDoc comment templates for classes and methods. In Python programs, follow the documentation style taught in the Software Engineering course using [docstrings](https://ohjelmistotekniikka-hy.github.io/python/viikko6#docstring-ja-koodin-dokumentointi).
For other programming languages, follow the documentation conventions specific to that language.

### Specification Document
The specification document must include the following information:
- Which programming language are you using?
- Also, mention any other languages you are proficient in to the extent that you could peer-review projects written in them.
- What algorithms and data structures will you implement in your project?
- What problem are you solving?
- What inputs does the program receive, and how are they used?
- Expected time and space complexities (e.g., Big-O analysis)
  - Find out as much as possible. You are not expected to prove or measure anything yourself.
  - Use time and space complexity as a tool to understand how to approach the project.
  - Check Wikipedia or other reliable sources, and ensure you understand where these complexities come from in your algorithm. Why does your algorithm require that amount of time?
- References
  
**The Core of Your Project**
Describe the *core* of your project in a few sentences within the specification document.
**Take your time on this**, as it will help in the project's development.
Although the project requires additional code beyond its core functionality, most of your development time should be spent on the core. Plan your time accordingly.
- If your project focuses on game AI, the core is artificial intelligence, not methods required for running the game.
- If your project is about pathfinding, the core is pathfinding algorithms, not methods for visualizing graphs.

For administrative reasons, the specification document must also mention the study program you belong to (e.g., Bachelor's in Computer Science (TKT) or Bachelor of Science (BSc)). Additionally, it should specify the language used in the project documentation.
In this course, the specification document serves as an early-stage planning tool and does not need to be updated during the course unless the instructor requests clarifications.
**Note** that the instructor has assessed the project's scope and difficulty based on the specification document. A significantly smaller-scale project is usually not sufficient for passing the course.

### Implementation Document
The implementation document must include the following:
- The general structure of the program
- Achieved time and space complexities (e.g., Big-O analysis based on pseudocode)
- Performance and Big-O complexity comparison (if relevant to the project)
- Possible shortcomings and suggestions for improvement
- **Use of large language models (ChatGPT, etc.). Mention which model you used and how. If you did not use any, explicitly state that. This is important!**
- References


{% include typo_instructions_en.md %}
