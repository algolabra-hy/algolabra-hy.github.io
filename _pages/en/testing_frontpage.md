---
layout: page
permalink: /testing-en
title: Testing the Project
title_long: Testing the Project
lang: en # fi or en
ref: testing_frontpage # same as the markdown filename
---
## Testing Requirements
Read about the [testing requirements]({% link _pages/en/testing_requirements.md %}) in the course evaluation.
## Unit Testing and Dependency Injection
If you are not familiar with unit testing, read the [unit testing guide]({% link _pages/en/unit_testing.md %}) from the Software Engineering course. The material on [dependency injection]({% link _pages/en/dependency_injection_python.md %}) may also be useful. Dependency injection is a programming technique that makes testing easier.

## Testing Complicated Algorithms
The coursework involves implementing complicated algorithms. Testing these can be challenging, as unit tests are often not sufficient. Proper testing of complicated algorithms requires a deep understanding of how the algorithm works. What does it mean for your algorithm to be correct?
- The correctness of a game-playing bot is not simply that it plays well. For example, a Minesweeper bot should never hit a mine when a tile is considered safe. A chess bot must not make illegal moves and should be able to deliver checkmate, if possible within the given search depth.
- The correctness of a pathfinding algorithm is not just about finding the shortest path. For example, an A* search with an inverted heuristic will still find the shortest path but will take much longer than expected.
- For a compression algorithm, correctness is not just ensuring that the decompressed file matches the original. Additionally, the size of the compressed file should meet the expectations.
- When testing the correctness of neural networks, it is not enough that the network classifies a large portion of the test set correctly. You also must test whether the network’s structure is correct and whether backpropagation functions as expected.

### Representativeness of Test Inputs
For complicated algorithms, it may be difficult to come up with representative inputs for testing. Can we be sure that our test inputs cover all branches? What if our code only fails with inputs larger than a thousand? Especially when testing complicated algorithms, it is crucial that the test inputs are representative.
Read more about representative test inputs [here]({% link _pages/en/testing_representative_inputs.md %}).

### Beyond Unit Tests
While unit tests and representative inputs go a long way, [comprehensive coursework testing]({% link _pages/en/testing_requirements.md %}) often requires additional testing techniques. Examples of such techniques include:
- [Integration Testing](https://en.wikipedia.org/wiki/Integration_testing).
- [End-to-End Testing](https://www.browserstack.com/guide/end-to-end-testing)
- [Invariant Testing]({% link _pages/en/invariant_testing.md %}), and
- [Performance Testing]({% link _pages/en/performance_testing.md %})
***Note:** You don’t need to use all of these. The most important thing is to choose the testing methods that best suit your coursework. The course staff can assist.
Compared to unit tests, correctness and performance tests for more complex features can take a significant amount of time. Therefore, they may not be ideal to run alongside unit tests every time. Instead, a few representative cases (e.g., automatically found ones) can be included in unit tests, while the rest can be executed separately in a dedicated test program.
In other words, your coursework should include *both* unit tests and more advanced testing methods.

## Additional Material
- [Pylint]({% link _pages/en/pylint.md %}) is a static analysis tool for Python code that helps maintain code quality.
- [Testing Neural Networks](https://www.sebastianbjorkqvist.com/blog/writing-automated-tests-for-neural-networks/) – A blog post by Sebastian Björkqvist.
- [Range Minimum Query Example](https://github.com/TiraLabra/Testing-and-rmq) – A repository with examples of testing more complicated algorithms.

{% include typo_instructions_en.md %}
