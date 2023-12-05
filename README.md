# Implementation Of Baroque Chess

## Overview
This repository contains a Python implementation of a Baroque Chess agent using the python-chess library. The Baroque Chess agent employs a simple evaluation function and the alpha-beta pruning algorithm to make strategic moves.

### Table of Contents
[Introduction](#Introduction)

[Usage](#Usage)

[Baroque Chess Rules](#Baroque-Chess-Rules)

[Agent Implementation](#Agent-Implementation)

[Alpha-Beta Pruning](#Alpha--Beta-Pruning)

[Evaluation Function](#Evaluation-Function)

### Introduction

Baroque Chess is a variant of chess that introduces unconventional pieces and changes to the standard chess rules. This project implements a Baroque Chess agent with a basic evaluation function and the alpha-beta pruning algorithm to make optimal moves.

### Usage
To use the Baroque Chess agent, follow these steps:
1. Install the required Python library:
   <pre>
     pip install python-chess
   </pre>
   
2. **Initialization:**
   <pre>
      agent = BaroqueChessAgent(depth=3)
      </pre>

- Initialize the BaroqueChessAgent with a specified search depth.

3. **Manual Setup:**
<pre>
initial_position = "rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1"
board = chess.Board(initial_position)
   
   </pre>
   
- Set up the Baroque Chess board with the desired initial position

 4. **Example Usage**
   <pre>
      while not board.is_game_over():
          legal_moves = list(board.legal_moves)
          if not legal_moves:
              print("No legal moves. Game over.")
              break

          move = agent.get_best_move(board)
          print(f"Move: {board.san(move)}")
          board.push(move)

          print("Current Position:")
          print(board)

          #Check for a draw
          if board.is_variant_draw():
          print("Game is a draw.")
          break
        
   </pre>
- Execute the example script to witness the agent's strategic decisions.
   

### Baroque Chess Rules
Baroque Chess introduces unique pieces and changes to the standard chess rules. Familiarize yourself with the Baroque Chess rules to understand the game dynamics with the reference [About Baroque Chess](https://en.wikipedia.org/wiki/Baroque_chess)


### Agent Implementation
The BaroqueChessAgent class implements the Baroque Chess agent. It includes methods for evaluating the board, performing alpha-beta pruning, and determining the best move.


### Alpha-Beta Pruning
The agent utilizes the Alpha-Beta Pruning algorithm to optimize the minimax search, efficiently exploring the game tree and reducing the number of evaluated positions.

<pre>
def alpha_beta_pruning(self, board, depth, alpha, beta, maximizing_player):
   
    if depth == 0 or board.is_game_over():
        return self.evaluate_board(board)

    legal_moves = list(board.legal_moves)
    if maximizing_player:
        max_eval = float('-inf')
        for move in legal_moves:
            board.push(move)
            eval = self.alpha_beta_pruning(board, depth - 1, alpha, beta, False)
            board.pop()
            max_eval = max(max_eval, eval)
            alpha = max(alpha, eval)
            if beta <= alpha:
                break
        return max_eval
    else:
        min_eval = float('inf')
        for move in legal_moves:
            board.push(move)
            eval = self.alpha_beta_pruning(board, depth - 1, alpha, beta, True)
            board.pop()
            min_eval = min(min_eval, eval)
            beta = min(beta, eval)
            if beta <= alpha:
                break
        return min_eval
               </pre>
               
**Description:**

This method recursively implements the Alpha-Beta Pruning algorithm for decision-making during gameplay. It evaluates possible moves on the chess board, minimizing the number of positions evaluated to improve performance.

**Parameters:**

-**'board'** (chess.Board): The current state of the chess board.

-**'depth'** (int): The depth of the search tree.

-**'alpha'** (float): The best value that the maximizing player currently can guarantee.

-**'beta'** (float): The best value that the minimizing player currently can guarantee.

-**'maximizing_player'** (bool): Indicates whether the current player is maximizing or minimizing.

**Returns:**

**'-float'**: The evaluated score of the board.

### Evaluation Function
The evaluation function assigns values to pieces and calculates a board score based on the current piece configuration. Feel free to enhance this function for more sophisticated evaluations.

**evaluate_board method:**
<pre>
   def evaluate_board(self, board):
    """
    Evaluates the current chess board using a simple evaluation function.

    Parameters:
    - board (chess.Board): The chess board to evaluate.

    Returns:
    - float: The evaluated score of the board.
    """
    piece_values = {
        chess.PAWN: 1,
        chess.KNIGHT: 3,
        chess.BISHOP: 3,
        chess.ROOK: 5,
        chess.QUEEN: 9,
        chess.KING: 0,
    }
    return board.turn * sum(piece_values[piece.piece_type] for piece in board.piece_map().values())

</pre>

**Parameters:**

**-board** (chess.Board): The chess board to evaluate.

**Returns:**

**-float**: The evaluated score of the board.

### Customization

Feel free to enhance the evaluation function or experiment with different search depths to tailor the agent's behavior to your preferences.


### Output 
