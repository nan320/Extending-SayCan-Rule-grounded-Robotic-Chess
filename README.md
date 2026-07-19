# 🤖 SayCan Robotic Chess

**SayCan probability fusion for rule-grounded robotic chess in PyBullet.**

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PyBullet](https://img.shields.io/badge/PyBullet-3.2.6-green.svg)](https://pybullet.org)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o--mini-orange.svg)](https://platform.openai.com/)

Complete implementation of **Score(a) = p(Say) × p(Can)** for a simulated chess-playing robot.

- **p(Say)**: Strategic preference from Deepseek/Chatgpt log-probabilities over legal move menus
- **p(Can)**: Geometric feasibility proxy (IK solvability + workspace bounds + travel distance)
- **Validation**: python-chess ensures every move is FIDE-legal before execution
- **Simulation**: PyBullet with UR5e 6-DOF arm and Robotiq 2F-85 gripper

📄 **Project Report**: See [SayCan_Robotic_Chess_Report.pdf](https://github.com/your-username/saycan-robotic-chess/blob/main/report.pdf)

🎥 **Demo Video**: [Watch on YouTube](https://youtu.be/your-video-link)

---

## 📊 Example Output
Turn 1 (Black to move):

Top SayCan candidates:

Pick the black Pawn 5 and place it on the e5
p(Say)=0.959, p(Can)=0.761, Score=0.730 ✅ SELECTED

Pick the black Pawn 4 and place it on the d5
p(Say)=0.029, p(Can)=0.761, Score=0.022

Pick the black Pawn 6 and place it on the f5
p(Say)=0.011, p(Can)=0.761, Score=0.008

Executed: Pick the black Pawn 5 and place it on the e5

text

---

## 🏗️ System Architecture
Current Chess State (FEN)
↓
LLM Menu Prompt (A, B, C, ...)
↓
p(Say) from Token Log-Probs (Softmax)
↓
p(Can) from Geometric Feasibility
↓
Score = p(Say) × p(Can)
↓
Best Candidate (argmax Score)
↓
python-chess Validation
↓
PyBullet Execution (UR5e + Gripper)

text

---

## 🚀 Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/your-username/saycan-robotic-chess.git
cd saycan-robotic-chess
2. Install dependencies
bash
pip install -r requirements.txt
3. Download asset files
Place the following folders in the project root:

assets/ur5e/ — UR5e robot model

assets/robotiq_2f_85/ — Robotiq gripper model

assets/chess_set/ — Chess piece models

4. Set up OpenAI API key
python
import openai
openai.api_key = "your-api-key-here"
5. Run the notebook
bash
jupyter notebook MLProject5.ipynb
Then execute all cells, or run:

python
from src.saycan_scorer import run_saycan_chess

# Run 20 turns of chess with SayCan probability fusion
env, chess_board, piece_positions, feedback = run_saycan_chess(num_turns=20)
📁 Project Structure
text
saycan-robotic-chess/
├── MLProject5.ipynb          # Main implementation notebook
├── README.md                 # This file
├── requirements.txt          # Python dependencies
├── LICENSE                   # MIT License
├── assets/                   # URDF models
│   ├── ur5e/
│   ├── robotiq_2f_85/
│   └── chess_set/
└── videos/                   # Demo videos
    ├── debug_video.mp4
    └── full_simulation.mp4
🔬 Methods Used vs Not Used
Component	Status	Role
PyBullet + UR5e + Robotiq	✅ Used	Physics simulation, IK, motion planning
python-chess	✅ Used	FEN state, legal moves, game termination
OpenAI GPT-4o-mini (logprobs)	✅ Used	p(Say) extraction from token probabilities
Geometric p(Can)	✅ Used	IK feasibility + workspace bounds + distance
SayCan Score Fusion	✅ Used	p(Say) × p(Can) ranking
ViLD / YOLO	❌ Not Used	Project uses known simulator poses
CLIPort Training	❌ Not Used	All policies are scripted
LLM Fine-tuning	❌ Not Used	Inference only (consistent with project brief)
📈 Evaluation Metrics
Metric	Result
Legal Move Rate (after validation)	100%
IK Solvability Rate	95.6%
Task Completion (20 turns)	100%
📚 References
SayCan Original Paper: Ahn, M., Brohan, A., Brown, N., et al. "Do As I Can, Not As I Say: Grounding Language in Robotic Affordances." CoRL 2022. arXiv:2204.01691

python-chess: Fiekas, N. https://github.com/niklasf/python-chess

PyBullet: Coumans, E. and Bai, Y. http://pybullet.org

UR5e: Universal Robots. https://www.universal-robots.com/products/ur5e/

Robotiq 2F-85: Robotiq. https://robotiq.com/products/2f-85-adaptive-gripper

🤝 Authors
Name	Affiliation
Nan Wang	Politecnico di Milano
Shiyuan Liu	Politecnico di Milano
Tingyu Chen	Politecnico di Milano
Jintao Ma	Université Paris-Saclay
Course: Machine Learning For Mechanical System, Politecnico di Milano, 2025

📄 License
MIT License — see LICENSE for details.

🙏 Acknowledgments
Course instructors: A. Moroncelli and L. Roveda, Politecnico di Milano

LEON Group for foundational robotics and LLM course materials

🔗 Links

🎥 Demo Video
https://youtube.com/shorts/CpGgXjuBb8E?si=Al9Ur2BMkbvfTiN6


📧 Contact: {nan.wang, shiyuan.liu, tingyu.chen}@polimi.it
