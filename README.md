Wumpus World AI Agent (Flask)
📌 Overview

This project is a Wumpus World simulation implemented using Flask (Python).
An intelligent agent explores a grid environment while avoiding hidden dangers using logical reasoning (Knowledge Base + Resolution).

🎯 Features
Grid-based environment (custom size)
Random placement of:
🕳️ Pits
👹 Wumpus
Intelligent agent with:
Perception (Breeze, Stench)
Logical inference using Resolution
Step-by-step simulation
Web-based interface (Flask)
🧩 Concepts Used
Artificial Intelligence (AI)
Knowledge-Based Agents
Propositional Logic
Resolution Algorithm
Flask Web Development
🗂️ Project Structure
project/
│── app.py
│── templates/
│    └── index.html
│── static/ (optional)
⚙️ Installation & Setup
1. Clone or Download
git clone <your-repo-link>
cd project
2. Install Dependencies
pip install flask
3. Run the Application
python app.py
4. Open in Browser
http://127.0.0.1:5000/
🎮 How It Works
1. Start Episode
User selects:
Grid size (Rows × Columns)
Number of pits
2. Agent Behavior
Starts at (0,0)
Observes:
Breeze → Pit nearby
Stench → Wumpus nearby
3. Decision Making

Agent uses:

Knowledge Base (KB)
Resolution algorithm

To:

Infer safe cells
Avoid dangerous cells
Move step-by-step
🧠 Knowledge Representation

Each cell is represented using literals:

P_r_c → Pit at (r,c)
W_r_c → Wumpus at (r,c)
!P_r_c → No pit
!W_r_c → No Wumpus
🔍 Inference Rules
No Breeze → No pit in neighbors
Breeze → At least one neighbor has a pit
No Stench → No Wumpus nearby
Stench → Wumpus in one neighbor
🚀 API Endpoints
/start (POST)

Starts a new game

Input:

{
  "rows": 4,
  "cols": 4,
  "pits": 3
}
/step (POST)

Moves agent one step forward

/

Loads the UI

📊 Game States

Each cell can be:

unknown
safe
danger
inferred
🛡️ Safety Logic
Agent never moves randomly
Moves only if:
Proven safe OR
Inferred safe

If no safe move:

❌ Agent stops
📈 Outputs
Agent position
Percepts (Breeze, Stench)
Moves count
Inference steps
Game status
❌ Termination Conditions
Agent falls into pit → Game Over
Agent meets Wumpus → Game Over
No safe moves → Agent halts
💡 Example
Agent at (1,2)
Percepts: Breeze, Stench
🔮 Future Improvements
Add shooting arrow to kill Wumpus
Add scoring system
Improve UI visualization
Add manual control mode
