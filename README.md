# Sensor Fusion and Object Detection

## Project Overview

This project implements a multi-object tracking and sensor-fusion pipeline for autonomous driving.

It builds on a previous 3D object detection project and uses `fpn_resnet` detections as input for tracking. The project combines LiDAR and camera measurements using an Extended Kalman Filter (EKF), track management, data association, and sensor fusion.

---

## Main Components

### 1. Extended Kalman Filter Tracking

Implemented in `filter.py`.

The tracking system:

- Predicts object motion using a 3D constant-velocity model
- Computes the system matrix and process noise covariance
- Updates tracks using incoming measurements
- Calculates measurement residuals and residual covariance

The single-target tracking experiment achieved a mean RMSE of approximately **0.28**, below the target value of 0.35.

---

### 2. Track Management

The track management component:

- Initializes new tracks from unassigned LiDAR measurements
- Transforms measurements from sensor coordinates to vehicle coordinates
- Maintains track scores and states
- Promotes tracks to tentative or confirmed states
- Deletes tracks when their score becomes too low or uncertainty becomes too large

This allows the system to create, maintain, and remove tracks automatically.

---

### 3. Data Association

Implemented in `association.py`.

The association process uses:

- Mahalanobis distance
- Chi-square gating
- Nearest-neighbor association
- Association matrices
- Unassigned track and measurement handling

This step determines which measurements belong to which existing tracks.

The tracking results show that temporary false tracks may appear, but persistent confirmed ghost tracks are avoided.

---

### 4. LiDAR-Camera Sensor Fusion

The project combines measurements from LiDAR and camera sensors.

The sensor-fusion implementation includes:

- Sensor field-of-view checks
- Coordinate transformations
- Nonlinear camera measurement modeling
- Camera measurement initialization
- LiDAR and camera measurement updates

LiDAR provides accurate distance information, while cameras provide useful visual and object-class information. Combining both sensors can improve the robustness of an autonomous driving perception system.

---

## Technologies and Concepts

- Python
- Extended Kalman Filter
- LiDAR
- Camera Sensors
- Sensor Fusion
- Multi-Object Tracking
- Mahalanobis Distance
- Chi-Square Gating
- Nearest-Neighbor Association
- FPN-ResNet
- 3D Object Detection

---

## Results

The project successfully demonstrates:

- Single-target tracking
- Automatic track initialization and deletion
- Multi-object tracking
- LiDAR-camera sensor fusion
- Track-state management
- Association between measurements and tracks

A tracking visualization is included in:

`my_tracking_results.avi`

---

## Challenges and Future Improvements

Some of the main challenges included:

- Managing track scores and deleting old tracks
- Implementing the nonlinear camera measurement model
- Correctly associating measurements with multiple tracks
- Configuring measurement noise

Possible future improvements include using camera-based object class and shape information to improve association and selecting different tracking models based on object distance and geometry.

---

## Project Report

For detailed implementation steps, results, and discussion, see:

[View Project Write-up](writeup.pdf)

---

## Author

**Shamima Sultana**

