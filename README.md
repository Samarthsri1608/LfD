# 🤖 Learning from Demonstration (LfD) for Robots

This repository contains the implementation of a **Learning from Demonstration (LfD)** pipeline for robots, developed as part of a research project exploring how robots can **learn new skills by observing human demonstrations** instead of being explicitly programmed.

The system integrates **ROS 2**, **Gazebo**, and **PyTorch** to enable **end-to-end imitation learning**, mapping **visual and proprioceptive inputs** to **robot control actions**.

---

## 🧩 Project Overview

**Learning from Demonstration (LfD)** is a core technique in robot learning that allows autonomous agents to acquire new behaviors from expert demonstrations.  
This project implements and compares multiple imitation learning approaches:

- **Behavior Cloning (BC)** – supervised imitation using state–action pairs.  
- **Inverse Reinforcement Learning (IRL)** – recovering the reward function driving expert actions.  
- **Generative Adversarial Imitation Learning (GAIL)** – learning via adversarial expert–learner interaction.

The objective is to evaluate how effectively robots can **generalize learned behaviors** to **unseen environments**, improving adaptability and collaboration in human–robot systems.

---

## ⚙️ System Architecture

Human Demonstration (Teleoperation / Simulation)
│
▼
Data Collection (ROS 2)
│
▼
Trajectory + Visual Feature Extraction
│
▼
Policy Learning (PyTorch)
│
▼
Policy Deployment (ROS 2 + Gazebo)
│
▼
Evaluation & Generalization Tests


---

## 🧠 Key Components

| Component | Description |
|------------|-------------|
| **ROS 2 (Humble/Foxy)** | Middleware for robotic communication and control |
| **Gazebo / Ignition** | 3D simulator for collecting demonstrations and testing learned policies |
| **PyTorch** | Deep learning framework for training imitation models |
| **OpenAI Gym / RL Bench (optional)** | For standardized task environments |
| **Teleop Node** | Interface for human-controlled demonstrations |

---

## 🧪 Features

✅ End-to-end LfD pipeline (from demonstration to autonomous execution)  
✅ Integration of ROS 2 nodes with PyTorch models  
✅ Support for Behavior Cloning, IRL, and GAIL  
✅ Real-time data collection from teleoperation or simulation  
✅ Evaluation metrics: success rate, imitation accuracy, generalization  
✅ Modular and reproducible design for research and extensions  

---

## 🧰 Installation

### Prerequisites
- **Ubuntu 22.04 / 24.04**
- **ROS 2 (Humble or newer)**
- **Gazebo / Ignition Fortress or Harmonic**
- **Python 3.10+**
- **PyTorch ≥ 2.0**
- **Colcon build tools**

### Setup Instructions
```bash
# Clone repository
git clone https://github.com/Samarthsri1608/LfD.git
cd LfD

# Setup workspace
mkdir -p ~/lfd_ws/src
mv * ~/lfd_ws/src/
cd ~/lfd_ws

# Install dependencies
rosdep install --from-paths src --ignore-src -r -y
pip install -r src/requirements.txt

# Build the workspace
colcon build
source install/setup.bash

```
---

## 🎮 Usage
1. Run Gazebo Simulation
ros2 launch lfd_sim simulation.launch.py

2. Record Human Demonstrations
ros2 run lfd_demo record_demo --output demo_data/

3. Train Imitation Policy
python train_policy.py --method behavior_cloning --data demo_data/

4. Deploy Learned Policy
ros2 run lfd_policy execute_policy --model checkpoints/bc_model.pth


## Evaluation Metrics

Task Success Rate (SR) – Percentage of successful task completions

Mean Squared Error (MSE) – Between predicted and expert trajectories

Imitation Accuracy (IA) – Similarity score between action distributions

Generalization Index (GI) – Performance on unseen initial states

## Directory Structure
LfD/
├── lfd_demo/                 # ROS 2 package for demonstration collection
├── lfd_policy/               # ROS 2 package for policy deployment
├── lfd_training/             # Training scripts for BC, IRL, GAIL
├── models/                   # Pretrained models
├── launch/                   # Simulation and execution launch files
├── demo_data/                # Sample trajectories (optional)
├── docs/                     # Research documentation
├── requirements.txt
└── README.md

## 🧩 Research Objectives

Develop a reproducible LfD pipeline in ROS 2 + Gazebo

Integrate deep imitation learning models in PyTorch

Quantitatively evaluate learned behaviors across tasks

Contribute an open-source framework for future LfD research

## 📚 Citation

If you use this repository in your research, please cite:

@article{Samarth2025lfd,
  title   = {Learning from Demonstration for Robots: An End-to-End Imitation Learning Pipeline in ROS 2 and Gazebo},
  author  = {Samarth Srivastava},
  year    = {2025},
  journal = {Unpublished Research Project / GitHub Repository}
}

## 📜 License

This project is licensed under the MIT License — see the LICENSE file for details.

## 🙌 Acknowledgements

This project is inspired by:

OpenAI’s Imitation Learning Benchmarks

Stanford’s CS 287: Advanced Robotics course materials

The ROS 2 + Gazebo simulation ecosystem

Researchers in LfD, IRL, and GAIL for foundational work in robot imitation learning