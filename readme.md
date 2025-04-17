# ♟️ Sunfish Chess Engine – Project Presentation 

## 📌 Introduction

**Sunfish** is a minimalist yet powerful chess engine written in under 150 lines of Python. Despite its simplicity, it achieves a playing strength of over **2000 ELO** on Lichess and provides an excellent platform for learning and experimenting with chess engine internals.

---

## 🧠 1. What is Sunfish?

Sunfish stands out due to:
- **Compact design**: ~131 lines of Python code.
- **Educational value**: Great for learning AI search algorithms and evaluation functions.
- **Experimentation**: Used in testing neural nets, parallel search, and engine optimization.

---

## ⚙️ 2. How Does It Work?

- **Search Algorithm**: Uses the *MTD-bi* (Memory-enhanced Test Driver with zero-width window) algorithm, also called **NegaC\***.
- **Evaluation Function**: Based on **Piece-Square Tables**, assigning scores to pieces based on their position.
- **Data Structures**: Uses simple Python lists and dictionaries for board representation and move generation.
-It is basically chess game. you need to enter your move(ex: e5/d3). After that computer play with you as your opponent.

## 🧪 3. Playing Strength
- **Strengths**: Efficient positional play due to PST-based evaluation.
- **Weaknesses**: Limited tactical depth and no advanced pruning technique.

