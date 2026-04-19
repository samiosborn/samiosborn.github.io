---
layout: project
title: Embedded Bring-up and First Balance-Direction Test
project: balancebot
project_title: BalanceBot
category: robotics
kind: build-log
date: 2026-03-08
order: 1
summary: Brought up the IMU, motor driver, and encoders on the ESP32, then ran the first suspended balance-direction test.
permalink: /projects/robotics/balancebot/build-logs/embedded-bring-up/
---
## What changed
- Set up the firmware structure around separate drivers, estimation, control, and robot state.
- Brought up the ICM-20948 IMU and verified pitch estimation.
- Brought up the SparkFun motor driver over Qwiic / I2C.
- Brought up both quadrature encoders and verified their counts independently.
- Verified motor-to-encoder channel mapping with short pulse tests.
- Ran a first suspended balance-direction test with the motors off the ground.

## What broke
- The IMU orientation initially drifted into an unsafe-tilt fault because the sensor mount had moved.
- Motor-driver bring-up initially failed until the wiring and I2C initialisation path were cleaned up.
- Some early test runs looked sluggish because the motors are rated for 12V but are currently being driven from a 2S pack.

## What was learned
- The software stack is now healthy enough to support controlled hardware testing.
- IMU mounting and coordinate consistency matter immediately.
- It is worth testing each subsystem in isolation before attempting full balancing.
- The balance loop is active, but tuning and available motor authority still need work.

## Next
- Tighten the inner-loop gains.
- Refine the restrained balance test setup.
- Start using encoder feedback more directly in the balancing analysis.