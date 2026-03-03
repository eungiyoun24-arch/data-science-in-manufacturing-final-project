# Data Science in Manufacturing (ME 453) Final Project

This project implements an automated pipeline to monitor and classify the quality of ultrasonic welding processes using Power and Force signals. It covers the entire data science workflow: from raw signal preprocessing and feature engineering to statistical validation and machine learning classification.

## Project Overview
Ultrasonic welding is a high-frequency process where quality is critical. This repository demonstrates how to:
1. Signal Preprocessing: Automatically detect the main-weld region from noisy raw data.
2. Feature Extraction: Generate meaningful features from both time and frequency domains.
3. Statistical Analysis: Rank features using Fisher Ratio to identify the most informative sensors.
4. Machine Learning: Build and evaluate LDA, QDA, and KNN models to predict weld quality (Cold, Good, Excessive).

---

## Data Processing and Feature Engineering

### 1. Main-Weld Detection
Raw signals contain pre-weld and post-weld noise. I implemented automated segmentation using a Savgol filter for smoothing and sliding variance to pinpoint the high-energy welding phase.

### 2. Feature Extraction Groups
Features were engineered across three categories to capture the physics of the process:
* Group A (Process): Physical variables like pressure and height change.
* Group B (Power - Time Domain): Statistical moments (mean, max, std) and energy via trapezoidal integration.
* Group C (Force - Frequency Domain): Spectral analysis via FFT to identify peak frequencies and magnitudes.

---

## Statistical Analysis and Feature Selection

### Fisher Ratio Analysis
To determine which features best separate the quality classes, I calculated the Fisher Ratio for each feature.
* Finding: Power-based features (P_max, P_std, P_energy) showed significantly higher Fisher Ratios than force features.
* Sensor Conclusion: The power sensor is more sensitive to welding quality variations, making it the primary choice for real-time monitoring.

### Statistical Process Control (SPC)
I established control limits (LCL and UCL) based on the +/- 3-sigma distribution of good welds.

---

## Machine Learning Classification

### Feature Selection
I used SequentialFeatureSelector (forward selection) with a greedy algorithm to find the optimal feature subset, reducing dimensionality while maintaining high accuracy.
* Selected Features: Feature 1, Feature 7, Feature 8

### Model Performance
Three models were trained and tested on a 70/30 split. The results indicate high separability in the feature space:

| Model | Accuracy |
| :--- | :--- |
| LDA (Linear Discriminant Analysis) | 1.00 |
| KNN (K-Nearest Neighbors) | 1.00 |
| QDA (Quadratic Discriminant Analysis) | 0.90 |

---

## Evaluation
The models were evaluated using normalized confusion matrices and class prediction error plots to ensure robustness across all three quality classes.

---

## Skills
* Language: Python
* Data Analysis: Pandas, NumPy
* Signal Processing: Scipy (Savgol filter, FFT)
* Machine Learning: Scikit-learn, Mlxtend
* Visualization: Matplotlib, Yellowbrick

---
