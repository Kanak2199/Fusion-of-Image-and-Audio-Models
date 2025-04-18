﻿
# Classification using Fusion of Image and Audio Models

**Author**: Kanak Tiwari  
**Institution**: Texas A&M University  
**Email**: kanaktiwari@tamu.edu  

---

## Overview

This project presents a multimodal deep learning approach for digit classification using the MNIST dataset. Unlike traditional models that rely solely on image data, this work fuses both **image and audio inputs** to significantly enhance classification accuracy. A custom fusion model using **Convolutional Neural Networks (CNNs)** is developed for each modality.

---

## Problem Statement

Real-world applications such as speech-based authentication and voice-controlled interfaces require accurate classification using both visual and auditory cues. This project aims to build a **Fusion Model** that intelligently combines features from both audio and image data for digit classification.

---

## Dataset

- **Image Data**: 28x28 grayscale handwritten digits (0–9)
- **Audio Data**: 507-dimensional vectors of spoken digits
- **Labels**: Integer values 0 through 9

## Methodology

### 1. Data Preprocessing
- Data loaded from `.npy` and `.csv` files
- Normalization attempted but excluded for better results
- Created custom PyTorch `TensorDataset`
- Split into 80% training and 20% validation

### 2. Model Design

#### 🔹 Fusion Model 1:
- **Image**: 2-layer CNN (`CNN2Custom`)
- **Audio**: 1-layer CNN

#### 🔹 Fusion Model 2 (Best Model):
- **Image**: 3-layer CNN (`CNN3Custom`)
- **Audio**: 1-layer CNN

Final output: feature concatenation → fully connected layer → 10-class prediction

### 3. Model Training
- Optimizer: Adam
- Loss: CrossEntropyLoss
- Learning rate: 0.001
- Epochs: 10, Batch Size: 64
- Early stopping based on F1 score (best epoch = 8)

### 4. Hyperparameter Tuning

| Model Variant               | Image CNN Layers | Dropout | Performance |
|----------------------------|------------------|---------|-------------|
| Fusion Model 1 - Comb. 1   | 2                | 0.2     | Good        |
| Fusion Model 1 - Comb. 2   | 2                | 0.5     | Good        |
| Fusion Model 2 - Comb. 1   | 3                | 0.2     | Better      |
| ✅ Fusion Model 2 - Comb. 2 | 3                | 0.5     | **Best**    |

---

## 📊 Results

| Metric             | Value     |
|--------------------|-----------|
| Training Accuracy   | 0.9981    |
| Validation Accuracy | 0.9959    |
| Best Epoch          | 8         |

### Accuracy vs. Epoch Curve
- Both training and validation accuracies improved steadily and stabilized after epoch 8.

---

## 📉 Embedding & Clustering

### 🔹 Image Embeddings
- Dimensionality reduced from 128 → 2 using t-SNE
- Applied K-Means (k=10)
- Clear cluster separation with strong label alignment

### 🔹 Audio Embeddings
- t-SNE results showed overlapping clusters
- K-Means could not clearly separate digit labels

---

## ✅ Test Evaluation

- Fusion Model 2 (Combination 2) tested on 10,000 unseen samples
- First 50 predictions were visualized and classified correctly
- Predictions submitted to Kaggle as CSV file

---

## 🧠 Conclusion

The fusion approach combining CNNs for both image and audio features showed superior accuracy over single-modality models. Best results were achieved using:

- CNN (3-layer) for image
- CNN (1-layer) for audio
- Dropout = 0.5

🔮 **Future Work**: Explore using RNNs for audio data to better capture sequential patterns and improve classification accuracy.

---

## 📚 References

1. Shao, Ma, Zhu, Deng, Zhai. *MNIST Handwritten Digit Classification Using CNNs with Hyperparameter Optimization*. [Link](https://www.researchgate.net/publication/369265604)  
2. Szegedy et al., *GoogLeNet: Going Deeper with Convolutions*. [arXiv](https://arxiv.org/abs/1409.4842v1)  
3. Simonyan & Zisserman, *VGG16: Very Deep Convolutional Networks for Large-Scale Image Recognition*. [arXiv](https://arxiv.org/abs/1409.1556)

---

