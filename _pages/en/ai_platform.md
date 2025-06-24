---
layout: page
permalink: /aiplatform-en
title: AI platform
title_long: AI platform
lang: en # fi or en
ref: ai_platform
---

#### Currently Supported Features
Currently, the AI platform supports **chess** and **Connect Four**. The local version of the AI platform (which runs on your computer) works on **Linux computers** (at least on the freshman laptop).
The platform does not work on the shared disks of the university stationary computers. 

If you encounter the error message "no module called pex" while using it, you can try installing the Pex library by following [these instructions](https://pypi.org/project/pex/).
**Note:** The AI platform does not work on virtual machines. 

#### Debug information

- **24.6.2025** if running ./tira-ai-local fails with an error related to sandboxing, a workaround is to run with the command line argument --no-sandbox. This corresponds to solution number two listed [here](https://authmane512.medium.com/solve-the-suid-sandbox-helper-binary-was-found-but-is-not-configured-correctly-3-solutions-4f1425a9a76c) and works on a fuksiläppäri. Other solutions can also work but are untested. 


## AI-Platform – A Development-Supporting Framework for AIs
AI-Platform is a software project developed as a framework for course assignments, providing students with a platform to develop their game AIs. More specifically, the platform offers - with minimal setup - a graphical user interface and the ability for a human player to compete against a developing AI bot.
Setting up the platform is significantly easier than coding a GUI, so we strongly recommend it to anyone developing a chess or Connect Four AI for their assignment.
The AI platform is available on [GitHub](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file). Its README is well-written and covers the same topics as this text (in a more concise manner).
**Note:** However, the [example project](https://github.com/game-ai-platform-team/stupid-chess-ai) mentioned in the README includes an [AI](https://github.com/game-ai-platform-team/stupid-chess-ai/blob/main/src/stupid_ai.py) that uses Python’s chess library, which is **not allowed** in the course assignment.
If you use the AI platform in your assignment, **remember to mention it** in your documentation and user manual so that peer reviewers know how to run your program correctly.

## Minimal Setup Instructions
Below are minimal instructions for starting Python-based chess or Connect Four development with the AI platform on a Linux computer.
After following this section, you should be able to begin developing your course project in Python. The platform also supports other programming languages.
More details on configuring your project can be found in the section [Configuring Your Project]({% link _pages/en/ai_platform.md %}#configuring-your-project).
1. Download the [latest release ZIP file](https://github.com/game-ai-platform-team/tira-ai-local/releases) (e.g., tira-ai-local-linux-x64-1.0.4.zip).
![]({{ "/images/tira-ai1.png" | absolute_url }})
1. Clone an example AI project: [Chess](https://github.com/game-ai-platform-team/stupid-chess-ai), [Connect Four](https://github.com/game-ai-platform-team/stupid-connect-four-ai)
- Copy the contents of the cloned example AI project into your course project repository.
1. Install [Poetry]({% link _pages/en/poetry.md %}).
1. Extract the platform ZIP file, navigate to the extracted folder in the terminal, and start the platform with the command:```./tira-ai-local``` **nNote** if the command fails on an error related to sandboxing, check degub information at the top of the page. 
![]({{ "/images/tira-ai2.png" | absolute_url }})
1. Select the correct game from the top menu.
 ![]({{ "/images/tira-ai4.png" | absolute_url }})
1. Drag and drop your course project’s root folder into the box under the "submit" folder and click "Submit."
- Once Poetry is installed (you can check by running poetry -v in the terminal to ensure no errors appear), you can leave the "Run setup.sh" box unchecked.
1. Your game should start.
- Any error messages will appear in the terminal at the bottom of the screen. If issues arise, check that your project structure matches the example AIs.
- More details on project configuration requirements can be found in the section [Configuring Your Project]({% link _pages/en/ai_platform.md %}#configuring-your-project).
![]({{ "/images/tira-ai5.png" | absolute_url }})
 ![]({{ "/images/tira-ai6.png" | absolute_url }})

If you've made it this far, you can start developing your AI by modifying the file ``main.py`` (for Connect Four) or ``src/stupid_ai.py`` (for Chess).
At this point, it's a good idea to familiarize yourself with the structure of the example AIs and the [guidelines for communicating with the AI platform]({% link _pages/en/ai_platform.md %}#communication-with-the-ai-platform).
Remember that both example AIs make only random moves, so you should remove their logic and start building your AI as soon as possible.
Important: The stupid_ai.py file uses Python's chess library, which is **not allowed** in your final course project. You must implement move validation and board state management yourself!

You can (and should) modify the file names and project structure as needed. However, remember to update the scripts in the tiraconfig folders after making changes.
The "runcommand" script must contain the exact command for the AI platform to call to start your AI.
The "setup.sh" script should include installation commands for all the libraries your AI depends on.
Note: Running setup.sh is not necessary if your device already has the required libraries installed. However, you must still add the installation commands to the script so that, for example, your peer reviewers can properly run your project.

## Configuring Your Project
The AI platform supports multiple programming languages in addition to Python and Poetry. This section explains how to configure your project to work with the platform. The same instructions can be found in the [platform's README](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#ai-configuration).

In short, the AI platform expects your project's root directory to contain a folder named ``tiraconfig``, which must include at least the following two files:
``runcommand`` and ``setup.sh``.

The **setup.sh** file should contain all the commands needed to install the required libraries and dependencies for your AI.
After running setup.sh, your machine should be able to execute the command in runcommand without any additional errors.
For Python projects using Poetry, an example setup.sh might look like this:
```
#! /bin/bash

poetry install
```
The first line tells the terminal that it is a script to be executed. The second line installs Poetry.

In the **runcommand** file, you should include the exact command to start your AI from the terminal. Note that this does not necessarily have to be a Python command; you can use compiled languages as well (in this case, the setup.sh file should handle compiling your program).
When the command in runcommand is executed, your AI should start and enter an infinite loop where it reads commands from stdin and outputs its responses to stdout.
For a Python-based AI, this might look like the following example:
```python
def main():
    while True:
        # Read command from the platform
        command = input().strip()
        
        # Process the command and print responses
        # Your AI's logic goes here
        
        # For example, output a move:
        print("Your AI's move")

if __name__ == "__main__":
    main()
```
The loop is terminated by the AI platform's "kill process" button, which sends a "sigterm" signal followed by a "sigkill" signal to your program. You don't need to handle these signals. As long as you don't actively add code that prevents them, these signals will cause your program to terminate, after which you must submit it again.

## Communication with the AI Platform
Refer also to the [platform's README](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#ai-communication-protocol-input).
Your AI communicates with the platform through standard output and input.

**Input**. Each loop in your AI should begin by reading input from standard input. In Python, this can be done using the ``input()`` method. All strings sent by the platform are in the format ``COMMAND:DATA``, where ``COMMAND`` is one of the following:
- ``PLAY``: The platform wants your AI to play a move and print it to standard output.
- **Note**: Your AI may receive multiple PLAY commands consecutively, so it should be able to calculate the next move for both players. Make sure your AI knows whose turn it is and can make a move for the correct player each time it reads a ``PLAY`` command.
- ``MOVE``: The platform performed a move, and your AI should update its game logic to reflect it. Usually, this command is sent after a human has played a move through the platform. The move performed will be in the ``DATA`` part. The exact format depends on the game being played. See the game-specific formats [below]().
- ``BOARD``: Your AI's application logic should set the board to a specific configuration. The ``DATA`` part contains a string representation of the current board state. See the game-specific formats [below]({% link _pages/en/ai_platform.md %}#game-specific-instructions).
- ``RESET``: The platform wants your AI to reset the game to its initial setup.

**To use the platform**, you need to implement at least the handling of ``PLAY`` and ``MOVE`` commands in your AI. The ``BOARD`` and ``RESET`` commands are only sent if the user of the AI platform (usually yourself) either:
1. presses the reset button, or
1. tries to browse through past moves to make a different move.
 
So, as long as you don't use these features, an AI that supports only ``PLAY`` and ``MOVE`` commands can be used. However, we recommend you implement ``BOARD`` and ``RESET`` commands as soon as possible.

**Output** Your AI can print anything to standard output (e.g., using the print() method in Python). The AI platform looks for outputs in the format: ``MOVE:move``
It reads the move in the [game-specific format]({% link _pages/en/ai_platform.md %}#game-specific-instructions)) and executes it. If ``move`` does not correspond to a legal move in the given game state, the platform will crash.

Any other strings printed by your AI will be saved to the platform's terminal and shown to the user. This way, you can print logs to help with your development.

#### Example Chess AI
Let's take a closer look at the structure of the example AI project (stupid_ai.py).
```python
import random
# The use of the chess library IS NOT allowed in the project 
import chess
import time

def set_board(board: chess.Board, board_position:str):
    print(f"Set board to {board_position}!")
    board.set_fen(board_position)

def make_move(board: chess.Board):
    legal_moves = [move.uci() for move in list(board.legal_moves)]
    print(f"I found {len(legal_moves)} legal moves: {', '.join(legal_moves)}")
    choice = random.choice(legal_moves)
    board.push_uci(choice)

    return choice

def main():

    board = chess.Board()

     while True:
        opponent_move = input()
        time.sleep(random.randrange(1,10)/100)
        if opponent_move.startswith("BOARD:"):
            set_board(board, opponent_move.removeprefix("BOARD:"))
        elif opponent_move.startswith("RESET:"):
            board.reset()
            print("Board reset!")
        elif opponent_move.startswith("PLAY:"):
            choice = make_move(board)
            # example about logs
            print(f"I chose {choice}!")
            # example about posting a move
            print(f"MOVE:{choice}")
        elif opponent_move.startswith("MOVE:"):
            move = opponent_move.removeprefix("MOVE:")
            board.push_uci(move)
            print(f"Received move: {move}")
        else:
            print(f"Unknown tag: {opponent_move}")
            break

if __name__ == "__main__":
    main()
```
**Note**: this example uses Python's built-in chess library, which is **not** allowed in the assignment. Therefore, you need to implement your own board management and move generation.

In the example, the main method initializes the chessboard and starts an infinite loop. Each loop begins with the ``input()`` method, which reads the command sent by the platform. After that, all incoming commands (PLAY, MOVE, BOARD, and RESET) are executed. For example, when receiving a command that starts with the string "MOVE:" the AI first removes the prefix, and then the remainder corresponds to a move in [chess notation]({% link _pages/en/ai_platform.md %}#chess-moves). It then performs the received move. The example program sends the move information back to the platform with the command ``print(f"MOVE:{choice}")``. All other output will appear in the platform's terminal.

## Game Specific Instructions
Let's take a look at the game-specific string representations of the board states and moves.

### Chess
See also [README](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#chess)

### Chess Moves
The interface supports the UCI standard for representing chess moves as strings.
 Each move string consists of four or five characters.
 The first two characters represent the starting square of the piece being moved. The next two characters represent the square where it is moved to (see the image below). White pieces start on ranks 1 and 2, and black pieces on ranks 7 and 8. The white king starts on e1, and the white queen starts on d1.
 
The fifth character is used only for pawn promotion.
 The fifth character denotes the piece to which the pawn is promoted:
**q** -> queen, **r** -> rook, **b** -> bishop, **k** -> knight

![]({{ "https://ucichessengine.files.wordpress.com/2011/03/square_numbers.gif" | absolute_url }})

For example, the string "e2e4" represents a piece moving from e2 to e4. The string "e7e8q" represents a pawn on e7 promoting to a queen.

Castling is represented by a king's move of two or three squares. If you attempt to move a rook, it is interpreted as a rook move.

#### Chessboard
The string representing the state of the chessboard is explained [here](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#boards-fen).
For the assignment, you don't necessarily need to keep track of castling or en passant captures. However, the AI platform allows these moves, so if you make these moves through the platform as a human, you will need to account for them in the validity check.

### Connect Four
See also [readme](https://github.com/game-ai-platform-team/tira-ai-local?tab=readme-ov-file#connect-four).

####Connect Four Moves
Connect Four moves are simply represented by the column where the move is made. The leftmost column is numbered 0, and the rightmost column is numbered 6. Note that your AI needs to keep track of whose turn it is. The "Red" player makes the first move.

#### Connect Four Board
Connect Four boards are represented as a sequence of moves. After the "BOARD:" command, a series of numbers follows, separated by commas.
The first number represents the first move made by the red player, the second number represents the move made by the yellow player, and so on.

## Thanks
Thanks for the development of the AI platform go to the software project team. In the spring of 2024, it was developed by Jiahao Li, Max Leikas, Rasmus Marttila, Elijas Veijalainen, Miika Piiparinen, and Emilia Kupsanen under the guidance of Marianna Ojanen. The entire project can be found on [Github](https://github.com/game-ai-platform-team).

{% include typo_instructions_en.md %}
