---
layout: project
title: Front-end and Bootstrap Baseline
project: monoslam
project_title: MonoSLAM
category: vision-slam
kind: build-log
date: 2026-03-10
order: 1
summary: Implemented front-end matching and first complete two-view bootstrap pass.
permalink: /projects/vision-slam/monoslam/build-logs/frontend-and-bootstrap/
---
## What changed
- Added feature extraction and descriptor matching.
- Implemented essential-matrix RANSAC.
- Wired pose recovery and initial triangulation.

## What broke
- Several bootstrap runs passed RANSAC but failed depth consistency checks.

## What was learned
- Inlier count alone was a poor quality indicator.
- Parallax thresholding was essential for stable initial maps.

## Next
- Add cheirality and parallax diagnostics to logs.
- Improve keyframe acceptance logic.
