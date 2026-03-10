---
layout: project
title: Quadratic MLP Derivation for XOR
project: xor-classification
project_title: XOR Classification
category: learning-control
kind: note
date: 2025-03-23
order: 1
summary: Model definition, manual gradient derivation, and optimisation details for XOR classification.
permalink: /projects/learning-control/xor-classification/notes/quadratic-mlp-derivation/
---
XOR is not linearly separable, so a purely linear classifier cannot solve it. This model introduces non-linearity through a quadratic hidden transformation while keeping the architecture minimal.

## Model definition
- Input sum: \( s = w_1x_1 + w_2x_2 + b \)
- Hidden map: \( t = s(sv_0 + v_1) \)
- Output: \( o = \sigma(t) = \frac{1}{1 + e^{-t}} \)
- Loss: \( L = -y\log(o) - (1-y)\log(1-o) \)

## Chain-rule structure
Gradients follow the same chain-rule decomposition:

\[
\frac{\partial L}{\partial w_i} = \frac{\partial L}{\partial o}
\cdot \frac{\partial o}{\partial t}
\cdot \frac{\partial t}{\partial s}
\cdot \frac{\partial s}{\partial w_i}
\]

\[
\frac{\partial L}{\partial v_i} = \frac{\partial L}{\partial o}
\cdot \frac{\partial o}{\partial t}
\cdot \frac{\partial t}{\partial v_i}
\]

Key local derivatives:
- \( \frac{\partial s}{\partial w_1}=x_1,\; \frac{\partial s}{\partial w_2}=x_2,\; \frac{\partial s}{\partial b}=1 \)
- \( \frac{\partial t}{\partial s}=2sv_0+v_1,\; \frac{\partial t}{\partial v_0}=s^2,\; \frac{\partial t}{\partial v_1}=s \)
- \( \frac{d\sigma}{dt}=\sigma(t)(1-\sigma(t)) \)

## Optimisation and stability notes
Weights are initialised with Xavier scaling and updated with gradient descent:

\[
\theta \leftarrow \theta - \eta\nabla_\theta L
\]

The practical lesson is that gradient correctness is necessary but insufficient: the hidden non-linearity and learning rate jointly determine whether training converges smoothly.
