# Sunfish - A Lightweight Python Chess Engine

Sunfish is a simple yet effective chess engine written in pure Python. It's designed with clarity and minimalism in mind, making it one of the best engines to study and understand the inner workings of chess engines. Despite its simplicity, it implements powerful techniques such as alpha-beta pruning, positional evaluation, and efficient board representation.

## Table of Contents

- [About the Project](#about-the-project)
- [Core Concepts](#core-concepts)
- [Evaluation Function](#evaluation-function)
- [Board Representation](#board-representation)
- [Move Generation](#move-generation)
- [Search Algorithm](#search-algorithm)
- [Engine Architecture](#engine-architecture)
- [How to Run](#how-to-run)
- [Sample Game Interaction](#sample-game-interaction)
- [Understanding the Output](#understanding-the-output)
- [Performance](#performance)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Learning Resources](#learning-resources)
- [License](#license)
- [Credits](#credits)

---

## About the Project

Sunfish was originally created to demonstrate the basics of a chess engine in under 500 lines of Python. It is capable of playing legal chess moves, performing search and evaluation, and generating reasonable responses against human players.

This version is an enhanced and annotated version of the original engine, intended for learning and experimenting. It is an excellent choice for:

- Students learning about AI and game theory
- Developers curious about chess engine design
- Hobbyists looking to build their own chess bot

---

## Core Concepts

### 1. Board Representation

Sunfish uses a *120-square board* (a technique also used in professional engines like Stockfish). It pads an 8×8 board inside a 10×12 grid, allowing easy detection of off-board moves.

- Legal board indices: 21 to 98 (excluding border)
- Each square contains a piece code (e.g., 'P', 'k', '.')
- Pieces are represented as single characters:
  - Uppercase = White ('P', 'N', 'B', 'R', 'Q', 'K')
  - Lowercase = Black ('p', 'n', 'b', 'r', 'q', 'k')

### 2. Positional Evaluation

Each piece has a *base value*:
- Pawn: 100
- Knight: 300
- Bishop: 320
- Rook: 500
- Queen: 900
- King: 20000 (arbitrary high for game-end conditions)

Each piece also receives a *positional bonus* using piece-square tables (PSTs), which give extra weight to central control, safety, or promotion potential.

### 3. Move Generation

Legal moves are generated using pre-defined directions and offsets:
- Pawns can move forward or capture diagonally
- Sliding pieces (bishop, rook, queen) repeat steps in a direction until blocked
- Special moves like castling and en-passant may be added manually

---

## Evaluation Function

The engine evaluates positions based on:
- *Material Balance:* Sum of the values of all remaining pieces
- *Positional Bonuses:* Piece-square table values based on the piece’s location
- *Turn Modifier:* Positive score for white, negative for black

This makes the engine prefer development, central control, and mobility.

Example:
```python
score = material_score + positional_bonus
if not white_to_move:
    score = -score
