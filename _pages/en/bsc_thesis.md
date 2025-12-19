---
layout: page
permalink: /bscthesis-en
title: The algorithmics project and the bachelors thesis
title_long: Kandi
lang: en # fi or en
ref: bsc_thesis # same as the markdown filename
---

## An Important Note 
These pages contain information regarding the use of your algorithmics project in your B.Sc. thesis. **We emphasize** that the discussion on these pages should not be interpreted as a guarantee of acceptable topics for your thesis. All decisions regarding the scope of B.Sc. theses are made by the thesis seminar personnel. The views on these pages are based on previous experiences of the project personnel regarding thesis supervision. Current practices might be different, and you should contact the thesis seminar personnel for the most up-to-date information.

To put it another way, if you pick a topic from these pages and produce an acceptable algorithmics project, then you can most likely agree with your thesis supervisor to write about a related topic in your thesis. However, picking a topic from these pages does not automatically commit you to any specific thesis topic. You should also be proactive in letting the personnel of the thesis seminar know if you are interested in writing about a topic related to your algorithmics lab.

## The Algorithmics Project as Support for the Thesis 
Many of the [project topics]({% link _pages/en/topics.md %}) we list as examples can also work as thesis topics. Since the successful completion of an algorithmics project will require you to learn about the [core of your project]({% link _pages/en/documentation.md %}#specification-document) anyway, we strongly recommend that you make use of the newfound understanding when writing your thesis.

A well-planned and realized algorithmics project can, in some cases, offer an opportunity to include an experimental section in your thesis. You could, for example, use the final project to measure the performance of the algorithm in line with the research objectives of your thesis. You should agree on the inclusion and contents of an experimental section with your thesis supervisor early in the project. Note also that, in most cases, the thesis seminar alone is not long enough to allow implementing and evaluating algorithms. If you are interested in including an experimental section, we strongly recommend that you make use of the opportunity provided by the algorithmics project.

## Project Topics as Thesis Topics
The rest of the page contains free-form thoughts on the suitability of project topics as thesis topics. We assume that you have familiarized yourself with the corresponding sections on the [topic pages]({% link _pages/en/topics.md %}). A general rule of thumb is that for a project topic to be suitable as a thesis topic, you should be able to find scientific publications (not just course books) on the topic. The motivation, planning, and analysis of a (potential) experimental section should be tied to the research literature to be a part of the research into the thesis topic. The purpose of an experimental section is to produce more information on the algorithm or the corresponding section of the thesis, not to be its main content.

### Graphs and Pathfinding
If you want to write about [pathfinding]({% link _pages/en/topics.md %}#graphs-and-pathfinding) in your thesis, you should ensure that you can find scientific publications on the algorithms you implement, not only course books. Suitable algorithms include, for example, Jump Point Search (JPS) or more complex methods. One possible approach would be to implement JPS in your algorithmics project and discuss it and [Fringe Search](https://webdocs.cs.ualberta.ca/~holte/Publications/fringe.pdf) in your thesis, even if you do not implement the latter in your project. In contrast, basic approaches like A* and Dijkstra are most often not suitable as thesis topics as they can be difficult to find references on.

### Data Compression
The Lempel–Ziv algorithms mentioned on the [example topics]({% link _pages/en/topics.md %}#data-compression) page are suitable for thesis topics. As they are somewhat older, the existing scientific literature on them might, however, require a bit more effort to read.

If you are interested in including an experimental section on data compression in your thesis, we recommend that you focus your algorithmics project on text compression, since designing and executing an experimental section on text compression is often simpler than experimenting with image or sound compression.

### Games
The pure minimax algorithm with alpha–beta pruning is too simple to be a thesis topic on its own. You can, however, write your thesis about its extensions, such as the [ProbCut](https://journals.sagepub.com/doi/abs/10.3233/ICG-1995-18202) algorithm. Game AI can, however, be challenging to scope down into a thesis topic.


### DPLL
The [DPLL]({% link _pages/en/topics.md %}#dpll) algorithm, or the more broadly used CDCL algorithm, can be used as the basis for numerous different thesis topics. If you want to include an experimental section in a DPLL-themed thesis, you should implement several different search heuristics in your algorithmics project.

### Machine Learning
[Machine learning]({% link _pages/en/topics.md %}#machine-learning) is a broad area. While some topics in machine learning are suitable for thesis topics, many are too complicated. As such, any thesis topic related to machine learning should be carefully discussed with your thesis supervisor. While definitive statements on good project topics are difficult to make, we recommend you focus on straightforward approaches that lend themselves to measurable performance. For example, while a program that produces “nice-sounding music” is perfectly acceptable as a project topic, it is not well-suited for a B.Sc. thesis since measuring the “niceness” of music is too subjective, and the algorithms underlying music production are often too complex to write theses about. A better idea is to implement a simple neural network with basic backpropagation that classifies handwritten digits.

### Dungeon Generation
[Dungeon generation]({% link _pages/en/topics.md %}#dungeon-generation) is not the best basis for a B.Sc. thesis. An abstract treatment of some of the algorithms underlying dungeon generation methods could work as a thesis topic, as long as scientific papers on them can be found. Also remember that you cannot report on the “niceness” of the dungeons your program creates in an experimental section; plan your project in a way that lets you extract additional information on the operation of the algorithms.

### Encryption and Security
The algorithms related to [encryption]({% link _pages/en/topics.md %}#encryption-and-security) or the computation of prime numbers often lend themselves to thesis topics. In contrast, the algorithms for breaking encryptions that we propose are typically too simple to write theses about.

### Signal Processing
The techniques used in [signal processing]({% link _pages/fin/topics.md %}#signal-processing) can often be used for topics for a B.Sc. thesis. You should, however, be careful to ensure that you can find scientific publications on your project topics. For example, implementing the [fast fourier-transform](https://en.wikipedia.org/wiki/Fast_Fourier_transform) based on a course book is perfectly acceptable as an algorithmics project; your B.Sc. thesis should also include references that are not course books.


### Container Packing
The [container packing]({% link _pages/en/topics.md %}#container-packing) project topic is based on the so-called [knapsack](https://en.wikipedia.org/wiki/Knapsack_problem)-problem, one of the classical NP-complete problems. Such problems can form the basis for your B.Sc. topic, as long as the specific scope is discussed with your thesis instructors.


### Interpreter or Compiler for Regular Expressions
[Regular expressions]({% link _pages/en/topics.md %}#interpreter-or-compiler-for-regular-expressions) are part of the B.Sc. courses. As such, potential thesis topics on this subject should be sufficiently expanded. Make sure to talk about the topic with your thesis supervisor.


 
{% include typo_instructions_en.md %}




