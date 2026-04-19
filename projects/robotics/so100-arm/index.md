---
layout: project
title: SO100 Arm Overview
project: so100-arm
project_title: SO100 Arm
category: robotics
kind: project
order: 2
date: 2025-10-12
summary: Manipulation project exploring kinematics, calibration, and reliable arm control primitives.
permalink: /projects/robotics/so100-arm/
project_links:
  - label: Code Repository
    url: https://github.com/samiosborn/Robotics/tree/main/Robot_Arm_SO100
---
## What this project is
A practical manipulation stack built around the SO100 robotic arm platform.

## Why it matters
Manipulator reliability depends on clean interfaces between kinematics, calibration, and task-level control. This project is focused on that interface.

## Architecture overview
1. Joint-level communication and command interface.
2. Forward/inverse kinematics routines.
3. Calibration and repeatability checks.
4. Task scripts for pick-place and waypoint tracking.

## Current status
- Joint control interface stable.
- Calibration workflow established.
- Task-level scripts under active iteration.

## Selected results
- Repeatable end-effector placement in constrained test routines.

## Roadmap
- Extend IK handling near singular configurations.
- Add vision-guided waypoint experiments.
