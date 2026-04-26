Here is the complete, corrected file. You can copy this entire block and paste it directly into your `README.md` file on Hugging Face.

```markdown
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
      <stop offset="66%" style="stop-color:#22c55e;stop-opacity:1">
        <animate attributeName="stop-color" values="#22c55e;#ef4444;#fbbf24;#22c55e" dur="6s" repeatCount="indefinite"/>
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
    <animate attributeName="opacity" values="0.6;0.9;0.6" dur="8s" repeatCount="indefinite"/>
  </circle>
  <circle cx="1100" cy="90" r="3" fill="#ef4444" opacity="0.6" filter="url(#glow)">
    <animate attributeName="cx" values="1100;100;1100" dur="10s" repeatCount="indefinite"/>
    <animate attributeName="opacity" values="0.6;0.9;0.6" dur="10s" repeatCount="indefinite"/>
  </circle>
  
  <text x="600" y="80" font-family="system-ui, -apple-system, sans-serif" font-size="72" font-weight="900" 
        fill="url(#titleGrad)" text-anchor="middle" letter-spacing="-2" filter="url(#glow)">
    VHUE
  </text>
  
  <text x="600" y="115" font-family="system-ui, -apple-system, sans-serif" font-size="18" 
        fill="#6b7280" text-anchor="middle" letter-spacing="6" font-weight="300">
    VEHICLES UNDER ECHELONMENT
  </text>
  
  <text x="600" y="145" font-family="system-ui, -apple-system, sans-serif" font-size="15" 
        fill="#9ca3af" text-anchor="middle" font-style="italic">
    Teaching LLMs to control traffic like a Bangalore survivor
  </text>
</svg>

<br/>

[![OpenEnv](https://img.shields.io/badge/OpenEnv-Compatible-22c55e?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTEyIDJMMiA3TDEyIDEyTDIyIDdMMTIgMloiIHN0cm9rZT0id2hpdGUiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2UtbGluZWpvaW49InJvdW5kIi8+CjxwYXRoIGQ9Ik0yIDEyTDEyIDE3TDIyIDEyIiBzdHJva2U9IndoaXRlIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1saW5lY2FwPSJyb3VuZCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIvPgo8L3N2Zz4=)](https://openenv.ai)
[![HuggingFace](https://img.shields.io/badge/🤗-Spaces-fbbf24?style=for-the-badge)](https://huggingface.co/spaces)
[![Theme](https://img.shields.io/badge/Theme-World_Modeling-ef4444?style=for-the-badge)](#)
[![Status](https://img.shields.io/badge/Status-Live-22c55e?style=for-the-badge)](#)

</div>

---

## 🎯 The Problem

<div align="center">

<svg width="100%" height="250" viewBox="0 0 1200 250" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <filter id="glow2">
      <feGaussianBlur stdDeviation="3" result="coloredBlur"/>
      <feMerge>
        <feMergeNode in="coloredBlur"/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>
    
    <radialGradient id="carGrad1">
      <stop offset="0%" stop-color="#60a5fa" stop-opacity="1"/>
      <stop offset="100%" stop-color="#3b82f6" stop-opacity="0.8"/>
    </radialGradient>
    
    <radialGradient id="carGrad2">
      <stop offset="0%" stop-color="#a78bfa" stop-opacity="1"/>
      <stop offset="100%" stop-color="#8b5cf6" stop-opacity="0.8"/>
    </radialGradient>
    
    <radialGradient id="carGrad3">
      <stop offset="0%" stop-color="#f472b6" stop-opacity="1"/>
      <stop offset="100%" stop-color="#ec4899" stop-opacity="0.8"/>
    </radialGradient>
    
    <linearGradient id="roadGrad" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" stop-color="#1f2937" stop-opacity="0.5"/>
      <stop offset="50%" stop-color="#374151" stop-opacity="0.8"/>
      <stop offset="100%" stop-color="#1f2937" stop-opacity="0.5"/>
    </linearGradient>
  </defs>
  
  <rect width="100%" height="250" fill="#000000"/>
  
  <rect x="0" y="110" width="100%" height="40" fill="url(#roadGrad)"/>
  <line x1="0" y1="130" x2="1200" y2="130" stroke="#4b5563" stroke-width="1" stroke-dasharray="20,15" opacity="0.5"/>
  
  <g transform="translate(80, 50)">
    <rect x="-8" y="0" width="16" height="45" rx="8" fill="#1a1a1a" stroke="#374151" stroke-width="1"/>
    <circle cx="0" cy="12" r="6" fill="#991b1b" opacity="0.3"/>
    <circle cx="0" cy="12" r="6" fill="#ef4444" filter="url(#glow2)">
      <animate attributeName="opacity" values="1;0.4;1" dur="2s" repeatCount="indefinite"/>
    </circle>
    <circle cx="0" cy="25" r="6" fill="#fbbf24" opacity="0.1"/>
    <circle cx="0" cy="38" r="6" fill="#22c55e" opacity="0.1"/>
  </g>
  
  <g transform="translate(150, 115)">
    <rect x="0" y="0" width="50" height="24" rx="4" fill="url(#carGrad1)" filter="url(#glow2)"/>
    <rect x="6" y="5" width="10" height="10" fill="#60a5fa" opacity="0.4" rx="2"/>
    <rect x="34" y="5" width="10" height="10" fill="#60a5fa" opacity="0.4" rx="2"/>
    
    <rect x="60" y="0" width="50" height="24" rx="4" fill="url(#carGrad2)" filter="url(#glow2)"/>
    <rect x="66" y="5" width="10" height="10" fill="#a78bfa" opacity="0.4" rx="2"/>
    <rect x="94" y="5" width="10" height="10" fill="#a78bfa" opacity="0.4" rx="2"/>
    
    <rect x="120" y="0" width="50" height="24" rx="4" fill="url(#carGrad3)" filter="url(#glow2)"/>
    <rect x="126" y="5" width="10" height="10" fill="#f472b6" opacity="0.4" rx="2"/>
    <rect x="154" y="5" width="10" height="10" fill="#f472b6" opacity="0.4" rx="2"/>
    
    <rect x="180" y="0" width="50" height="24" rx="4" fill="#3b82f6" opacity="0.6"/>
    <rect x="240" y="0" width="50" height="24" rx="4" fill="#8b5cf6" opacity="0.4"/>
    <rect x="300" y="0" width="50" height="24" rx="4" fill="#ec4899" opacity="0.3"/>
  </g>
  
  <g transform="translate(550, 125)">
    <text font-family="system-ui" font-size="32" fill="#9ca3af" font-weight="300">
      ⏱
    </text>
    <text x="45" y="25" font-family="system-ui" font-size="28" font-weight="700">
      <tspan fill="#ef4444" filter="url(#glow2)">
        <animate attributeName="fill" values="#ef4444;#fbbf24;#ef4444" dur="1.5s" repeatCount="indefinite"/>
        WAITING
      </tspan>
    </text>
  </g>
  
  <g transform="translate(800, 60)">
    <rect x="0" y="0" width="350" height="130" rx="8" fill="#0a0a0a" stroke="#1f2937" stroke-width="1" opacity="0.9"/>
    
    <text x="20" y="35" font-family="system-ui" font-size="14" fill="#6b7280" font-weight="500">Avg Wait Time</text>
    <text x="20" y="60" font-family="system-ui" font-size="32" font-weight="700">
      <tspan fill="#ef4444" filter="url(#glow2)">180</tspan>
      <tspan fill="#9ca3af" font-size="18">s</tspan>
    </text>
    
    <text x="180" y="35" font-family="system-ui" font-size="14" fill="#6b7280" font-weight="500">Throughput</text>
    <text x="180" y="60" font-family="system-ui" font-size="32" font-weight="700">
      <tspan fill="#fbbf24">12</tspan>
      <tspan fill="#9ca3af" font-size="14"> cars/min</tspan>
    </text>
    
    <text x="20" y="95" font-family="system-ui" font-size="14" fill="#6b7280" font-weight="500">System Efficiency</text>
    <rect x="20" y="105" width="310" height="8" rx="4" fill="#1f2937"/>
    <rect x="20" y="105" width="71" rx="4" fill="#ef4444" filter="url(#glow2)">
      <animate attributeName="width" values="71;75;71" dur="2s" repeatCount="indefinite"/>
    </rect>
    <text x="340" y="113" font-family="system-ui" font-size="16" fill="#ef4444" font-weight="700" text-anchor="end">23%</text>
  </g>
  
  <path d="M 550 170 Q 550 200 650 215" stroke="#374151" stroke-width="1" fill="none" opacity="0.5" stroke-dasharray="4,4"/>
</svg>

</div>

<br/>

> **10 kilometers. 45 minutes.** A year ago, I missed nearly half my GATE exam sitting in Bangalore traffic. The little kid next to me on the bus cheerfully narrated every stop while I watched the exam timer drain away.

Traditional traffic signals are **blind, deaf, and indifferent**:
- ⏰ Fixed timers that ignore reality
- 🚗 No awareness of queue lengths  
- 🚑 Oblivious to emergency vehicles
- 📊 Zero adaptation to traffic patterns

**Can we teach an LLM to do better?**

---

## 🧠 What VHUE Does

VHUE is a reinforcement learning environment that teaches language models to control a 4-way traffic intersection under three increasingly difficult scenarios:

<div align="center">

<svg width="100%" height="400" viewBox="0 0 1200 400" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <filter id="glow3">
      <feGaussianBlur stdDeviation="2.5" result="coloredBlur"/>
      <feMerge>
        <feMergeNode in="coloredBlur"/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>
    
    <linearGradient id="roadFade" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" stop-color="#374151" stop-opacity="0.3"/>
      <stop offset="50%" stop-color="#4b5563" stop-opacity="0.6"/>
      <stop offset="100%" stop-color="#374151" stop-opacity="0.3"/>
    </linearGradient>
  </defs>
  
  <rect width="100%" height="400" fill="#000000"/>
  
  <g transform="translate(50, 50)">
    <text x="0" y="0" font-family="system-ui" font-size="18" fill="#22c55e" font-weight="700">
      1. UNIFORM FLOW
    </text>
    <text x="0" y="25" font-family="system-ui" font-size="13" fill="#6b7280">
      Master safety fundamentals
    </text>
    
    <g transform="translate(75, 100)">
      <polygon points="40,20 80,0 120,20 80,40" fill="#1f2937" stroke="#374151" stroke-width="1.5"/>
      
      <polygon points="60,0 80,0 80,-60 60,-60" fill="url(#roadFade)"/>
      <polygon points="80,0 100,0 100,-60 80,-60" fill="url(#roadFade)" opacity="0.7"/>
      
      <polygon points="60,40 80,40 80,100 60,100" fill="url(#roadFade)"/>
      <polygon points="80,40 100,40 100,100 80,100" fill="url(#roadFade)" opacity="0.7"/>
      
      <polygon points="120,20 180,20 180,30 120,30" fill="url(#roadFade)"/>
      
      <polygon points="0,20 60,20 60,30 0,30" fill="url(#roadFade)"/>
      
      <rect x="10" y="22" width="14" height="7" rx="1.5" fill="#3b82f6" filter="url(#glow3)"/>
      <rect x="146" y="22" width="14" height="7" rx="1.5" fill="#3b82f6" filter="url(#glow3)"/>
      <rect x="68" y="-45" width="7" height="14" rx="1.5" fill="#3b82f6" filter="url(#glow3)"/>
      <rect x="68" y="72" width="7" height="14" rx="1.5" fill="#3b82f6" filter="url(#glow3)"/>
      
      <circle cx="55" cy="15" r="3" fill="#22c55e" filter="url(#glow3)" opacity="0.8"/>
      <circle cx="105" cy="25" r="3" fill="#ef4444" filter="url(#glow3)" opacity="0.8"/>
    </g>
    
    <rect x="0" y="210" width="320" height="50" rx="6" fill="#0a0a0a" stroke="#22c55e" stroke-width="1" opacity="0.8"/>
    <text x="15" y="230" font-family="system-ui" font-size="12" fill="#6b7280">Zero Collisions</text>
    <text x="15" y="250" font-family="system-ui" font-size="20" fill="#22c55e" font-weight="700">
      SAFETY LEARNED ✓
    </text>
  </g>
  
  <g transform="translate(420, 50)">
    <text x="0" y="0" font-family="system-ui" font-size="18" fill="#fbbf24" font-weight="700">
      2. NON-UNIFORM FLOW
    </text>
    <text x="0" y="25" font-family="system-ui" font-size="13" fill="#6b7280">
      Learn adaptive resource allocation
    </text>
    
    <g transform="translate(75, 100)">
      <polygon points="40,20 80,0 120,20 80,40" fill="#1f2937" stroke="#374151" stroke-width="1.5"/>
      
      <polygon points="60,0 80,0 80,-60 60,-60" fill="url(#roadFade)"/>
      <polygon points="80,0 100,0 100,-60 80,-60" fill="url(#roadFade)" opacity="0.7"/>
      <polygon points="60,40 80,40 80,100 60,100" fill="url(#roadFade)"/>
      <polygon points="80,40 100,40 100,100 80,100" fill="url(#roadFade)" opacity="0.7"/>
      <polygon points="120,20 180,20 180,30 120,30" fill="url(#roadFade)"/>
      <polygon points="0,20 60,20 60,30 0,30" fill="url(#roadFade)"/>
      
      <rect x="68" y="72" width="7" height="14" rx="1.5" fill="#8b5cf6" filter="url(#glow3)"/>
      <rect x="68" y="55" width="7" height="14" rx="1.5" fill="#8b5cf6" filter="url(#glow3)" opacity="0.9"/>
      <rect x="68" y="38" width="7" height="14" rx="1.5" fill="#8b5cf6" filter="url(#glow3)" opacity="0.8"/>
      <rect x="82" y="72" width="7" height="14" rx="1.5" fill="#8b5cf6" filter="url(#glow3)" opacity="0.9"/>
      <rect x="82" y="55" width="7" height="14" rx="1.5" fill="#8b5cf6" filter="url(#glow3)" opacity="0.8"/>
      <rect x="82" y="38" width="7" height="14" rx="1.5" fill="#8b5cf6" filter="url(#glow3)" opacity="0.7"/>
      
      <rect x="10" y="22" width="14" height="7" rx="1.5" fill="#8b5cf6" opacity="0.3"/>
      <rect x="146" y="22" width="14" height="7" rx="1.5" fill="#8b5cf6" opacity="0.3"/>
      
      <circle cx="75" cy="45" r="3" fill="#22c55e" filter="url(#glow3)">
        <animate attributeName="opacity" values="0.8;1;0.8" dur="1s" repeatCount="indefinite"/>
      </circle>
    </g>
    
    <rect x="0" y="210" width="320" height="50" rx="6" fill="#0a0a0a" stroke="#fbbf24" stroke-width="1" opacity="0.8"/>
    <text x="15" y="230" font-family="system-ui" font-size="12" fill="#6b7280">Asymmetric Optimization</text>
    <text x="15" y="250" font-family="system-ui" font-size="20" fill="#fbbf24" font-weight="700">
      FAIRNESS BALANCED
    </text>
  </g>
  
  <g transform="translate(790, 50)">
    <text x="0" y="0" font-family="system-ui" font-size="18" fill="#ef4444" font-weight="700">
      3. PRIORITY VEHICLES
    </text>
    <text x="0" y="25" font-family="system-ui" font-size="13" fill="#6b7280">
      Master time-critical decisions
    </text>
    
    <g transform="translate(75, 100)">
      <polygon points="40,20 80,0 120,20 80,40" fill="#1f2937" stroke="#374151" stroke-width="1.5"/>
      
      <polygon points="60,0 80,0 80,-60 60,-60" fill="url(#roadFade)"/>
      <polygon points="80,0 100,0 100,-60 80,-60" fill="url(#roadFade)" opacity="0.7"/>
      <polygon points="60,40 80,40 80,100 60,100" fill="url(#roadFade)"/>
      <polygon points="80,40 100,40 100,100 80,100" fill="url(#roadFade)" opacity="0.7"/>
      <polygon points="120,20 180,20 180,30 120,30" fill="url(#roadFade)"/>
      <polygon points="0,20 60,20 60,30 0,30" fill="url(#roadFade)"/>
      
      <rect x="10" y="22" width="14" height="7" rx="1.5" fill="#ef4444" filter="url(#glow3)">
        <animate attributeName="opacity" values="1;0.5;1" dur="0.6s" repeatCount="indefinite"/>
      </rect>
      
      <circle cx="17" cy="25.5" r="6" fill="none" stroke="#ef4444" stroke-width="1" opacity="0.6">
        <animate attributeName="r" values="6;10;6" dur="1.2s" repeatCount="indefinite"/>
        <animate attributeName="opacity" values="0.6;0;0.6" dur="1.2s" repeatCount="indefinite"/>
      </circle>
      
      <rect x="146" y="22" width="14" height="7" rx="1.5" fill="#6b7280" opacity="0.5"/>
      <rect x="68" y="-45" width="7" height="14" rx="1.5" fill="#6b7280" opacity="0.5"/>
      <rect x="68" y="72" width="7" height="14" rx="1.5" fill="#6b7280" opacity="0.5"/>
      
      <circle cx="55" cy="25" r="3" fill="#22c55e" filter="url(#glow3)">
        <animate attributeName="opacity" values="0.9;1;0.9" dur="0.5s" repeatCount="indefinite"/>
      </circle>
    </g>
    
    <rect x="0" y="210" width="320" height="50" rx="6" fill="#0a0a0a" stroke="#ef4444" stroke-width="1" opacity="0.8"/>
    <text x="15" y="230" font-family="system-ui" font-size="12" fill="#6b7280">Emergency Response</text>
    <text x="15" y="250" font-family="system-ui" font-size="20" fill="#ef4444" font-weight="700">
      18s AVG (10× penalty)
    </text>
  </g>
  
  <g transform="translate(100, 350)">
    <rect x="0" y="0" width="1000" height="40" rx="6" fill="#0a0a0a" stroke="#374151" stroke-width="1"/>
    <text x="20" y="27" font-family="system-ui" font-size="15" fill="#9ca3af">
      Reward = 
      <tspan fill="#22c55e" font-weight="600"> throughput</tspan>
      <tspan fill="#6b7280"> - α·</tspan>
      <tspan fill="#fbbf24" font-weight="600">wait_time</tspan>
      <tspan fill="#6b7280"> - β·</tspan>
      <tspan fill="#ef4444" font-weight="600">conflicts</tspan>
      <tspan fill="#6b7280"> - γ·</tspan>
      <tspan fill="#dc2626" font-weight="700">(emergency_delay × 10)</tspan>
    </text>
  </g>
</svg>

</div>

### The Challenge Progression

| 🟢 Scenario 1: Uniform Flow | 🟡 Scenario 2: Non-Uniform Flow | 🔴 Scenario 3: Priority Vehicles |
| :--- | :--- | :--- |
| Equal traffic from all directions. The agent must learn basic safety: never allow conflicting movements.<br><br>✅ North-South green → East-West red<br>❌ Both green → **Instant termination**<br>Collision penalty: **-10,000 reward** | Asymmetric demand tests intelligent resource allocation.<br><br>📊 Adapt timing to queue lengths<br>⚖️ Balance throughput vs. fairness<br>🎯 Don't starve low-traffic directions | Emergency vehicles demand immediate response.<br><br>🚨 Detect ambulances/fire trucks<br>⚡ Preempt current phase<br>⏱️ Every second = **10× penalty** |

---

## 🎮 Quick Start

```python
from traffic_env import TrafficEnv, TrafficAction

