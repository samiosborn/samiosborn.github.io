---
layout: project
title: Epipolar Geometry in the Front-end
project: monoslam
project_title: MonoSLAM
category: vision-slam
kind: note
date: 2026-03-16
order: 3
summary: How epipolar constraints are used to filter correspondences before optimisation.
permalink: /projects/vision-slam/monoslam/notes/epipolar-geometry/
---
Epipolar geometry reduces correspondence ambiguity before optimisation and improves robustness under noise.

The front-end uses the normalised epipolar residual as a gating signal before passing matches into pose estimation. This shifts work away from later optimisation stages and limits contamination from weak correspondences.
