# 🧭 Wumpus World — Logic-Based AI Agent

A Flask-based simulation of the classic **Wumpus World** problem, where an AI agent navigates a grid using **propositional logic** and **resolution-based inference** to avoid pits and the Wumpus.

---

## 🗺️ What Is Wumpus World?

Wumpus World is a benchmark environment for knowledge-based AI agents. The agent explores an unknown grid that contains:

- **Wumpus** — a monster that kills the agent on contact
- **Pits** — bottomless holes that kill the agent on contact
- **Percepts** — indirect clues the agent uses to reason about danger:
  - `Breeze` — a pit is in an adjacent cell
  - `Stench` — the Wumpus is in an adjacent cell

The agent must use logical inference to determine which cells are safe to visit.

---

## ✨ Features

- Configurable grid size and number of pits
- Propositional logic **Knowledge Base (KB)** built in real time as the agent explores
- **Resolution-based theorem proving** to verify cell safety before moving
- Step-by-step agent movement via a REST API
- Cell state tracking: `unknown`, `inferred` (safe), `safe` (visited), `danger`
- Inference step counter and move tracker

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Flask

### Installation

```bash
git clone https://github.com/your-username/wumpus-world.git
cd wumpus-world
pip install flask
```

### Running the App

```bash
python app.py
```

The server starts at `http://127.0.0.1:5000` by default.

---

## 📡 API Reference

### `POST /start`

Initializes a new episode.

**Request Body (JSON):**

| Field  | Type | Default | Description              |
|--------|------|---------|--------------------------|
| `rows` | int  | `4`     | Number of grid rows (min 3) |
| `cols` | int  | `4`     | Number of grid columns (min 3) |
| `pits` | int  | `3`     | Number of pits to place  |

**Example:**
```json
{ "rows": 4, "cols": 4, "pits": 3 }
```

---

### `POST /step`

Advances the agent by one move using the KB to pick a safe cell.

**No request body required.**

---

### Response Schema

Both endpoints return:

```json
{
  "R": 4,
  "C": 4,
  "agent": [0, 1],
  "alive": true,
  "running": true,
  "cell_states": { "0,0": "safe", "0,1": "inferred", ... },
  "visited": [[0, 0]],
  "percepts": ["Breeze"],
  "inference_steps": 12,
  "moves": 1,
  "status": "Agent at (0,1). Percepts: Breeze",
  "pits": [],
  "wumpus": null
}
```

> **Note:** `pits` and `wumpus` are only revealed in the response once the agent has entered a danger cell (game over).

---

## 🧠 How the Agent Thinks

1. **Perceive** — On entering a cell, the agent checks for `Breeze` and `Stench`.
2. **Tell** — The KB is updated with clauses derived from the percepts (e.g., no breeze → no pit in any neighbor).
3. **Ask** — Before moving to an unvisited neighbor, the agent queries the KB using resolution to prove `¬Pit` and `¬Wumpus`.
4. **Move** — The agent prioritizes:
   - Already-inferred safe neighbors
   - Provably safe unvisited neighbors
   - Halts if no safe move can be proven

---

## 📁 Project Structure

```
wumpus-world/
├── app.py          # Main Flask application & all game logic
└── templates/
    └── index.html  # Frontend UI (connect your own or use the API directly)
```

---

## ⚙️ Configuration Notes

- The agent always starts at cell `(0, 0)`, which is guaranteed safe.
- The Wumpus and pits are never placed at `(0, 0)`.
- Grid minimum is `3×3`.
- The resolution prover caps clause count at **800** to prevent runaway inference.