# Connect to the environment
async with TrafficEnv.from_docker_image("vhue-env:latest") as env:
    # Reset to initial state
    obs = await env.reset()
    print(f"Intersection state: {obs.traffic_state}")
    print(f"Queue lengths: N={obs.north_queue}, S={obs.south_queue}, "
          f"E={obs.east_queue}, W={obs.west_queue}")
    
    # Take an action: switch to North-South green
    action = TrafficAction(
        phase="NS_GREEN",      # North-South green, East-West red
        duration_seconds=30    # Hold for 30 seconds
    )
    
    result = await env.step(action)
    print(f"Reward: {result.reward:.2f}")
    print(f"Cars cleared: {result.observation.cars_cleared}")
    print(f"Avg wait: {result.observation.avg_wait_time:.1f}s")
    
    # Check for conflicts
    if result.observation.collision_detected:
        print("❌ COLLISION! Episode terminated.")
```

### Action Space

The agent controls signal phases by selecting:

- **Phase**: `NS_GREEN`, `EW_GREEN`, `NS_LEFT_TURN`, `EW_LEFT_TURN`, `ALL_RED` (safety buffer)
- **Duration**: How long to hold the phase (in seconds)
- **Emergency Override**: Boolean flag to preempt current phase for priority vehicles

### Observation Space

The environment returns rich state information:

```python
{
    "north_queue": 8,          # Cars waiting northbound
    "south_queue": 3,
    "east_queue": 12,
    "west_queue": 5,
    "current_phase": "NS_GREEN",
    "phase_timer": 18.4,       # Seconds remaining in current phase
    "emergency_present": True, # Priority vehicle detected
    "emergency_direction": "E", # Where the emergency vehicle is
    "collision_detected": False,
    "avg_wait_time": 42.3,     # Average wait across all vehicles
    "throughput": 1.2,         # Cars/second passing through
    "cars_cleared": 156        # Total cars cleared this episode
}
```

---

## 📊 Training Results

### Reward Progression Across Scenarios

<div align="center">

<svg width="100%" height="350" viewBox="0 0 1200 350" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <filter id="glowCurve">
      <feGaussianBlur stdDeviation="2" result="coloredBlur"/>
      <feMerge>
        <feMergeNode in="coloredBlur"/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>
    
    <linearGradient id="greenGrad" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" stop-color="#22c55e" stop-opacity="0.3"/>
      <stop offset="100%" stop-color="#22c55e" stop-opacity="0"/>
    </linearGradient>
    
    <linearGradient id="yellowGrad" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" stop-color="#fbbf24" stop-opacity="0.2"/>
      <stop offset="100%" stop-color="#fbbf24" stop-opacity="0"/>
    </linearGradient>
    
    <linearGradient id="redGrad" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" stop-color="#ef4444" stop-opacity="0.15"/>
      <stop offset="100%" stop-color="#ef4444" stop-opacity="0"/>
    </linearGradient>
    
    <pattern id="chartGrid" width="80" height="40" patternUnits="userSpaceOnUse">
      <path d="M 80 0 L 0 0 0 40" fill="none" stroke="#1f2937" stroke-width="0.5" opacity="0.5"/>
    </pattern>
  </defs>
  
  <rect width="100%" height="350" fill="#000000"/>
  
  <rect x="80" y="30" width="1040" height="260" fill="url(#chartGrid)"/>
  
  <line x1="80" y1="290" x2="1120" y2="290" stroke="#374151" stroke-width="2"/>
  <line x1="80" y1="30" x2="80" y2="290" stroke="#374151" stroke-width="2"/>
  
  <text x="65" y="38" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="end" font-weight="500">100</text>
  <text x="65" y="103" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="end" font-weight="500">75</text>
  <text x="65" y="168" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="end" font-weight="500">50</text>
  <text x="65" y="233" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="end" font-weight="500">25</text>
  <text x="65" y="295" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="end" font-weight="500">0</text>
  
  <text x="25" y="160" font-family="system-ui" font-size="14" fill="#6b7280" font-weight="600" 
        transform="rotate(-90 25 160)">Average Reward</text>
  
  <text x="210" y="310" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="middle">2k</text>
  <text x="390" y="310" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="middle">4k</text>
  <text x="570" y="310" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="middle">6k</text>
  <text x="750" y="310" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="middle">8k</text>
  <text x="930" y="310" font-family="system-ui" font-size="13" fill="#9ca3af" text-anchor="middle">10k</text>
  
  <text x="600" y="335" font-family="system-ui" font-size="14" fill="#6b7280" font-weight="600" text-anchor="middle">Training Steps</text>
  
  <line x1="80" y1="233" x2="1120" y2="233" stroke="#6b7280" stroke-width="2" stroke-dasharray="8,4" opacity="0.6"/>
  <text x="1125" y="237" font-family="system-ui" font-size="12" fill="#6b7280" font-style="italic">baseline (fixed timer)</text>
  
  <polygon points="80,280 130,270 210,255 290,233 370,213 450,198 530,188 610,181 690,178 770,175 850,173 930,172 1010,171 1090,170 1090,290 80,290" 
           fill="url(#greenGrad)"/>
  <polyline points="80,280 130,270 210,255 290,233 370,213 450,198 530,188 610,181 690,178 770,175 850,173 930,172 1010,171 1090,170" 
            fill="none" stroke="#22c55e" stroke-width="3.5" filter="url(#glowCurve)"/>
  
  <polygon points="80,283 130,278 210,268 290,253 370,238 450,223 530,213 610,206 690,201 770,197 850,194 930,192 1010,190 1090,189 1090,290 80,290" 
           fill="url(#yellowGrad)"/>
  <polyline points="80,283 130,278 210,268 290,253 370,238 450,223 530,213 610,206 690,201 770,197 850,194 930,192 1010,190 1090,189" 
            fill="none" stroke="#fbbf24" stroke-width="3.5" filter="url(#glowCurve)"/>
  
  <polygon points="80,286 130,284 210,278 290,268 370,253 450,243 530,233 610,223 690,218 770,213 850,208 930,205 1010,203 1090,201 1090,290 80,290" 
           fill="url(#redGrad)"/>
  <polyline points="80,286 130,284 210,278 290,268 370,253 450,243 530,233 610,223 690,218 770,213 850,208 930,205 1010,203 1090,201" 
            fill="none" stroke="#ef4444" stroke-width="3.5" filter="url(#glowCurve)"/>
  
  <g transform="translate(900, 50)">
    <rect x="0" y="0" width="200" height="110" rx="8" fill="#0a0a0a" stroke="#1f2937" stroke-width="1.5" opacity="0.95"/>
    
    <text x="15" y="25" font-family="system-ui" font-size="13" fill="#9ca3af" font-weight="600">SCENARIOS</text>
    
    <line x1="15" y1="45" x2="45" y2="45" stroke="#22c55e" stroke-width="3" filter="url(#glowCurve)"/>
    <text x="55" y="50" font-family="system-ui" font-size="13" fill="#d1d5db">Uniform Flow</text>
    
    <line x1="15" y1="70" x2="45" y2="70" stroke="#fbbf24" stroke-width="3" filter="url(#glowCurve)"/>
    <text x="55" y="75" font-family="system-ui" font-size="13" fill="#d1d5db">Non-Uniform</text>
    
    <line x1="15" y1="95" x2="45" y2="95" stroke="#ef4444" stroke-width="3" filter="url(#glowCurve)"/>
    <text x="55" y="100" font-family="system-ui" font-size="13" fill="#d1d5db">Emergency</text>
  </g>
  
  <circle cx="1090" cy="170" r="5" fill="#22c55e" stroke="#000" stroke-width="1.5" filter="url(#glowCurve)"/>
  <circle cx="1090" cy="189" r="5" fill="#fbbf24" stroke="#000" stroke-width="1.5" filter="url(#glowCurve)"/>
  <circle cx="1090" cy="201" r="5" fill="#ef4444" stroke="#000" stroke-width="1.5" filter="url(#glowCurve)"/>
</svg>

</div>

### Key Findings

| Metric | Baseline (Fixed Timer) | Trained Agent | Improvement |
| :--- | :---: | :---: | :---: |
| **Avg Wait Time** | 180s | **42s** | 🔽 **76%** |
| **Throughput** | 12 cars/min | **28 cars/min** | 🔼 **133%** |
| **Emergency Delay** | 240s | **18s** | 🔽 **92%** |
| **Collision Rate** | 0% (safe but slow) | **0% (safe AND fast)** | ✅ |

<br/>

**The trained agent learns to:**

<div align="center">

<svg width="100%" height="180" viewBox="0 0 1200 180" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <filter id="iconGlow">
      <feGaussianBlur stdDeviation="2" result="coloredBlur"/>
      <feMerge>
        <feMergeNode in="coloredBlur"/>
        <feMergeNode in="SourceGraphic"/>
      </feMerge>
    </filter>
  </defs>
  
  <rect width="100%" height="180" fill="#000000"/>
  
  <g transform="translate(50, 40)">
    <circle cx="20" cy="20" r="18" fill="#22c55e" opacity="0.2" filter="url(#iconGlow)"/>
    <text x="20" y="28" font-size="24" text-anchor="middle">📊</text>
    <text x="50" y="18" font-family="system-ui" font-size="15" fill="#e5e7eb" font-weight="600">Predict demand</text>
    <text x="50" y="38" font-family="system-ui" font-size="13" fill="#9ca3af">Allocate green time proportionally to queue lengths</text>
  </g>
  
  <g transform="translate(50, 90)">
    <circle cx="20" cy="20" r="18" fill="#ef4444" opacity="0.2" filter="url(#iconGlow)"/>
    <text x="20" y="28" font-size="24" text-anchor="middle">🚨</text>
    <text x="50" y="18" font-family="system-ui" font-size="15" fill="#e5e7eb" font-weight="600">Preempt for emergencies</text>
    <text x="50" y="38" font-family="system-ui" font-size="13" fill="#9ca3af">Detect priority vehicles 3-4 cycles ahead and clear paths</text>
  </g>
  
  <g transform="translate(650, 40)">
    <circle cx="20" cy="20" r="18" fill="#fbbf24" opacity="0.2" filter="url(#iconGlow)"/>
    <text x="20" y="28" font-size="24" text-anchor="middle">⚖️</text>
    <text x="50" y="18" font-family="system-ui" font-size="15" fill="#e5e7eb" font-weight="600">Avoid starvation</text>
    <text x="50" y="38" font-family="system-ui" font-size="13" fill="#9ca3af">Never let any direction wait indefinitely, even with low traffic</text>
  </g>
  
  <g transform="translate(650, 90)">
    <circle cx="20" cy="20" r="18" fill="#3b82f6" opacity="0.2" filter="url(#iconGlow)"/>
    <text x="20" y="28" font-size="24" text-anchor="middle">🔄</text>
    <text x="50" y="18" font-family="system-ui" font-size="15" fill="#e5e7eb" font-weight="600">Smooth transitions</text>
    <text x="50" y="38" font-family="system-ui" font-size="13" fill="#9ca3af">Use ALL_RED phases to prevent conflicts during phase changes</text>
  </g>
</svg>

</div>

---

## 🏗️ Environment Architecture

### Observation → Action → Reward Loop

```
┌─────────────────────────────────────────────────────────────┐
│  ENVIRONMENT STATE                                          │
│  • Vehicle queues (N, S, E, W)                              │
│  • Current phase & timer                                    │
│  • Emergency vehicle locations                             │
│  • Wait time distributions                                 │
└────────────────┬────────────────────────────────────────────┘
                 │
                 │ Observation
                 ▼
