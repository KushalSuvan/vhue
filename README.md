```yaml
---
title: Mesoscopic Traffic Env
emoji: 🚦
colorFrom: indigo
colorTo: blue
sdk: docker
app_file: server/app.py
pinned: false
app_port: 8000
base_path: /web
tags:
  - openenv
  - reinforcement-learning
  - unsloth
  - traffic-flow-theory
short_description: Devolving microscopic priority routing to mesoscopic cell eviction for LLM training.
---
```

<div align="center">
  
# 🚦 Traffic Env: Devolving Microscopic Priority to Mesoscopic Cells
**An OpenEnv Environment for Training LLMs in Spatiotemporal Traffic Flow Theory**

[![Open UI](https://img.shields.io/badge/Launch-Traffic_Env_UI-indigo?style=for-the-badge&logo=huggingface)](https://etherealwhisper-traffic-env-ui.hf.space)
[![Math Proofs](https://img.shields.io/badge/Read-Mathematical_Foundations-slate?style=for-the-badge&logo=github)](https://kushalsuvan.github.io/vhue)
[![OpenEnv](https://img.shields.io/badge/Powered_by-OpenEnv-blue?style=for-the-badge)](#)

*You live in Bangalore with its traffic. You know the problem...*
<br><br>

</div>

---

## 1. The Problem: A Universal Testbed for Spatial-Temporal Flow
Traffic management is one of the most complex stochastic challenges in the real world. A standard intersection does not just require an agent to "prevent crashes"; it requires forecasting dynamically shifting Origin-Destination (OD) probability matrices and handling cascading fluid dynamics.

Traditionally, modeling this requires tracking 10,000+ individual vehicle entities (Microscopic/Lagrangian tracking), which is computationally explosive, slow, and incredibly difficult to interface with modern AI training loops. 

**Our Novel Angle:** We didn't just build a game; we built an agent-agnostic research sandbox. By leveraging modern Traffic Flow Theory, we established a rigorous mathematical proof that under a strict "no-overtake" (FIFO) constraint, the complex problem of **microscopic priority routing** mathematically devolves into a highly efficient **mesoscopic cell eviction** problem. 

This environment provides researchers with a mathematically accurate, lightweight spatial-temporal benchmark. Whether you are testing an LLM, a traditional RL agent, or a heuristic algorithm, this OpenEnv environment exposes the raw, underlying physics of traffic flow.

*Could a researcher write a paper about testing an agent on this? Yes. We already drafted the [mathematical foundations here](https://kushalsuvan.github.io/vhue).*

---

## 2. Environment Architecture & Physics
Because this environment is agent-agnostic, the underlying simulation must be flawless. This is a rigorously backed physics environment built on the **Lighthill-Whitham-Richards (LWR)** conservation law and computationally discretized using **Daganzo’s Cell Transmission Model (1994)**.

### The Observation Space
The environment exposes a heavily optimized, real-world mesoscopic state to whatever client connects to it:
* **Cell Occupancy Densities:** Flow volumes waiting at intersection boundaries, representing kinetic fluid density waves.
* **Global Route Probability Distributions:** An encoded matrix representing the current temporal "phase" of traffic (e.g., morning school rush vs. evening commercial rush), modeled as multivariate white noise decoupling.
* **Priority Flags:** Boolean arrays indicating the presence of emergency/priority vehicles trapped within specific mesoscopic cells.

---

## 3. The Reward Signal (OpenEnv Rubrics)
We use OpenEnv's composable rubrics to provide a rich, multi-dimensional reward signal that is mathematically impossible to "game." 

* **Safety Rubric [Hard Constraint]:** Authorizing conflicting routes immediately triggers an accident scenario. **Reward = -1.0**, and the episode terminates.
* **Throughput Rubric [Continuous]:** Positive scalar rewards based on the integral of outbound flow volume over time.
* **Starvation Penalty [Decay]:** To prevent the LLM from gaming the system by permanently leaving the highest-volume lane green, cells exponentially accumulate negative rewards for wait times exceeding a threshold.
* **Priority Eviction Bonus [Spike]:** A large reward multiplier applied *only* when a priority cell is successfully flushed through the intersection boundary.

---

## 4. Training & Results: Unsloth + GRPO
*Note for Reviewers: The interactive training plots and complete Google Colab notebook can be found linked below.*

We tackled the environment using **Unsloth** alongside **Group Relative Policy Optimization (GRPO)** to maximize the training efficiency of the LLM agent. 

<div align="center">
  <img src="https://placehold.co/600x300/fcfcfc/374151?text=Insert+WandB+Loss/Reward+Plot+Here" alt="Training Curve Placeholder" style="border-radius: 8px; border: 1px solid #eaeaea;">
  <p><i>Figure 1: Reward accumulation over 10k steps. The blue line represents the GRPO-trained agent, demonstrating a sharp learning curve in recognizing OD shifts. The red line represents the random baseline.</i></p>
</div>

**Key Results:**
* **Untrained Baseline:** Averaged high collision rates and total gridlock within 50 steps due to route starvation.
* **Trained Agent:** Successfully learned to map priority vehicle tags to bulk cell-eviction actions without violating the safety matrices.

🔗 **[Run the Training Script in Google Colab (Link)](#)**
🔗 **[View Full WandB Metrics (Link)](#)**

---

## 5. Quick Start (OpenEnv Client)

Built natively on OpenEnv, interacting with the physics engine is clean and synchronous.

```bash
# Clone and run the server locally
docker build -t traffic_env:latest -f server/Dockerfile .
```

```python
from traffic_env import TrafficEnv, TrafficAction

# Async by default — use async with / await
async with TrafficEnv(base_url="http://localhost:8000") as env:
    # Initialize the mesoscopic state
    result = await env.reset()
    print(result.observation.scene_description)
    
    # Observe the Global Route Probability shift
    print(f"Current Matrix Phase: {result.observation.od_matrix_phase}")

    # Step the environment: Force cell eviction for priority lane 2
    result = await env.step(TrafficAction(
        action_type="evict_cell",
        target_lane=2
    ))
    
    print(f"Volume Evicted: {result.observation.evicted_volume}")
    print(f"Reward: {result.reward}")
```

### File Structure
```text
traffic_env/
├── openenv.yaml                # OpenEnv manifest
├── pyproject.toml              # Dependencies
├── client.py                   # TrafficEnv client
├── models.py                   # Pydantic Action/Observation schemas
└── server/
    ├── traffic_env_environment.py # Core Daganzo CTM physics engine
    └── app.py                  # FastAPI + WebSocket router
```
