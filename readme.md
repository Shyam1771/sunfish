https://drive.google.com/file/d/18IXcpEuvuynxpK-X20gjWy4TZsL2TQ77/view?usp=drive_link
## How the Engine Decides Its Next Move

The core logic of Sunfish revolves around simulating future moves and evaluating the resulting positions to find the best move. This is done using the *Minimax algorithm with Alpha-Beta Pruning*.

### Step-by-Step Logic of Finding the Best Move

---

### 1. *Move Generation*
Sunfish first generates all pseudo-legal moves available to the current player. This includes:
- Normal piece movements
- Captures
- Pawn promotions

Note: Special rules like castling or en-passant are typically not included in the base version.

---

### 2. *Simulation of Each Move*
For every generated move:
- The engine simulates the move by creating a new position with that move applied.
- This new position becomes the input for the next step in the decision tree.

---

### 3. *Recursive Evaluation (Minimax)*
The engine calls the search function recursively to evaluate each resulting position:

- If it's the engine’s turn again (after the opponent moves), it tries to *maximize* the score.
- If it's the opponent's turn, the engine tries to *minimize* the score.

This recursion continues until a certain depth is reached (e.g., 3 or 4 plies), after which a static evaluation is performed.

---

### 4. *Static Evaluation*
At the deepest level of recursion (leaf nodes), the engine evaluates the board using the following:
- *Material Score*: Total value of pieces on board (e.g., pawn=100, queen=900).
- *Positional Bonus*: Values from piece-square tables (PSTs), giving extra score for:
  - Central control
  - Advanced pawns
  - Knight outposts
  - King safety, etc.

This combined score reflects how "good" a position is for the current player.

---

### 5. *Alpha-Beta Pruning*
To make the engine efficient:
- If one move already proves to be worse than a previously evaluated option, it stops checking further (prunes the branch).
- This prevents the engine from evaluating every possible outcome and saves computation.

---

### 6. *Select the Best Move*
When all moves have been evaluated:
- The engine picks the move with the *highest score* if it's its own turn.
- Or the move that results in the *lowest score* for the opponent.

This move is returned as the *best move* to play.

---

## 7. *How Evaluation Score Is Calculated*

The evaluation score in the Sunfish engine helps determine how good or bad a position is for the current player. This score is a combination of *material value* and *positional bonuses*. Here’s a breakdown of how the evaluation is calculated:

---

### 8. *Material Score*

Each piece is assigned a numerical value, commonly used in chess engines:

| Piece  | Symbol | Value  |
|--------|--------|--------|
| Pawn   | 'P'    | 100    |
| Knight | 'N'    | 300    |
| Bishop | 'B'    | 325    |
| Rook   | 'R'    | 500    |
| Queen  | 'Q'    | 900    |
| King   | 'K'    | 0 (not counted) |

- For example, a position with 2 white pawns, 1 white rook, and 1 black queen would score:
  - White: 2×100 + 500 = *700*
  - Black: 900
  - Final score = *700 - 900 = -200* (white is losing by 200)

---

### 9. *Positional Bonus (Piece-Square Tables)*

For each piece type, a *Piece-Square Table (PST)* is used. This is an 8×8 grid that assigns a small bonus or penalty to each square on the board.

- These tables reward:
  - Pawns that are advanced or on central files
  - Knights in the center
  - Bishops on long diagonals
  - Rooks on open files
  - King safety (castled, away from center)

*Example (Pawns)*:  
The pawn PST gives higher values to central and advanced squares:
