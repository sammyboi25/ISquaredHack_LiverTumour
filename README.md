# ISquaredHackathon
This repository contains the winning solution for the iSquared Hackathon – Liver Ultrasound Detection Challenge.
The project implements a full end-to-end object detection pipeline using YOLO to detect and localize liver-related findings in ultrasound images.

The solution focuses heavily on data quality, class imbalance handling, and robust training, which played a key role in achieving top performance.

Problem Overview

Liver ultrasound images are challenging due to:

High noise and low contrast

Significant class imbalance:
<img width="1072" height="688" alt="image" src="https://github.com/user-attachments/assets/6b829d18-6c91-4a09-b35e-da2a4f53c15b" />

Presence of negative images with no detectable findings

Mixed-class images containing multiple lesion types

The goal was to build a model that accurately detects and localizes liver abnormalities while conforming to strict competition submission rules.

Dataset Handling & Preprocessing
1. Kaggle Integration

Dataset downloaded automatically using the Kaggle API

Secure API key handling via Colab environment

2. Dataset Auditing

Verified image–annotation pairing

Identified missing or empty annotation files

Quantified class imbalance and negative samples

Visualized class distributions before balancing

Class Separation Strategy

To gain finer control over imbalance and augmentation:

Training images were separated into:

Class-specific folders (0–6) for single-class images

Mixed-class folder for images containing multiple labels

Negative images (missing or empty annotations)

This enabled targeted balancing without corrupting bounding box integrity.

Class Balancing & Augmentation
Positive Classes

Balanced all 7 classes to match the largest class

Applied safe augmentations that preserve bounding boxes:

Brightness adjustment

Contrast scaling

Gamma correction

Ensured annotation consistency during augmentation

Negative Images

Augmented negative samples separately using:

Brightness/contrast shifts

Vertical flips

Rotations

Balanced negatives to reduce false positives

Final distributions were visualized to confirm dataset balance.

YOLO-Ready Dataset Construction

All balanced class images and annotations were merged into a single YOLO-compatible training folder

The balanced classes:
<img width="1072" height="688" alt="image" src="https://github.com/user-attachments/assets/84f241f7-8897-496f-bd37-81660065e194" />


Validation data was merged similarly

Custom YOLO dataset YAML created with medical class labels:

FFC, FFS, HCC, cyst, hemangioma, dysplastic, CCA

Model Training

Framework: Ultralytics YOLO

Model: YOLO (small variant)

Image size: 640×640

Early stopping with patience

GPU-accelerated training

Validation monitoring with mAP@0.5

Training emphasized stability and generalization over overfitting.

Evaluation

[![Open In Colab](https://colab.research.google.com/drive/1JVKMujD0OFVeH4nRmtIWIGuZZPACkahE#scrollTo=rL54NX3JbtE_)