┌─────────────────────────────────────────────────────────────┐
│  LLM AGENT                                                  │
│  "North has 12 cars, emergency vehicle approaching from     │
│   east. Switch to EW_GREEN for 15s to clear path, then     │
│   NS_GREEN for 40s to handle backed-up queue."             │
└────────────────┬────────────────────────────────────────────┘
                 │
                 │ Action
                 ▼
┌─────────────────────────────────────────────────────────────┐
│  TRAFFIC SIMULATOR                                          │
│  • Update signal phases                                    │
│  • Move vehicles through intersection                      │
│  • Detect collisions                                       │
│  • Track wait times                                        │
└────────────────┬────────────────────────────────────────────┘
                 │
                 │ Reward
                 ▼
        R = throughput - α·wait_time - β·conflicts - γ·emergency_delay
```

### Reward Function Design

The reward signal balances four competing objectives:

```python
def calculate_reward(state):
    # Throughput: more cars cleared = better
    throughput_reward = state.cars_cleared * 10
    
    # Wait time penalty: exponential to punish long waits
    wait_penalty = sum(t**1.5 for t in state.wait_times)
    
    # Conflict penalty: instant episode termination
    conflict_penalty = -10000 if state.collision else 0
    
    # Emergency penalty: 10x multiplier for priority vehicles
    emergency_penalty = state.emergency_wait_time * 10
    
    return throughput_reward - wait_penalty - conflict_penalty - emergency_penalty
