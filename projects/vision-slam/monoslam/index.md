---
layout: project
title: MonoSLAM Overview
project: monoslam
project_title: MonoSLAM
category: vision-slam
kind: project
order: 1
date: 2026-03-18
summary: Monocular SLAM implementation.
permalink: /projects/vision-slam/monoslam/
project_links:
  - label: GitHub Repository
    url: https://github.com/samiosborn/Robotics/tree/main/MonoSLAM
  - label: ETH3D Dataset
    url: https://www.eth3d.net/
---
## What this project is
MonoSLAM is a monocular visual SLAM build that tracks camera motion, estimates sparse structure, and incrementally refines the map in real time.

## Why it matters
Monocular SLAM sits at the boundary between geometry and systems engineering. It is a useful testbed for understanding uncertainty, observability, and failure modes in perception pipelines.

## Architecture overview
1. Feature extraction and matching in consecutive frames.
2. Two-view bootstrap with essential matrix, cheirality checks, and parallax constraints.
3. Keyframe insertion and pose-only optimisation.
4. Local map updates and outlier rejection.

## Current status
- Front-end feature matching implemented with reproducible parameter settings.
- Two-view bootstrap working on controlled sequence subsets.
- Keyframe tracking integrated; map consistency checks in progress.

## Selected results
- Stable bootstrap on short ETH3D sequences with robust inlier filtering.
- Tracking retained through moderate viewpoint changes.
- See the demo pages for visual output snapshots and diagnostics.

## Roadmap
- Add loop-closure candidates and relocalisation hooks.
- Improve failure detection around low-parallax segments.
- Expand quantitative benchmarking across more sequence types.
