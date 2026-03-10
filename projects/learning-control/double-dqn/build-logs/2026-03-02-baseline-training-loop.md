---
layout: project
title: Baseline Training Loop Complete
project: double-dqn
project_title: Double DQN
category: learning-control
kind: build-log
date: 2026-03-02
order: 1
summary: Completed baseline training loop and initial comparison against vanilla DQN.
permalink: /projects/learning-control/double-dqn/build-logs/baseline-training-loop/
---
## What changed
- Implemented replay buffer and target-network updates.
- Added Double DQN target computation.

## What broke
- Initial instability under high learning rates.

## What was learned
- Conservative update settings improved early training consistency.

## Next
- Add ablation runs with fixed random seeds.