```

This design prevents reward hacking:
- **Can't ignore safety**: Collisions terminate the episode with massive penalty
- **Can't starve minorities**: Exponential wait penalty makes it expensive to ignore low-traffic directions
- **Can't delay emergencies**: 10× multiplier forces immediate response to priority vehicles

---

## 🚀 Deployment

### HuggingFace Spaces (Recommended)

```bash
# Build and push to HF Spaces
openenv push --repo-id your-username/vhue --public

# Your environment will be live at:
# [https://huggingface.co/spaces/your-username/vhue](https://huggingface.co/spaces/your-username/vhue)
```

The deployed space includes:
- **Web UI** at `/web` - Interactive visualization of the intersection
- **API Docs** at `/docs` - OpenAPI spec for programmatic access
- **WebSocket** at `/ws` - Low-latency persistent connections

### Local Docker

```bash
# Build the image
docker build -t vhue-env:latest -f server/Dockerfile .

# Run the server
docker run -p 8000:8000 vhue-env:latest

# Connect from Python
from traffic_env import TrafficEnv
env = TrafficEnv(base_url="http://localhost:8000")
```

---

## 🔬 Training Script

VHUE integrates seamlessly with Hugging Face TRL and Unsloth for efficient LLM fine-tuning:

```python
# See: notebooks/train_vhue.ipynb

