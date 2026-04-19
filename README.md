# 3D Pedestrian Detection from a Single Camera — Intelligent Vehicles (TU Delft)

Final assignment for the **Intelligent Vehicles (ME41106)** course at TU Delft (2024–2025, Q2).

The goal is to detect pedestrians in 3D space using only a single monocular camera mounted on an autonomous vehicle, without relying on LiDAR or radar depth information.

---

## Problem

Recovering 3D positions from 2D images is an ill-posed problem: a single camera cannot directly measure depth. The core challenge is to lift 2D detections into 3D in a physically meaningful way.

## Approach

The pipeline combines a learned 2D detector with a geometric 3D lifting step:

1. **2D detection** — YOLO detects pedestrians in the camera image and returns bounding boxes.
2. **Ground plane constraint** — pedestrians are assumed to stand on a common ground plane (provided per frame by the dataset). Intersecting the bottom edge of each 2D bounding box with the ground plane recovers the 3D foot position.
3. **Height estimation** — the pedestrian height is estimated from the bounding box extent and the camera projection geometry.

This approach requires no additional sensors and runs in real time.

## Dataset

**View-of-Delft (VoD)** — a multi-sensor autonomous driving dataset recorded in Delft, The Netherlands. The vehicle carries a stereo camera, a LiDAR, and a radar. Ground-truth 3D annotations are provided for cars, pedestrians, and cyclists.

For this assignment, a subsequence of 115 timesteps (indices 1430–1545) is used.

## Modules

| Notebook | Content |
|----------|---------|
| `fa_00_overview` | Project setup and configuration |
| `fa_01a_data_visualization` | Sensor data visualization: coordinate frames, 3D bounding boxes, LiDAR/radar projections onto camera images, vehicle trajectory |
| `fa_02a_iv_only_3d_pedestrian_detection_single_camera` | Full 3D pedestrian detection pipeline (IV track) |

## Tech Stack

- Python 3, Jupyter notebooks
- NumPy, OpenCV, Matplotlib
- k3d (interactive 3D visualization in Jupyter)
- YOLO (2D object detection backbone)

## Key Concepts Covered

- Multi-sensor coordinate frame transforms (camera ↔ LiDAR ↔ radar ↔ world)
- Camera projection geometry (intrinsic matrix, homogeneous coordinates)
- Ground plane estimation and point-plane intersection
- 3D bounding box representation and visualization
- Quantitative evaluation of 3D detection performance
