🧠 Wumpus World AI Agent (Flask)
📌 Overview

This project is a Wumpus World simulation built using Flask (Python).
An intelligent agent explores a grid and avoids dangers using logical reasoning (Knowledge Base + Resolution).

🎯 Features
Custom grid size (Rows × Columns)
Random placement of:
🕳️ Pits
👹 Wumpus
Intelligent agent:
Detects Breeze and Stench
Uses logical inference
Step-by-step simulation
Web-based interface
🧩 Concepts Used
Artificial Intelligence (AI)
Knowledge-Based Agents
Propositional Logic
Resolution Algorithm
Flask
🗂️ Project Structure
project/
│── app.py
│── templates/
│    └── index.html
│── static/ (optional)
⚙️ Installation & Setup
1. Clone Repository
git clone <your-repo-link>
cd project
2. Install Dependencies
pip install flask
3. Run the App
python app.py
4. Open in Browser
http://127.0.0.1:5000/
🎮 How It Works
Start Episode
User selects:
Grid size
Number of pits
Agent Behavior
Starts at (0,0)
Percepts:
Breeze → Pit nearby
Stench → Wumpus nearby
Decision Making

Agent uses:

Knowledge Base (KB)
Resolution algorithm

To:

Infer safe cells
Avoid danger
Move step-by-step
🧠 Knowledge Representation
P_r_c → Pit at (r,c)
W_r_c → Wumpus at (r,c)
!P_r_c → No pit
!W_r_c → No Wumpus
🔍 Inference Rules
No Breeze → No pits nearby
Breeze → At least one pit nearby
No Stench → No Wumpus nearby
Stench → Wumpus nearby
🚀 API Endpoints
POST /start

Start a new game

Request:

{
  "rows": 4,
  "cols": 4,
  "pits": 3
}
POST /step

Move agent one step

GET /

Load UI

📊 Cell States
unknown
safe
danger
inferred
🛡️ Safety Logic

Agent moves only if:

Proven safe OR
Logically inferred safe

Otherwise:

❌ Stops
❌ Termination Conditions
Falls into pit → Game Over
Meets Wumpus → Game Over
No safe moves → Stops
📈 Output Includes
Agent position
Percepts
Moves count
Inference steps
