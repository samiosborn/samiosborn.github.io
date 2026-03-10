---
layout: project
title: Initial From-scratch Implementation
project: xor-classification
project_title: XOR Classification
category: learning-control
kind: build-log
date: 2025-03-23
order: 1
summary: First complete XOR classifier implementation with manual derivatives and convergence diagnostics.
permalink: /projects/learning-control/xor-classification/build-logs/initial-from-scratch-implementation/
---
## What changed
- Implemented forward pass with quadratic hidden transformation.
- Added manual gradient calculations for all parameters.
- Logged parameter updates and output-surface diagnostics.

## What broke
- Early runs were sensitive to initialisation scale and learning-rate choice.

## What was learned
- Explicit derivative checks were useful for debugging convergence behaviour.
- A simple architecture is enough for XOR when the non-linearity is well chosen.

## Next
- Compare against a baseline auto-diff implementation.
