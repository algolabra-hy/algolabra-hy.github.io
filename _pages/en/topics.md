---
layout: page
permalink: /topics-en
title: Topic suggestions for the project
title_long: Topics 
lang: en # fi or en
ref: topics # same as the markdown filename do not change 
---

This page will be made during the spring of 2025 and is included here for testing purposes. 

## Choosing a Topic

The main goal of the exercise is to implement and test more complex algorithms that have not been covered in previous courses. You can develop your own topic or choose one from the list below. The instructor will evaluate and approve the topic based on a specification document at the beginning of the course. If you choose your own topic, it may need to be adjusted to ensure appropriate complexity and scope.

Note that the suggestions below are only to help you get started. A key part of the exercise  is independent information gathering (with instructor support), studying your chosen topic, and understanding the algorithms. **Be prepared to spend time on this.** Implementing an algorithm without understanding how it works is extremely difficult and frustrating.

**Ask the instructor for guidance at any stage of the project, starting with topic selection.**

## Suggested topics
- [Graphs and pathfinding]({% link _pages/en/topics.md %}#graphs-and-pathfinding)
- [Data compression]({% link _pages/en/topics.md %}#data-compression) 
- [Games]({% link _pages/en/topics.md %}#games)
  - Gomoku
  - Minesweeper 
  - Chess
  - Reversi 
  - Battle Sheep 
  - 2048
  - Pentago
  - Rock-paper-scissors
  - 15-peli
- [DPLL]({% link _pages/en/topics.md %}#dpll)
- [Machine learning]({% link _pages/en/topics.md %}#machine-learning)
  - Computational creativity, text or music generation
  - Image recognition 
  - Generating dungeons
- [Encryption and Security]({% link _pages/en/topics.md %}#encryption and security)
- [Signal Processing]({% link _pages/en/topics.md %}#signal-processing)
- [Container packing]({% link _pages/en/topics.md %}#container-packing)
- [Regular expressions]({% link _pages/en/topics.md %}#compiler-or-interpreter-for-regular-expressios)
- [Spell checker]({% link _pages/en/topics.md %}#Spell-checker)
- [Scientific calculator]({% link _pages/en/topics.md %}#scientific-calculator)

---

## Graphs and pathfinding
How can the fastest/shortest route between two points in a graph be efficiently found? The graph nodes can be, for example, street addresses, public transportation stops, or coordinates.

### Detailed Specification

Implement a comparison of at least two different pathfinding algorithms. **Only one algorithm can be [Dijkstra’s algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) or [A\*](https://en.wikipedia.org/wiki/A*_search_algorithm)**, since Dijkstra is covered in the prerequisite Tira course, and A\* is very similar in implementation.

Suitable pathfinding algorithms for this project include:
- JPS (Jump Point Search). Useful visualization resources can be found for example [here](https://www.youtube.com/watch?v=NmM4pv8uQwI) and [here](https://zerowidth.com/2013/a-visual-explanation-of-jump-point-search/). The original research paper is available [here](http://users.cecs.anu.edu.au/~dharabor/data/papers/harabor-grastien-aaai11.pd).
- JPS can only be applied to grid-based maps, where movement is allowed in eight directions with two possible weights (depending on whether the movement is straight or diagonal).
 - Grid-based maps can be found, for example, on [the Moving AI Lab website](http://www.movingai.com/benchmarks/).
- [Fringe Search](https://webdocs.cs.ualberta.ca/~holte/Publications/fringe.pdf) is a more challenging but interesting algorithm to implement.

Additionally, solving the 15-puzzle, listed under the section [Games]({% link _pages/en/topics.md %}#games), is based on a pathfinding algorithm.


### Useful Tips  
When comparing pathfinding algorithms, it is essential to implement a visualization of the found path and the explored nodes/jump points **right from the start**. Without visualization, it is difficult to determine whether the algorithm is working correctly.  

Visualization helps verify the correctness of the search algorithm and speeds up debugging during development. However, implementing visualization should not take too much time, as the main focus should be on implementing and thoroughly testing the pathfinding algorithms. A graphical user interface can be useful, but simple ASCII graphics are sufficient if you are using grid-based maps.  

**Note:** To properly test correctness and efficiency, you need complex enough and sufficiently large maps that are suitable for the algorithms you are comparing. Creating such maps manually would be excessively time-consuming, so you should use ready-made maps from an external source.  

When implementing the code, **do not** attempt to create a separate "graph" object. Instead, read directly from integer or character arrays.

Ready-made maps can be found, for example, on the [Moving AI Lab](http://www.movingai.com/benchmarks/) website, in the [Shortest-Path Lab repository](https://bitbucket.org/shortestpathlab/benchmarks/src/master/grid-maps/), or from the [National Land Survey of Finland maps](http://kartat.kapsi.fi/). Note that in Moving AI’s grid maps, the reported distances are computed so that the path avoids the corner of an obstacle pixel rather than cutting diagonally across and partially passing through the obstacle pixel.  

Public transportation ([routes / schedules](https://developers.google.com/transit/gtfs/)), [Digitransit maps](https://digitransit.fi/en/developers/), and [open map data](https://www.openstreetmap.org) have also been popular sources for ready-made maps.

Some maps include distance data for various routes, which can be useful for testing. If your algorithm returns the correct path length for multiple sufficiently long and diverse routes, it probably finds the correct path. However, for example, when testing JPS, you must also examine that the processed jump points are correct. There may be errors in the algorithm that cause unnecessary computations, even if the shortest path is found.

## Data Compression

How can different types of files be compressed and decompressed efficiently? Compression algorithms can be categorized as either lossy or lossless methods. Lossy methods often achieve higher compression efficiency, meaning they can reduce file size more significantly. However, with lossy compression, the decompressed file may not be identical to the original. Lossy methods are commonly used for image and audio compression, whereas lossless methods are typically used for text compression. More about data compression on [Wikipedia](https://en.wikipedia.org/wiki/Data_compression).

### Detailed Specification

Implement algorithms for file compression and decompression. The appropriate number of compression algorithms to implement depends on their complexity. The instructor will provide further guidance on this. Meeting the course requirements requires typically implementing and comparing two different algorithms. However, some methods are complex enough that implementing just one is sufficient. **Discuss with the instructor** to determine a suitable scope, especially if you are working on image or audio compression.

Suitable compression methods for the project are for example 
- [Lempel-Ziv algorithms](https://en.wikipedia.org/wiki/LZ77_and_LZ78) such as LZ77, LZ78, LZSS, or LZW.
- [Huffman coding](https://en.wikipedia.org/wiki/Huffman_coding), which also requires efficient [Huffman tree storage](https://stackoverflow.com/questions/759707/efficient-way-of-storing-huffman-tree).

A suitable project topic is comparing one Lempel-Ziv algorithm to Huffman coding for text compression. The program must generate a single binary file on disk that contains all the necessary data for decompression, and its size should be characteristic of the chosen compression method. The compressed file must include, for example, a Huffman tree or a dictionary if the compression method requires one. These structures must also be stored efficiently — not in formats like XML or JSON.

### Useful Tips
When compressing natural language text (or program source code), the compressed file size should be approximately 40–60% of the original size, provided the input file is sufficiently large. For text compression, only lossless methods are used since the compressed text files must be fully restorable to their original form.
For image and audio compression, a much higher compression ratio is typically desired. However, this is only possible with lossy methods, meaning the compressed file cannot be restored to its original form.

Achieving the project requirements involves reading and writing data at the bit level, which cannot be done using the same tools as handling text files. You can use built-in data structures from your programming language for all compression algorithms.
**Note:** Your compression algorithms must be tested with [representative inputs]({% link _pages/en/testing_representative_inputs.md %}) that are sufficiently large.
End-to-end testing (compressing + decompressing and comparing the result to the original file) is a necessary part of correctness testing. Some errors only appear when the file is large enough or contains a sufficiently diverse set of characters. The compression method can not be tested separately because it is impossible to calculate manually the expected compressed result for a multi-megabyte file.

---

## Games
In this topic, you will choose a game and implement an AI for it. For most games listed below, AI can be implemented using the [minimax algorithm with alpha-beta pruning](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning). 

The minimax algorithm evaluates possible moves by looking ahead in the game and selecting a move that guarantees a win if such a move exists. The algorithm assumes that the AI and the opponent will always make the best possible move for themselves in every situation.
Since most game states cannot be fully calculated to a guaranteed win, loss, or draw, the algorithm searches ahead for a limited number of moves instead. It then uses a heuristic to evaluate how favorable each resulting position is. The move that leads to the best outcome according to this evaluation is then chosen.

**If you want to develop an AI for chess or Connect Four and you have a Linux machine**, we strongly recommend using the [AI platform]({% link _pages/en/ai_platform.md %}) for your project. The platform provides a graphical user interface and allows you to play against your AI with minimal overhead. Note that the platform currently works only on native Linux machines — any form of Linux emulation is not supported.

### Detailed Specification
Implement an AI for a game. Your AI must be able to play against a human through the user interface. To use your AI, you must also implement the game logic and the user interface. However, do not spend too much time on these parts — the core focus of the project is the AI itself. You must not use pre-made libraries for game logic. This means that tasks such as generating legal moves, detecting wins, and executing moves must be implemented by you. You may use existing tools for the user interface, but for many games, a text-based interface is completely sufficient. The UI does not need to be tested.

Below is a list of some games that are suitable for a topic, along with useful advice for each one. For games where the game logic and the user interface are easier to implement, the AI itself is required to have more advanced features. These additional requirements are mentioned separately for each game. Unless some other solution is suggested, AI for these games can be implemented using the minimax algorithm.
If you want to optimize minimax, the first step — regardless of the game— is to implement iterative deepening and move reordering as described for the Connect Four game. Using a transposition table allows even more reuse of previously computed values. However, combining transposition tables with iterative deepening can be challenging, and finding the correct information on it may be difficult — so feel free to ask the course instructor for guidance. Without iterative deepening, the heuristic function that evaluates a game state is just as good as its ability to estimate the game state’s potential. However, when iterative deepening is used, the consistency of the heuristic function (which is not always the same as correctness) becomes an important factor affecting search speed. Guidance on this can also be obtained from the instructor.

#### Five in a Row / Gomoku
Implement Five in a Row played on a 20 × 20 grid, where the goal is to form a row of at least five marks to win. 

**Additional Requirements.**
- For a successful implementation, an efficient solution is required, which includes:
Investigating only free spaces that are at most two spaces away from previously made moves, or some better way of pruning moves to experiment. The moves are not computed separately for each game state, but a list of moves is maintained and updated with each move made or experimented with during the computation. This updated list is passed as a parameter to the next level in the minimax.
- In Five-in-row, it’s often necessary to respond to the opponent's previous move, or it may be beneficial for future moves. The best response is often a move adjacent to the previous one. Follow this heuristic by prioritizing the neighbors of the last move and making them the first to investigate.
- Win detection is done by examining only the rows that contain the last move. If a row of five marks is formed, the player who made the previous move is the winner, and the last move is part of the winning row. 

**Useful Tips**

Do not first implement the game logic and AI for a 3 × 3 board. Everything needs to be done quite differently when the board is large.

#### Chess

A chess game played on an 8 × 8 board with standard rules, where you may choose to omit some or all of the following features:

    Castling
    En passant
    Pawn promotion
    Stalemate

Your project’s heuristic function should evaluate, in addition to material count, the placement of pieces on the board. For the UI, you can use the [AI platform]({% link _pages/en/ai_platform.md %}) provided for the project.

#### Connect4
The game is played on a 6 × 7 board, and the goal is to get four of your own pieces in a row. If you're not familiar with the game, see [Connect Four on Wikipedia](https://en.wikipedia.org/wiki/Connect_Four).
**This is a good topic** if you want to spend most of your time specifically optimizing the minimax algorithm. Generating the moves to be investigated and executing the moves in Connect4 is simpler than in many other games, allowing you to focus on improving the AI.

[This AI](https://connect4.gamesolver.org/) plays Connect4 perfectly. It can be used to study the game and, for example, to generate game states that lead to a guaranteed win, which you will need for testing.

**Additional Requirements.**
In minimax-based Connect4 projects, the following optimizations are required:
- *Basic move ordering.* In all stages of computation (within the minimax), always try making a move in the central column first and then proceed towards the edges. This speeds up alpha-beta pruning because the best move is often found in the center.
- *Iterative Deepening.* Perform minimax first at a shallow depth, and then progressively at greater depths until the time limit is reached. This allows better use of available time, as the time required for calculations at the same depth can vary significantly between game states. For each examined game state, store the information about which move was best for the current player. When the same game state is visited during the same or a later iteration, the move previously identified as the best is investigated first. It is often the best or at least a good move even when deeper moves are computed, so alpha-beta pruning becomes more effective as the alpha/beta values are quickly adjusted. Create a new hash table every time the user has made a move, and the AI decides its next move. The memory usage is moderate, and you can use a regular hash table (dictionary, HashMap). In the hash table, the key represents the game state, and the value is the move.
- Win detection is done by examining only the rows that contain the last move. If a row of four marks is formed, the player who made the previous move is the winner, and the last move is part of the winning row. 

**Note** that in iterative deepening, you cannot store move values in the hash table and return them in later iterations. You only can store information about the best move in the state. Values computed in earlier iterations are not valid because the heuristic value changes as deeper computations are performed. The same game state can be reached through multiple move sequences also within the same iteration, but due to alpha-beta pruning, the computed values are often not exact but rather upper or lower bounds of the true values. Therefore, the value computed previously cannot be directly used even when the search depth is the same. All valid moves must be investigated unless an alpha-beta cutoff occurs, and the move previously estimated best can only be used for move ordering.

#### Othello / Reversi

In Othello, you have an 8 × 8 board. The player with the most pieces on the board when the game ends wins the game.

**Useful Tips**
Compared to chess, for example, evaluating a game state meaningfully in Othello is difficult. However, the same challenge applies to a human player as well.
Guidance on designing a heuristic evaluation function can be found, for example, in:
- [Kartik Kukreja’s blog](https://kartikkukreja.wordpress.com/2013/03/30/heuristic-function-for-reversiothello/).
[Vaishnavi Sannidhanam and Muthukaruppan Annamalai’s course project](https://courses.cs.washington.edu/courses/cse573/04au/Project/mini1/RUSSIA/Final_Paper.pdf)

Besides minimax, you can also use [Monte Carlo Tree Search](https://en.wikipedia.org/wiki/Monte_Carlo_tree_search) to decide the moves without an evaluation function.

#### 2048
[2048](https://en.wikipedia.org/wiki/2048_(video_game)) differs from the previous games in that it features only one player and a random element. [Expectiminimax algorithm](https://en.wikipedia.org/wiki/Expectiminimax) applies to such problems, modified so that instead of two players, there is one player and a random event. Good results have also been achieved using minimax, where the random event is treated as the opponent, even though this approach assumes that a new number always appears in the worst possible location with the worst possible value.

If you take a model for the heuristic evaluation function from somewhere, note that the same function might not be ideal for both minimax and expectiminimax. With minimax, a greater search depth can be achieved through alpha-beta pruning, so, for example, the number of free squares better predicts success. A good heuristic function, in any case, considers both the number of free spaces and the distribution of values.
Yun Nie, Wenqi Hou, and Yicheng An have written a [short article on the approaches and heuristics](https://cs229.stanford.edu/proj2016/report/NieHouAn-AIPlays2048-report.pdf).

#### Battle sheep

[Battle Sheep](https://www.lautapelit.fi/product/20852/battle-sheep) is a fun alternative to classic games. The board doesn't need to be modifiable like in the board game; you can use an appropriate fixed board. A graphical user interface is highly recommended for this game to ensure smooth gameplay.

#### Pentago
[Pentago](https://www.martinexshop.com/peliko-pentago) is also an interesting new game that can be implemented using minimax. It is challenging for human players to plan moves that involve rotating parts of the board, so the AI has a good opportunity to excel. On the other hand, at the start, there are as many as 36*8 = 288 possible moves. Even computing only four moves ahead (two pairs of moves) requires efficient solutions.

#### Rock-Paper-Scissors

Rock-paper-scissors is a game familiar to everyone that generally cannot be played well or poorly. An AI for the game cannot be implemented using the minimax algorithm because it assumes that the opponent always makes the best counter-move, which means that every move you make leads to a loss and is equally bad. Instead, develop an AI that tries to learn its opponent's playing style and perform well against it. One way to learn an opponent's style is to use [Markov chains](https://arxiv.org/pdf/2003.06769) of various orders (see also the section on [computational creativity]({% link _pages/en/topics.md %}#machine-learning)). Other models of the opponent's behavior can also be added to this framework. **It is advisable to discuss this topic with your supervisor if you are interested**.

#### 15 Puzzle
[The 15 Puzzle](https://en.m.wikipedia.org/wiki/15_Puzzle) is a challenging problem, and solving it can take a significant amount of time in the worst-case scenario, especially with a weak heuristic. The solution should primarily utilize the [IDA* algorithm](https://en.wikipedia.org/wiki/Iterative_deepening_A*). Discuss with your supervisor if you wish to use an alternative approach. Heuristic distance functions suitable for this puzzle are described, for example, on [Michael Kim’s blog](https://michael.kim/blog/puzzle). More information on the IDA* algorithm can be found on, for instance, the [Geeks for Geeks website](https://www.geeksforgeeks.org/iterative-deepening-a-algorithm-ida-artificial-intelligence/).

#### Minesweeper
Information on Minesweeper solvers suitable for this course can be found in [David Becerrar's bachelor's thesis](https://dash.harvard.edu/handle/1/14398552). If you are using Java in your project, you can implement the solver/assistant interface using the provided [Minesweeper project template](https://github.com/TiraLabra/minesweeper). If you use the ready-made Java template, clearly indicate in the code comments which parts are your code and which belong to the template. Do not modify the template; instead, write your code in new classes/methods.

---

## DPLL

[The Boolean satisfiability problem](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem) (SAT) is central to theoretical and applied computer science. Modern implementations of so-called CDCL algorithms (SAT solvers) are capable of determining the satisfiability of formulas containing millions of variables. Such algorithms are used in many [practical applications](https://en.wikipedia.org/wiki/SAT_solver#Applications); for example, efficient SAT solvers are essential in verifying the correctness of various circuits.
Implementing an efficient CDCL algorithm is too demanding for a course project. Instead, in this topic we will study its predecessor, the [DPLL algorithm](https://en.wikipedia.org/wiki/DPLL_algorithm).

### Detailed specification
Implement a program that reads a propositional logic formula in conjunctive normal form (CNF) from a [DIMACS](https://www.cs.utexas.edu/users/moore/acl2/manuals/current/manual/index-seo.php/SATLINK____DIMACS) formatted file and returns either a satisfying truth assignment or a confirmation that no such assignment exists. The program must use the DPLL algorithm.
The program must implement [unit propagation](https://en.wikipedia.org/wiki/Unit_propagation) and [pure literal elimination](https://users.aalto.fi/~tjunttil/2020-DP-AUT/notes-sat/preprocessing.html#pure-literal-elimination). A more detailed explanation of the algorithm can be found [here](https://users.aalto.fi/~tjunttil/2020-DP-AUT/notes-sat/dpll.html). The data structures required for handling the formula must be implemented from scratch. C++ is the best language for implementing this topic.

### Useful tips
You can test the correctness of your algorithm by comparing its results with those of a CDCL SAT solver. Suitable options for this include [CaDiCaL](https://github.com/arminbiere/cadical/tree/master) and [Kissat](https://github.com/arminbiere/kissat). Both repositories also contain test formulas: [CaDiCaL tests](https://github.com/arminbiere/cadical/tree/master/test/cnf), [Kissat tests](https://github.com/arminbiere/kissat/tree/master/test/cnf).
Notice that both CaDiCaL and Kissat are highly optimized implementations of the CDCL algorithm, and your solver will not come close to their efficiency within the scope of this course.

You can generate additional test formulas using tools like [CNFGen](https://massimolauria.net/cnfgen/).

**Additional Challenge**
If you want an extra challenge, you can explore the [2-watched literal technique](https://www.youtube.com/watch?v=n3e-f0vMHz8) for implementing unit propagation efficiently.
Without the 2-watched literal technique, your program will likely only be able to solve formulas with around 100 variables. This is sufficient for the course project, but you should adjust your test inputs accordingly.
Further optimizations for your algorithm can be found in the [Aalto University course materials](https://users.aalto.fi/~tjunttil/2020-DP-AUT/notes-sat/cdcl.html). A particularly significant (but challenging) optimization is learning conflict clauses and performing non-chronological backjumping.

Keep in mind that SAT solvers can be used to solve various problems by first encoding them in propositional logic. Can you make your DPLL algorithm efficient enough to solve [Sudoku puzzles](https://sat.inesc-id.pt/~ines/publications/aimath06.pdf)?

---







{% include typo_instructions_en.md %}
