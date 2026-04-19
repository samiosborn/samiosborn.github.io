---
layout: project
title: XOR Classification Overview
project: xor-classification
project_title: XOR Classification
category: learning-control
kind: project
order: 2
date: 2025-03-23
summary: A from-scratch quadratic MLP implementation for XOR classification, with manual derivatives and training diagnostics.
permalink: /projects/learning-control/xor-classification/
project_links:
  - label: Source Code
    url: https://github.com/samiosborn/Maths/tree/master/Multi-Layer-Perceptron
---
## What this project is
A small but rigorous learning systems build: a neural network that classifies XOR using a quadratic hidden transformation and manual backpropagation.

## Why it matters
XOR is a compact test case for non-linear representational power. It forces the model to move beyond linear decision boundaries and is a clear setting for validating first-principles derivations.

## Architecture overview
1. Input sum: `s = w1 x1 + w2 x2 + b`.
2. Quadratic hidden map: `t = s(sv0 + v1)`.
3. Sigmoid output and binary cross-entropy objective.
4. Gradient-descent updates from hand-derived gradients.

## Current status
- Full training loop implemented from scratch.
- Gradients derived and coded without auto-diff tooling.
- Visual diagnostics available for decision surface and weight evolution.

## Selected results
- Near-perfect accuracy on XOR points and stable behaviour on small perturbations.
- Smooth non-linear decision surface matching expected XOR geometry.

## Roadmap
- Compare with equivalent auto-diff implementation to benchmark numerical differences.
- Extend to small multi-class synthetic datasets with controlled non-linearity.
