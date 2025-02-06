---
layout: page
permalink: /testreqs-en
title: Testing requirements
title_long: How to get high marks
lang: en # fi or en
ref: testing_requirements # same as the markdown filename should not be changes
---
## Requirements for Tests – What Needs to Be Tested?
Each project requires at least automated [unit tests]({% link _pages/en/unit_testing.md %}) that test the **functionality** of the work.
 The user interface and I/O (such as file reading) do *not* need to be tested, and no extra points will be awarded for testing these elements.
Generally, the purpose of tests is to ensure that your algorithm is correctly implemented. What this means in practice depends on the topic. Below are some examples. The course staff will assist if needed.
- Is your neural network structure as it should be?
- Does your game AI always make legal moves?
- Does your chess bot checkmate if it’s possible in its search depth?
- Does your pathfinding algorithm visit exactly the nodes it should and no more?
- Does your RSA encryption work correctly with both small and large keys?
- Does your data compression algorithm correctly compress and decompress files of all sizes?

Another important part of convincing tests is testing with [representative]({% link _pages/en/testing_representative_inputs.md %}) inputs. Many algorithms implemented in the project are complex enough that not all bugs can be found with small inputs. For RSA-related projects, for example, realistic prime numbers are not 13 or even 61403. You operate on numbers with hundreds of digits. Convincing tests, therefore, include both "human-readable" inputs and "realistic" inputs.
 Typically, convincing tests require more than just unit testing and may involve [advanced testing techniques]({% link _pages/en/testing_frontpage.md %}#beyond-unit-testing). Consider what would suit your project and consult your instructor if needed. Typically, [integration](https://en.wikipedia.org/wiki/Integration_testing) or [end-to-end testing](https://www.techtarget.com/searchsoftwarequality/definition/End-to-end-testing) should be sufficient.

## The Purpose of Tests in This Course
An essential part of this course is the independent design and implementation of a complete project and its tests.
The aim is — with the instructor's help — to think for yourself about what kind of tests are needed to be (reasonably) confident that your program is correctly implemented. Note that this is different from testing the efficiency of your program. In other courses, tests are often provided in advance, and you must pass those specific tests. In this course, however, you are expected to understand what should actually be tested in each project. **Be prepared to spend time on test design.** Consider what each method in your program should do. What size inputs should they handle? What edge cases should be addressed? Note that, for example, the number of tests is not what matters most. Representative tests can often be achieved with just a few well-chosen test cases and inputs. On the other hand, a large number of randomly written tests may not be efficient.

Aim to ensure that for every test you implement, you can explain (at least to yourself) why this test with these inputs is included.
**The instructor is available to help if needed** — reach out if you're struggling to progress with the tests. However, be prepared for the instructor to ask what your method is supposed to do and what size inputs it should handle. You don’t need to have exhaustive answers to these questions before contacting the instructor. Think about them and be ready to explain your perspective to the instructor about why the test development isn't progressing.

## Grading of the Tests
The table below provides more detailed guidance on what is required from the tests in the project. However, each project will always be evaluated as a whole, and for example, the difficulty of the topic may slightly influence the evaluation. It is advisable to ask the instructor for help when needed.
 In the table, the word "method" refers to the methods of the functional logic.

 ---
| Level (score)                     | Description |
| :---------------------------------  |--------: |
| Insufficient/Fail (0)             | <span style="font-size:0.9em;">The main methods of the project are not tested at all, or the tests do not verify correctness-related aspects.</span> |
| Weak (1)                    |  <span style="font-size:0.9em;">The main methods of the project are tested with a few inputs. There are issues with the [representativeness]({% link _pages/en/testing_representative_inputs.md %}) of the selected inputs.</span>        |
| Average <br> (2-4)           | <span style="font-size:0.9em;">The key methods are tested with a few [representative]({% link _pages/en/testing_representative_inputs.md %}) inputs. The documentation of the tests explains their purpose.</span> |
| Satisfactory (5-7)              |  <span style="font-size:0.9em;">All key methods are tested. The inputs used are representative. The tests are repeatable and clear.</span>       |
| Convincing/Excellent (8-10)| <span style="font-size:0.9em;">Testing uses techniques that are appropriate for the topic and essential for testing correctness. The tests are very clear. The inputs used are well-justified and representative.</span>  |

 ---



{% include typo_instructions_en.md %}