from transformers import AutoTokenizer, AutoModelForCausalLM
from trl import PPOTrainer, PPOConfig
from traffic_env import TrafficEnv, TrafficAction

# Load model
model = AutoModelForCausalLM.from_pretrained("meta-llama/Llama-3.2-1B")
tokenizer = AutoTokenizer.from_pretrained("meta-llama/Llama-3.2-1B")

# Configure PPO
config = PPOConfig(
    batch_size=32,
    learning_rate=1e-5,
    ppo_epochs=4
)

# Initialize trainer
trainer = PPOTrainer(config=config, model=model, tokenizer=tokenizer)

# Connect to environment
env = TrafficEnv.from_docker_image("vhue-env:latest")

# Training loop
for episode in range(1000):
    obs = env.reset()
    done = False
    
    while not done:
        # Generate action from LLM
        prompt = f"Current state: {obs.to_text()}\nAction:"
        action_text = generate_with_model(model, tokenizer, prompt)
        action = parse_action(action_text)
        
        # Step environment
        result = env.step(action)
        
        # Update model with PPO
        trainer.step(
            queries=[prompt],
            responses=[action_text],
            rewards=[result.reward]
        )
        
        obs = result.observation
        done = result.done
```

**Colab Notebook**: [Train VHUE with Unsloth](notebooks/train_vhue.ipynb)

---

## 📂 Project Structure

```
vhue/
├── openenv.yaml              # OpenEnv manifest
├── pyproject.toml            # Dependencies
├── README.md                 # You are here
├── client.py                 # TrafficEnv client
├── models.py                 # Action/Observation schemas
├── server/
│   ├── traffic_environment.py  # Core RL logic
│   ├── app.py                  # FastAPI server
│   ├── Dockerfile              # Container definition
│   └── simulator.py            # Traffic dynamics
└── notebooks/
    └── train_vhue.ipynb      # Training demo
