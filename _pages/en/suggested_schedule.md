---
layout: page
permalink: /schedule-en
title: Recommended Schedule for the Project  
title_long: Recommended Schedule for the Project
lang: en # fi or en
ref: suggested_schedule # same as the markdown filename
---
The course has a submission every Saturday of weeks 1–6, and the deadlines can be found in the course calendar on Moodle.
## Week 1
- **Topic, Programming Language, and Scope Decided**  
  - Explore [topic suggestions]({% link _pages/en/topics.md %}).  
  - Discuss with the instructor if needed, especially if your planned topic is not on the suggested list.  
  - The instructor will review the specification document and provide feedback if necessary.  

- **[Exercise Repository]({% link _pages/en/git.md %}) Initialized and Registered in [Labtool](https://study.cs.helsinki.fi/labtool/)**  
  - Remember to enable [issues]({% link _pages/en/git.md %}#allowing-issues).  

- **[Project Management]({% link _pages/en/project_maintenance_frontpage.md %}#project-management) in Order**  
  - This means the repository should be set up and registered in Labtool.  
  - Additionally, there should be a way to compile code and manage dependencies.  
  - For Python, it is recommended to use Poetry, as other students commonly use it too, and it is a familiar tool for them.

**Week 1. Submission** (Check the date in the course calendar and [instructions]({% link _pages/en/documentation.md %}) for submissions)
-[Weekly Report 1]({% link _pages/en/documentation.md %}#weekly-submissions)
-[Specification Document]({% link _pages/en/documentation.md %}#specification-document)
Important: Remember to include your study program and the project’s programming language in the specification document!
Also, make sure to clearly define the core of your exercise project. More instructions can be found in the [specification document guidelines]({% link _pages/en/documentation.md %}#specification-document).

## Week 2
- Development of the **core area** of the project should begin **this week**.  
  - For example, if you're working on AI for a game, you should (preferably) start developing the AI itself this week.  
  - If your project involves implementing data structures, you can initially use built-in structures from your programming language and replace them later.  

- The project's code is [documented]({% link _pages/en/documentation.md %}#code-documentation) from the start.  

- Development of project tests (including [unit tests]({% link _pages/en/unit_testing.md %})) using [representative inputs]({% link _pages/en/testing_representative_inputs.md %}) has begun.  
  - Develop tests alongside your code.  
  - Tests should measure the *correctness* of your code. Don’t spend unnecessary time on excessive tests — first, consider what types of tests your project actually needs.  
    - The [Testing]({% link _pages/en/testing_frontpage.md %}) pages contain useful materials, but not all projects require everything found there.  
  - The project's [test coverage]({% link _pages/en/unit_testing.md %}#has-enough-testing-been-done-test-coverage) should be tracked.  

**Week 2. Submission**  
- [Weekly Report 2]({% link _pages/en/documentation.md %}#weekly-submissions)  

## Week 3
- **Core Project Area Developed**  
  - The project has a working (not necessarily polished) user interface.  
  - **All supporting methods for core functionality are complete.**  
  - Ideally, by this week, the project should be runnable, and its functionality should be observable.  

- Code quality is maintained using tools like [Pylint]({% link _pages/en/pylint.md %}).  

- The main implemented methods are comprehensively unit-tested with [representative inputs]({% link _pages/en/testing_representative_inputs.md %}).  

- Writing of the [Testing Documentation]({% link _pages/en/documentation.md %}#testing-document) has begun.  
  - The document includes a [test coverage report]({% link _pages/en/unit_testing.md %}#has-enough-testing-been-done-test-coverage).  

### **Week 3. Submission**  
- [Weekly Report 3]({% link _pages/en/documentation.md %}#weekly-submissions)

## Week 4
This week, focus on preparing your project for **peer review**.  
Ensure that your code is in a state where meaningful feedback can be given.  

- The **core functionality** of the program is nearly complete. Any custom data structures have been started.  
- Code is well [documented]({% link _pages/en/documentation.md %}#code-documentation) and thoroughly tested.  
- Work on the [Implementation Document]({% link _pages/en/documentation.md %}#implementation-document) has begun.  
- Development of **additional tests** beyond unit tests has started.  
  - Remember that not all types of tests are necessary—focus on those most relevant for validating your project.  
  - Document these in the [Testing Documentation]({% link _pages/en/documentation.md %}#testing-document).  

### **Week 4. Submission**  
- [Weekly Report 4]({% link _pages/en/documentation.md %}#weekly-submissions)  
- The **first peer review** will be assigned after this week’s submission.  
  - Find the link to the repository under review in Labtool.  
  - Remember to enable [issues]({% link _pages/en/git.md %}#allowing-issues).  
  - The peer review deadline is the same as for Week 5’s submission.  
  - Peer review instructions are available on [Moodle]({{site.moodle}}).
 
## Week 5


{% include typo_instructions_en.md %}
