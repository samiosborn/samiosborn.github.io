---
layout: project
title: Double DQN and Overestimation
project: double-dqn
project_title: Double DQN
category: learning-control
kind: note
date: 2026-03-01
order: 1
summary: Why decoupling action selection and evaluation reduces positive bias in Q estimates.
permalink: /projects/learning-control/double-dqn/notes/double-dqn-overestimation/
---
This note outlines the overestimation mechanism in vanilla DQN and the corresponding Double DQN correction.

The key idea is to split the action-selection and action-evaluation roles between online and target networks when computing the temporal-difference target.
