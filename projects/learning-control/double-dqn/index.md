---
layout: project
title: Double DQN Overview
project: double-dqn
project_title: Double DQN
category: learning-control
kind: project
order: 1
date: 2025-05-17
summary: Reinforcement learning project focused on overestimation bias and stable value learning.
permalink: /projects/learning-control/double-dqn/
project_links:
  - label: Code Repository
    url: https://github.com/samiosborn/Reinforcement-Learning/tree/main/CartPole
---
## What this project is
A Double DQN implementation and evaluation pipeline for analysing value overestimation and training stability.

## Why it matters
Many value-based methods can look stable while quietly accumulating biased estimates. Double DQN offers a direct way to reduce this bias.

## Architecture overview
1. Replay buffer and target network pipeline.
2. Double DQN target calculation.
3. Training/evaluation split with fixed seeds.
4. Monitoring of value estimates and policy performance.

## Current status
- Baseline training loop and replay handling implemented.
- Initial comparisons against vanilla DQN complete.
- Experiment tracking templates established.

## Selected results
- Reduced overestimation relative to vanilla baseline in early experiments.

## Roadmap
- Expand ablations over replay and target-update frequency.
- Improve run-to-run variance analysis.
