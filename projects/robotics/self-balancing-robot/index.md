---
layout: project
title: BalanceBot Overview
project: balancebot
project_title: BalanceBot
category: robotics
kind: project
order: 1
date: 2026-03-08
summary: Two-wheel self-balancing robot built around an ESP32, with a focus on sensing, embedded control, and disciplined hardware bring-up.
permalink: /projects/robotics/balancebot/
project_links:
  - label: Code Repository
    url: https://github.com/samiosborn/BalanceBot
---
## What this project is
BalanceBot is a two-wheel self-balancing robot built around an ESP32 microcontroller.

The project is being developed as a modular embedded robotics system rather than a quick prototype. The current focus is on getting the sensing, actuation, and balancing loop working reliably before adding higher-level behaviours.

## Why it matters
A self-balancing robot is a compact way to study real-time control properly. It forces the estimator, controller, motor commands, and safety logic to work together under tight timing and noisy measurements.

It is also a good platform for testing practical engineering questions such as:
- how much latency the control loop can tolerate
- how encoder and IMU noise affect stability
- how software structure helps or hurts hardware bring-up
- how much control authority is really available from a given motor and battery setup

## Hardware
- ELEGOO ESP32 development board
- diymore 30-pin ESP32 breakout board with screw terminals
- 2x JGA25-37 12V 200 RPM brushed DC gear motors with rear quadrature encoders
- SparkFun Qwiic Motor Driver (SCMD)
- ICM-20948 IMU
- 2S LiPo battery
- 5V buck converter

## Software architecture
The firmware is written in C++ and organised around a few clear layers:
1. Hardware drivers for the IMU, motor driver, and encoders.
2. Estimation for pitch and angular rate.
3. Balance control using a simple inner-loop controller.
4. Robot state and safety logic.
5. Bring-up and debug tooling for controlled testing.

## Current status
- Embedded project structure in place with PlatformIO and modular C++ components.
- IMU bring-up completed and pitch estimation working.
- Motor driver bring-up completed.
- Encoder bring-up completed on both wheels.
- Motor-to-encoder mapping checked.
- Initial suspended balance-direction tests completed.

## Selected results
- The sensing and actuation chain now works end to end.
- The robot can be armed safely in a controlled test setup.
- Initial balance-direction testing shows the controller is active, with further tuning still needed.

## Roadmap
- Improve inner-loop tuning and reduce sluggish response.
- Clean up balance-direction testing and move to restrained balancing tests.
- Add wheel-velocity estimation into the control stack.
- Add higher-level forward and turn commands.
- Add Wi-Fi control from a phone once the inner loop is reliable.