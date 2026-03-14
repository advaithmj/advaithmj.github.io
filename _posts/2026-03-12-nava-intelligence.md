---
layout: post
title: "I Built an AI That Designs and Simulates Rockets Autonomously"
date: 2026-03-12
categories: [project, AI, aerospace, robotics]
---

You give it a rocket spec. It simulates the flight, generates a 3D printable model, and hands you back a professional PDF report — completely on its own.

No human in the loop. Just a goal in, and engineering outputs out.

I built this from scratch. I'm in high school.

---

## What It Does

Nava Intelligence is an autonomous AI agent specialized for aerospace simulation. Given a natural language engineering goal, it:

1. Plans the task and writes a state file
2. Runs a full physics simulation using RocketPy — the same library used by real aerospace engineering teams
3. Generates a 4-panel trajectory plot (altitude, speed, acceleration, key metrics)
4. Produces a parametric 3D rocket model as an STL file via OpenSCAD
5. Writes a professional PDF report with all results embedded
6. Stops when done

Here's what a real run looks like. Input:

> *"Simulate a single-stage rocket: 20kg, 3000N motor, 3s burn. Give me the trajectory, a PDF report, and a 3D model."*

Output (autonomously, no intervention):

- **Apogee: 2,992 m**
- **Max velocity: 315 m/s**
- **Max acceleration: 109 m/s²**
- **Flight time: 53 seconds**

Plus a PDF report and a 3D printable STL file. All in under 2 minutes.

---

## How It Works

The agent runs in a loop. Each iteration it calls Claude's API, gets back either a tool call or a final answer, executes the tool in an isolated Docker sandbox, feeds the result back, and repeats.

The sandbox is the key part. The agent has full Python execution capability — it can write files, run simulations, call OpenSCAD — but it's completely isolated from the host machine. Whatever it does inside the container stays inside the container.

The stack:
- **Claude Haiku** as the reasoning engine
- **Docker** for the isolated execution sandbox
- **RocketPy** for flight physics
- **OpenSCAD** for parametric 3D modeling
- **ReportLab** for PDF generation
- **Python** for everything else

The whole thing is about 400 lines of agent infrastructure code. The hard part wasn't the code — it was figuring out how to make an AI agent that actually completes a task without going in circles.

---

## Why Aerospace

Small aerospace companies and startups need simulation work constantly. They don't always have a full simulation team. An autonomous agent that takes an engineering brief and returns results overnight — that's a real product with real value.

The goal is to be the best autonomous simulation tool for this specific domain. Not general AI. Not robotics. Aerospace simulation, done better than anything else.

---

## What's Next

- Multi-stage rocket simulation
- Structural load analysis
- Optimization loops (find the motor that maximizes apogee given a weight constraint)
- A web interface so you don't need to run it locally

The code is on GitHub. Pull requests welcome.

**[GitHub — Nava Intelligence](https://github.com/advaithmj/nava-intelligence)**
