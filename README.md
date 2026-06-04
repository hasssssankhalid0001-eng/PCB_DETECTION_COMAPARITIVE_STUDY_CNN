# PCB Defect Classification: A Comparative Study of CNN and Transfer Learning Approaches

## Project Motivation

Automated Printed Circuit Board (PCB) inspection is a critical problem in modern electronics manufacturing. Defects such as missing holes, open circuits, shorts, spurs, and spurious copper can significantly impact product reliability and lead to costly failures.

The objective of this project was to investigate whether deep learning-based image classification techniques could accurately identify different PCB defect categories from high-resolution PCB images.

Rather than focusing solely on model accuracy, this project emphasizes the complete machine learning workflow, including dataset analysis, model development, transfer learning, evaluation, failure analysis, and technical interpretation of results.

---

## Research Question

Can modern deep learning models successfully classify PCB defect types when trained on full-board PCB images?

To answer this question, multiple architectures were implemented and evaluated under identical conditions.

---

## Dataset Overview

### Dataset Characteristics

- Total Images: 693
- Number of Classes: 6
- Images per Class: ~115
- Original Resolution: ~3034 × 1586 pixels
- Color Format: RGB

### Defect Categories

- Missing Hole
- Mouse Bite
- Open Circuit
- Short
- Spur
- Spurious Copper

A key characteristic of this dataset is that the actual defect occupies only a very small region of the overall PCB image.

---

## Exploratory Data Analysis (EDA)

Before model development, the dataset was thoroughly analyzed:

✔ Class distribution analysis

✔ Image resolution inspection

✔ Image format verification

✔ Dataset balance validation

✔ Visualization of defect samples

The dataset was found to be nearly balanced across all six classes.

---

## Methodology

### 1. Data Preprocessing

The following preprocessing pipeline was implemented:

- Image resizing to 224×224
- Pixel normalization
- Data augmentation:
  - Rotation
  - Width shifting
  - Height shifting
  - Zoom augmentation
- 80/20 train-validation split

---

## Model 1: Custom CNN Baseline

A custom Convolutional Neural Network was designed and trained from scratch.

### Architecture

- Conv2D (32 filters)
- Batch Normalization
- Max Pooling

- Conv2D (64 filters)
- Batch Normalization
- Max Pooling

- Conv2D (128 filters)
- Batch Normalization
- Max Pooling

- Global Average Pooling
- Dense Layer (128 neurons)
- Dropout (0.5)
- Softmax Output Layer

### Objective

Establish a baseline performance benchmark before introducing transfer learning.

---

## Model 2: MobileNetV2 Transfer Learning

To determine whether pretrained visual representations could improve performance, MobileNetV2 pretrained on ImageNet was utilized.

### Transfer Learning Strategy

- ImageNet pretrained weights
- Feature extractor frozen
- Custom classification head added
- MobileNetV2-specific preprocessing
- Early stopping for training stabilization

### Advantages

- Reduced trainable parameters
- Faster convergence
- Access to pretrained visual features learned from millions of images

---

## Evaluation Metrics

Models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix
- Classification Report

This provides a more complete understanding of model behavior than accuracy alone.

---

## Experimental Results

### Baseline CNN

The baseline CNN failed to achieve meaningful class separation and performed close to random guessing.

### MobileNetV2

Despite transfer learning, MobileNetV2 also failed to significantly outperform the baseline model.

Observed validation accuracy remained approximately:

16–19%

which is close to the theoretical random-guessing accuracy for a 6-class problem:

1/6 = 16.67%

Classification reports showed strong prediction bias toward a single class while failing to generalize across the remaining categories.

---

## Failure Analysis

One of the primary goals of this project was understanding why the models failed.

### Key Observation

The original PCB images have a resolution of approximately:

3034 × 1586

However, deep learning models required resizing to:

224 × 224

for training.

### Technical Challenge

The actual defect often occupies only a tiny portion of the PCB image.

As a result:

Original PCB Image
→ Resize to 224×224
→ Defect region becomes extremely small
→ Critical visual information is lost

This significantly limits the model's ability to learn meaningful defect-specific features.

### Evidence

Both:

- CNN trained from scratch
- MobileNetV2 transfer learning

failed despite having very different learning mechanisms.

This suggests the primary bottleneck is not model architecture but information loss during preprocessing.

---

## Key Lessons Learned

This project provided practical experience with:

- Computer Vision pipelines
- Convolutional Neural Networks
- Transfer Learning
- MobileNetV2
- Data Augmentation
- Model Evaluation
- Error Analysis
- Failure Investigation
- Research-Oriented Machine Learning Workflow

Most importantly, it highlighted an important machine learning principle:

Better architectures cannot compensate for the loss of critical information during preprocessing.

---

## Future Work

Several directions could significantly improve performance:

### Defect Localization

Detect defect coordinates before classification.

### Patch-Based Classification

Train on cropped defect regions instead of full PCB images.

### Object Detection Models

- YOLO
- Faster R-CNN
- SSD

### High-Resolution Processing

Preserve defect details by training on image patches or larger input resolutions.

### Segmentation Approaches

Use segmentation networks to isolate defect regions before classification.

---

## Project Significance

Although high classification accuracy was not achieved, the project successfully demonstrates:

- End-to-end machine learning development
- Comparative model experimentation
- Transfer learning implementation
- Quantitative evaluation
- Technical debugging
- Failure analysis and interpretation

The project serves as a practical case study showing that understanding model limitations is often as valuable as achieving high accuracy.

---

## Technologies Used

- Python
- TensorFlow
- Keras
- NumPy
- Matplotlib
- Scikit-Learn
- Jupyter Notebook

---

## Author

Mohammad Hassan Khalid

B.Tech Electrical & Computer Engineering

Jamia Millia Islamia

Focused on Machine Learning, Deep Learning, and Applied AI Research.
