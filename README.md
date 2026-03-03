# Sign Language Image Classification using Deep Learning

## Project Overview

This project investigates the feasibility of using **deep learning** to classify **American Sign Language (ASL)** hand gestures into alphabetic characters. The work was completed as **Assignment 3**, simulating a real-world client request to assess whether sign language translation could be supported under **limited computational constraints**.

Using a labeled image dataset similar to MNIST, multiple deep neural network architectures were designed, trained, evaluated, and compared to determine the most effective approach for static ASL letter recognition.

---

## Problem Statement

A client is interested in developing an application that can translate **American Sign Language** into text for users who do not sign, or who sign using different styles or languages.

As a preliminary feasibility assessment:

- Only **static hand gestures** are considered
- Letters **J** and **Z** are excluded (they require motion)
- A strict constraint of **≤ 100 total training runs** applies across all models and hyperparameter choices

---

## Dataset Description

- **Source**: ASL Letter Dataset (MNIST-style CSV format)
- **Image Size**: 28 × 28 grayscale (flattened to 784 features)
- **Classes**: 24 (A–Z excluding J and Z)
- **Training Samples**: 27,454
- **Test Samples**: 7,172
- **Pixel Values**: Normalized to range [0, 1]

Each row consists of:
[label, pixel1, pixel2, ..., pixel784]

---

## Models Implemented

### 1️. Deep Fully Connected Network with Batch Normalization
- 20 Dense layers
- 100 neurons per layer
- He initialization
- Batch Normalization after each Dense layer
- Swish activation
- Softmax output layer (24 classes)

### 2️. Self-Normalizing Network (SELU)
- 20 Dense layers
- 100 neurons per layer
- LeCun normal initialization
- SELU activation
- Dropout (0.1) after every second Dense layer
- Softmax output layer

### 3️. Performance-Scheduled Model
- Retraining of the first model using:
  - Learning-rate scheduling
  - Performance monitoring
- Aimed at improving convergence and generalization

### 4️. Transfer Learning Model
- Based on MobileNet
- Pre-trained weights
- Frozen convolutional base
- Custom Dense layers added for ASL classification

---

## Data Preprocessing Steps

- Removed invalid classes (J and Z)
- Reindexed labels to ensure contiguous class range [0–23]
- Normalized pixel values to [0, 1]
- One-hot encoded class labels
- Applied PowerTransformer (Yeo-Johnson) for models requiring normally distributed inputs
- Visualized sample images for each class

---

## Training Details

- **Optimizer**: Nadam
- **Loss Function**: Categorical Cross-Entropy
- **Metric**: Accuracy
- **Training Environment**: Local machine only (no training on Gradescope)
- **Training Code**: Commented out before submission to avoid re-training

---

## Output Files

The following trained models and histories are included:
- best_dnn_bn_model.keras
- best_dnn_bn_perf_model.keras
- best_dnn_selu_model.keras
- best_mobilenet_model.keras
- history1
- history2
- history1_perf
- historymb

These files allow full reproducibility of results without retraining.

---

## Evaluation & Prediction

- Models were evaluated on unseen test data
- Accuracy comparisons were used to select the best-performing architecture
- The final model was used to:
  - Predict ASL letters
  - Convert predictions into readable text output
 
---

## Model Images

<figure>
  <img width="501" height="156" alt="sign language accuracy" src="https://github.com/user-attachments/assets/d7796170-6340-47c7-b8e9-eef55165dbb6" />
  <figcaption>Figure 1. Image of the accuracy and loss of the transfer learning model</figcaption>
</figure>

<figure>
  <img width="386" height="522" alt="sign language image" src="https://github.com/user-attachments/assets/04b67d04-981c-463d-8d0d-3ab5e99534c7" />
  <figcaption>Figure 2. Image of the model being used to accurately identify the sign language character provided</figcaption>
</figure>

---

## Key Takeaways

- Deep fully connected networks can effectively classify static ASL gestures
- Batch Normalization and SELU significantly improve training stability
- Transfer learning provides strong performance under limited training budgets
- Static gesture recognition is feasible, but motion-based signs require temporal models (e.g. RNNs or video-based CNNs)

---

## Technologies Used

- Python
- TensorFlow / Keras
- NumPy
- Pandas
- Scikit-learn
- Matplotlib / Seaborn
- OpenCV

---

## Notes

- All training was performed locally
- The notebook follows a strict step-by-step structure required by the autograder
- Training cells are commented out to prevent unintended execution
