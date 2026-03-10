---
layout: project
title: Initial Controller Tuning Pass
project: self-balancing-robot
project_title: Self-balancing Robot
category: robotics
kind: build-log
date: 2026-03-08
order: 1
summary: First tuning pass on the balancing loop with emphasis on stability margins.
permalink: /projects/robotics/self-balancing-robot/build-logs/controller-tuning/
---
## What changed
- Tuned baseline gains in closed-loop tests.
- Added simple anti-windup handling.

## What broke
- Oscillation appeared under aggressive gain settings.

## What was learned
- Estimator delay must be factored into tuning strategy.

## Next
- Add disturbance response tests.
