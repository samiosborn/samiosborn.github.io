---
layout: project
title: Cheirality and Parallax Checks
project: monoslam
project_title: MonoSLAM
category: vision-slam
kind: note
date: 2026-03-14
order: 2
summary: Using positive-depth and baseline-angle checks to reject geometrically invalid reconstructions.
permalink: /projects/vision-slam/monoslam/notes/cheirality-and-parallax/
---
A valid reconstruction requires positive depth in both camera frames and sufficient triangulation angle.

Practical checks in the pipeline:
1. Positive depth ratio for triangulated points.
2. Median parallax threshold to avoid near-degenerate solutions.
3. Early rejection if reconstructed structure collapses onto a narrow depth band.

These checks prevent apparently successful bootstrap cases from degrading immediately in tracking.
