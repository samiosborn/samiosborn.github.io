---
layout: project
title: Self-balancing Robot Overview
project: self-balancing-robot
project_title: Self-balancing Robot
category: robotics
kind: project
order: 1
date: 2026-03-08
summary: Inverted pendulum robot focused on sensing, linearisation, and robust control design.
permalink: /projects/robotics/self-balancing-robot/
project_links:
  - label: Code Repository
    url: https://github.com/samiosborn
---
## What this project is
A two-wheel inverted pendulum platform for studying estimation and real-time feedback control.

## Why it matters
Balancing systems expose control assumptions quickly. They are useful for testing model mismatch, sensor noise, and latency effects.

## Architecture overview
1. IMU and encoder sensing.
2. State estimation and filtering.
3. Linearised model around upright equilibrium.
4. Controller loop with safety constraints.

## Current status
- Sensor fusion baseline in place.
- First linear model validated against short rollouts.
- Controller tuning underway.

## Selected results
- Stable balance over short windows indoors.
- Repeatable failure cases recorded for tuning.

## Roadmap
- Improve estimator robustness under vibration.
- Add disturbance rejection tests.
- Extend to trajectory tracking.