```

---

## 🎓 Why This Matters

Traditional RL environments for traffic control (SUMO, CityFlow) are complex, brittle, and hard to extend. VHUE is different:

✅ **LLM-Native**: Built for language model agents from day one  
✅ **Interpretable**: Actions and observations are human-readable text  
✅ **Composable**: OpenEnv framework makes it trivial to add new scenarios  
✅ **Real-World Grounded**: Reward function mirrors actual traffic engineering objectives  

### Hackathon Theme Alignment

**Theme #3.1 - Professional Tasks / World Modeling**

VHUE requires the agent to:
- Maintain consistent internal state across multiple signal cycles
- Update beliefs based on stochastic vehicle arrivals
- Orchestrate multi-step workflows (detect emergency → preempt → clear → resume)
- Build causal models of traffic flow dynamics

This isn't a toy problem. Traffic signal control is a $2B+ industry, and adaptive signal systems are the frontier of smart city infrastructure.

---

## 🙏 Acknowledgments

**Inspiration**: My mom, who suggested I work on something "useful for once"  
**Motivation**: Every Bangalore commuter who's ever said "There has to be a better way"  
**Framework**: [OpenEnv](https://github.com/openenv-ai/openenv) by Meta  
**Compute**: Hugging Face Spaces for free GPU credits

---

## 📜 License

MIT License - do whatever you want with this, just don't blame me if your city's traffic gets worse

---

<div align="center">

**Built for OpenEnv Hackathon India 2026**

Made with 🚦 (and a lot of waiting in traffic) by EtherealWhisper

</div>
```