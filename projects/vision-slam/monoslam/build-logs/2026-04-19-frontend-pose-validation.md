---
layout: project
title: Frontend Pose Validation and ETH3D Diagnostics
project: monoslam
project_title: MonoSLAM
category: vision-slam
kind: build-log
date: 2026-04-19
order: 3
summary: Added ETH3D frontend diagnostics and pose-support guardrails to distinguish stable pose estimates from local ambiguous failures.
permalink: /projects/vision-slam/monoslam/build-logs/frontend-pose-validation/
---
## What changed
- Added a proper ETH3D frontend diagnostic path for bootstrap, tracking, pose estimation, and map growth.
- Built PnP diagnostics to inspect correspondence counts, inlier counts, and threshold sensitivity frame by frame.
- Added pose-support filtering to separate bootstrap-born landmarks from later map-growth landmarks during PnP.
- Added post-PnP spatial coverage checks to reject poses supported by tiny local image regions.
- Added component-based support diagnostics for the winning PnP inlier set.
- Added threshold-stability diagnostics to compare pose support across nearby reprojection thresholds.

## What broke
- Some later ETH3D frames produced locally consistent but globally wrong pose hypotheses.
- Looser PnP thresholds could recover a different pose on a disjoint inlier set rather than a broader version of the same solution.
- Pre-PnP thinning and local motion-consistency filtering were not reliable enough to become default guardrails.

## What was learned
- The main frontend failure mode was not simply "too few matches" but unstable pose support on ambiguous thin cable structure.
- Frame 4 showed that two different pose hypotheses could coexist, each supported by a different local cluster of correspondences.
- A small spatially concentrated support set can look geometrically plausible unless it is explicitly checked.
- Threshold-stability across nearby PnP settings is a stronger signal of a bad pose than component size alone.
- Guardrails are more useful after pose recovery than aggressive filtering before PnP.

## Next
- Run the threshold-stability guard across more ETH3D sequences and longer windows.
- Measure false rejections on stable frames versus detections on unstable local-cluster poses.
- Decide whether threshold stability should become a default frontend acceptance rule.