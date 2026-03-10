---
layout: project
title: Two-view Bootstrap
project: monoslam
project_title: MonoSLAM
category: vision-slam
kind: note
date: 2026-03-12
order: 1
summary: Essential matrix estimation, pose disambiguation, and robust initialisation checks for monocular SLAM.
permalink: /projects/vision-slam/monoslam/notes/two-view-bootstrap/
---
Two-view bootstrap initialises the map and sets the first reliable camera poses.

The implementation follows this sequence:
1. Estimate the essential matrix with RANSAC.
2. Recover candidate relative poses.
3. Apply cheirality constraints and parallax thresholds.
4. Triangulate initial landmarks and reject unstable points.

The main practical issue is balancing inlier count versus geometric quality. High inlier counts with poor parallax produce fragile initial maps; lower counts with stronger geometry usually produce better long-run tracking.
