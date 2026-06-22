The main goal is to compare two practical strategies: a global model trained on data from multiple users and a personalized model calibrated on a small amount of data from a specific user.

## Overview

EMG signals are highly user-dependent: muscle activation patterns vary across people, recording sessions, electrode placement, fatigue, and gesture execution style. Because of this, a model that works well on average may still perform poorly for some users.

This project builds an experimental benchmark to evaluate whether personalized calibration can improve gesture recognition compared with global subject-independent models.

## Dataset

The experiments use an EMG gesture dataset containing:

* 36 subjects
* 72 raw EMG recordings
* 8 EMG channels
* 6 target gesture classes
* two recording series per subject

## Methodology

The pipeline includes:

1. Raw EMG loading and validation
2. Signal filtering and time-gap segmentation
3. Windowing with 200 ms windows and 50% overlap
4. Feature extraction using MAV and MDF for each EMG channel
5. Global subject-independent model training
6. Personalized few-shot calibration
7. Per-subject evaluation and statistical comparison

## Models

The benchmark compares several models:

* Logistic Regression
* Random Forest
* MLP Neural Network
* 1D-CNN on raw EMG windows

## Evaluation Metrics

The main evaluation metrics are:

* Accuracy
* Macro-F1
* Balanced Accuracy
* Per-subject Macro-F1
* Bootstrap confidence intervals
* Win rate of personalized models over global baselines
* Inference time per EMG window

Additional analysis includes drift score estimation between recording sessions and statistical comparison using Wilcoxon signed-rank test and McNemar test.

## Key Results

The best global model was a 1D-CNN trained on raw EMG windows, reaching approximately 0.81 Macro-F1 on unseen users.

Personalized models showed stronger performance after short calibration. With 20 samples per class, a personalized Random Forest achieved approximately 0.90 Macro-F1 and outperformed the best global baseline for 5 out of 8 test users. With 40 samples per class, personalized Logistic Regression achieved the best overall result, reaching approximately 0.91 Macro-F1.
