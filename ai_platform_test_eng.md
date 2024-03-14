---
layout: page
permalink: /aiplatformtesteng
title: Artificial Intelligence Platform Testing
title_long: AIPlatform
inheader: no
---

<div style="color:black; border-style: solid; border-width: thick; border-color: red; padding: 10px; margin-bottom: 15px; padding: 10px; background-color: #F1EFEF;">

<h4>Currently Under Test Use</h4>

<p>
The AI platform is currently in (beta) testing for this course (4th period of the academic year 23-24). The course staff is also still learning to use it. Hence, there may be some uncertainties in the instructions, and practices may change. We aim to minimize the disruptions caused by these changes to the students.

Currently, the platform is only functional on Linux.
</p>

</div>

During this course, you can test the artificial intelligence development platform that is currently being developed for the AI project. Currently, the platform supports the development of a chess AI **on Linux**. So, if you plan to develop a chess AI for your project work, we recommend trying out this interface and providing active feedback on it to its developers.

In short, the platform provides a graphical user interface and the possibility to (fairly) easily play against your own AI. The purpose is to facilitate easier access to the core of the project work (i.e., working on the AI itself).

**If you plan to try the interface**:
1. Mention this in your specification document.
2. Add a brief feedback on its functionality and its impact on the project work development to each weekly report.
3. Remember to write in your manual how to run the entire project. This is important for example for peer review.

## Instructions for Downloading the Interface
![]({{ "/images/ailocal0.png" | absolute_url }})

1. Start by downloading the [AI-local](https://github.com/game-ai-platform-team/tira-ai-local/releases/tag/v1.0.0) release from the repository (the .zip file in the picture).
1. Unzip the file and launch the tira-ai-local program found therein (either from the terminal or by clicking on the folder).

![]({{ "/images/ailocal1.png" | absolute_url }})

After starting the program, you can link the root folder of your own AI project (enter into the file-path box then press submit).

**If the program does not run** your linux distribution might be missing the libatk library. You can install it following the instructions found [here](https://www.masmasit.com/2021/08/how-to-install-package-libatk-10so0-on_01058658241.html). 

## Configuring Your Own AI

For an example on how to configure your own AI, you can follow the [stupid chess AI](https://github.com/game-ai-platform-team/stupid-chess-ai) project. Shell scripts that set up and run the project are placed into the Tiraconfig folder.

Your own AI is written in a Python file that the "runcommand" script calls (in the example, /src/stupid_ai.py)

### Communication with the Interface
Let's look at the structure of the example project's AI (stupid_ai.py).

```python
import random
import time
# the chess library IS NOT PREMITED in your project
import chess

def main():

    board = chess.Board()

    while True:
        opponent_move = input()
        time.sleep(random.randrange(1,10)/100)
        if opponent_move != "":
            board.push_uci(opponent_move)
        legal_moves = [move.uci() for move in list(board.legal_moves)]
        choice = random.choice(legal_moves)
        board.push_uci(choice)

        # example about logs
        print(f"I moved {choice}\n")
        # example about posting a move
        print(f"MOVE: {choice} \n")                                                                                                              

if __name__ == "__main__":
    main()
```

**Note** this example uses the ready-made Python chess library which is not allowed in your project work. You need to implement the board management and move writing yourself.

In the example, the AI communicates with the interface through input() and print statements. The input() command reads the (human-made) move from the interface in the so-called uci format. After this, a new move is saved in the AI's own board management (in the example, the command "board.push()) after which the AI calculates the next move. Our example AI simply randomly chooses one of the legal moves and returns it in another print statement. Remember that your own project work cannot use methods from the chess library.

The interface also supports logging of other inputs. All print statements except those that begin with "MOVE:" are fed into the interface output, which can be read in the terminal opened by the program. If you try to send illegal moves from your AI, the interface will crash.

### Handling Moves as Strings
The interface supports the so-called uci standard for recording chess moves as strings. Each string that describes a move has four or five characters. The first two characters of the string are the starting square of the piece to be moved. The next two are the square to which it is moved (see the picture below). The white pieces start from rows 1 and 2, black from rows 7 and 8. The white king starts at the square e1 and the white queen at d1.

The fifth character is only used for pawn promotion. The fifth character represents the piece the pawn is promoted to: q -> queen, r -> rook, b -> bishop, k -> knight.

![]({{ "https://ucichessengine.files.wordpress.com/2011/03/square_numbers.gif" | absolute_url }})

For example, the string "e2e4" represents the move of a piece currently at square e2 to square e4. The string "e7e8q" represents the promotion of a pawn currently at square e7 to a queen.

Castling is denoted by moving the king two or three squares. If you try to move a rook, this will be interpreted as a rook move.

## Thanks
Thanks to the Software Production Project Team for developing the AI platform. The entire project can be found on Github, perhaps their names will be added to this page once I ask for permission.

