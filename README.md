<div align="center">
  
# 🚦 Traffic Env: Devolving Microscopic Priority to Mesoscopic Cells
**An OpenEnv Environment with Spatiotemporal Traffic Flow Emulation**

[![Open UI](https://img.shields.io/badge/Launch-Traffic_Env_UI-indigo?style=for-the-badge&logo=huggingface)](https://etherealwhisper-traffic-env-ui.hf.space)
[![Math Proofs](https://img.shields.io/badge/Read-Mathematical_Foundations-slate?style=for-the-badge&logo=github)](https://kushalsuvan.github.io/vhue)
[![Colab Training](https://img.shields.io/badge/Run-Colab_Training_Script-orange?style=for-the-badge&logo=googlecolab)](https://colab.research.google.com/drive/1TMq_qdFoHaiauP6KtKoWYse9n33RYw3x?usp=sharing)

> **🚨 NOTE FOR JUDGES: Please use the badges above for direct links to our Live Interactive UI, the Mathematical Proofs blog, and the Colab Training Script! 🚨**

*You live in Bangalore with its traffic. You know the problem...*
<br><br>

<img src=".assets/simulation.gif" width="750" alt="Traffic UI Simulation Demonstration" style="border-radius: 8px; border: 1px solid #eaeaea;">
<p><i>The Traffic Env OpenEnv UI, demonstrating stochastic phase shifts and real-time route execution.</i></p>

</div>

---

## 1. The Problem: A Universal Testbed for Spatial-Temporal Flow
Traffic management is one of the most complex stochastic challenges in the real world. A standard intersection does not just require an agent to "prevent crashes"; it requires forecasting dynamically shifting Origin-Destination (OD) probability matrices and handling cascading fluid dynamics.

Traditionally, modeling this requires tracking 10,000+ individual vehicle entities (Microscopic/Lagrangian tracking), which is computationally explosive, slow, and incredibly difficult to interface with modern AI training loops. 

**Our Novel Angle:** We didn't just build a game; we built an agent-agnostic research sandbox. By leveraging modern Traffic Flow Theory, we established a rigorous mathematical proof that under a strict "no-overtake" (FIFO) constraint, the complex problem of **microscopic priority routing** mathematically devolves into a highly efficient **mesoscopic cell eviction** problem. 

This environment provides researchers with a mathematically accurate, lightweight spatial-temporal benchmark. Whether you are testing an LLM, a traditional RL agent, or a heuristic algorithm, this OpenEnv environment exposes the raw, underlying physics of traffic flow.

---

## 2. Environment Architecture & Physics
Because this environment is agent-agnostic, the underlying simulation must be flawless. This is a rigorously backed physics environment built on the **Lighthill-Whitham-Richards (LWR)** conservation law and computationally discretized using **Daganzo’s Cell Transmission Model (1994)**.

<div align="center">
  <img src="./.assets/eviction.gif" width="600" alt="Mesoscopic Eviction Loop Animation" style="border: 1px solid #eaeaea; border-radius: 8px;">
  <p><i>Figure 1: The mathematical "no-overtake" constraint forcing the intersection to process priority vehicle routing as a bulk cell-eviction task.</i></p>
</div>