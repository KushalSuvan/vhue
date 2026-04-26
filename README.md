---
title: VHUE - Vehicles under Echelonment
emoji: 🚦
colorFrom: red
colorTo: green
sdk: docker
pinned: false
app_port: 8000
base_path: /web
tags:
  - openenv
  - reinforcement-learning
  - traffic-control
  - multi-agent
---

<div align="center">

<svg width="100%" height="180" viewBox="0 0 1200 180" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="titleGrad" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:#ef4444;stop-opacity:1">
        <animate attributeName="stop-color" values="#ef4444;#fbbf24;#22c55e;#ef4444" dur="6s" repeatCount="indefinite"/>
      </stop>
      <stop offset="33%" style="stop-color:#fbbf24;stop-opacity:1">
        <animate attributeName="stop-color" values="#fbbf24;#22c55e;#ef4444;#fbbf24" dur="6s" repeatCount="indefinite"/>
      </stop>
      <stop offset="100%" style="stop-color:#ef4444;stop-opacity:1">
        <animate attributeName="stop-color" values="#ef4444;#fbbf24;#22c55e;#ef4444" dur="6s" repeatCount="indefinite"/>
      </stop>
    </linearGradient>
    <filter id="glow">
      <feGaussianBlur stdDeviation="4" result="coloredBlur"/>
      <feMerge>
        <feMergeNode in="coloredBlur"/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>
    <pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
      <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#1a1a1a" stroke-width="0.5"/>
    </pattern>
  </defs>
  <rect width="100%" height="180" fill="#000000"/>
  <rect width="100%" height="180" fill="url(#grid)" opacity="0.3"/>
  <circle cx="100" cy="90" r="3" fill="#22c55e" opacity="0.6" filter="url(#glow)">
    <animate attributeName="cx" values="100;1100;100" dur="8s" repeatCount="indefinite"/>
  </circle>
  <text x="600" y="80" font-family="system-ui, sans-serif" font-size="72" font-weight="900" fill="url(#titleGrad)" text-anchor="middle" filter="url(#glow)">VHUE</text>
  <text x="600" y="115" font-family="system-ui, sans-serif" font-size="18" fill="#6b7280" text-anchor="middle" letter-spacing="6">VEHICLES UNDER ECHELONMENT</text>
  <text x="600" y="145" font-family="system-ui, sans-serif" font-size="15" fill="#9ca3af" text-anchor="middle" font-style="italic">Teaching LLMs to control traffic like a Bangalore survivor</text>
</svg>

<br/>

[![OpenEnv](https://img.shields.io/badge/OpenEnv-Compatible-22c55e?style=for-the-badge)](https://openenv.ai)
[![HuggingFace](https://img.shields.io/badge/🤗-Spaces-fbbf24?style=for-the-badge)](https://huggingface.co/spaces)

</div>

---

## 🎯 The Problem

<div align="center">
<svg width="100%" height="250" viewBox="0 0 1200 250" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <filter id="glow2"><feGaussianBlur stdDeviation="3" result="blur"/><feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
    <radialGradient id="carGrad1"><stop offset="0%" stop-color="#60a5fa"/><stop offset="100%" stop-color="#3b82f6"/></radialGradient>
    <linearGradient id="roadGrad"><stop offset="0%" stop-color="#1f2937"/><stop offset="50%" stop-color="#374151"/><stop offset="100%" stop-color="#1f2937"/></linearGradient>
  </defs>
  <rect width="100%" height="250" fill="#000000"/>
  <rect x="0" y="110" width="100%" height="40" fill="url(#roadGrad)"/>
  <g transform="translate(150, 115)">
    <rect x="0" y="0" width="50" height="24" rx="4" fill="url(#carGrad1)" filter="url(#glow2)"/>
    <rect x="60" y="0" width="50" height="24" rx="4" fill="#a78bfa" filter="url(#glow2)"/>
    <rect x="120" y="0" width="50" height="24" rx="4" fill="#f472b6" filter="url(#glow2)"/>
  </g>
  <text x="600" y="140" font-family="system-ui" font-size="28" font-weight="700" fill="#ef4444" filter="url(#glow2)">WAITING</text>
</svg>
</div>

> **10 kilometers. 45 minutes.** A year ago, I missed nearly half my GATE exam sitting in Bangalore traffic. 

---

## 🧠 What VHUE Does

VHUE is a reinforcement learning environment that teaches LLMs to control a 4-way intersection.

### Key Findings

| Metric | Baseline (Fixed Timer) | Trained Agent | Improvement |
| :--- | :---: | :---: | :---: |
| **Avg Wait Time** | 180s | **42s** | 🔽 **76%** |
| **Throughput** | 12 cars/min | **28 cars/min** | 🔼 **133%** |
| **Emergency Delay** | 240s | **18s** | 🔽 **92%** |

---

## 🏗️ Environment Architecture

```python
# Quick Start
async with TrafficEnv.from_docker_image("vhue-env:latest") as env:
    obs = await env.reset()
    action = TrafficAction(phase="NS_GREEN", duration_seconds=30)
    result = await env.step(action)