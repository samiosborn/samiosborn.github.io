---
layout: project
title: Joint Control Baseline
project: so100-arm
project_title: SO100 Arm
category: robotics
kind: build-log
date: 2026-03-04
order: 1
summary: Established first reliable joint control baseline with command timing checks.
permalink: /projects/robotics/so100-arm/build-logs/joint-control-baseline/
---
## What changed
- Added basic joint command pipeline.
- Validated timing and response logging.

## What broke
- Drift appeared after repeated long sequences.

## What was learned
- Calibration cadence has a clear impact on repeatability.

## Next
- Tighten calibration loop and add more validation trajectories.
