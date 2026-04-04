# 🌿 Hyperspectral Image Classification (Indian Pines)

**Denoising + Sparse Representation using ADMM**

---

## 📌 Overview

This project focuses on classifying hyperspectral images from the **Indian Pines dataset** using a structured, interpretable pipeline.

Instead of relying on complex black-box models, the approach is built using:

* Signal processing (denoising)
* Optimization techniques (sparse coding with ADMM)

👉 The goal is simple:
**Improve classification accuracy by cleaning the data and using meaningful representations.**

---

## ❓ Why This Problem is Challenging

Hyperspectral images contain hundreds of spectral bands per pixel.
While this gives rich information, it also introduces problems:

* Noise from sensors and environment
* Redundant or useless spectral bands
* Very high dimensional data
* Limited labeled samples

👉 Without proper preprocessing, classification becomes unreliable.

---

## ⚙️ Data Preprocessing

To improve data quality, several steps were applied:

* **Removed dead bands**
  (bands with very low variance or no useful information)

* **Removed water absorption bands**
  (distorted by atmospheric effects)

* **Normalization**
  (scaled all values for consistency)

* **Reshaping**
  Converted 3D data → 2D matrix (pixels × features)

👉 Result: Clean, usable spectral data.

---

## 🔧 Step 1: Least-Square Denoising

Noise was reduced using **Least-Square (LS) denoising**.

### Why LS Denoising?

* Reduces noise without destroying important patterns
* Preserves the shape of spectral signatures
* Keeps class-specific information intact

### Evaluation Metrics:

* RMSE (error reduction)
* Spectral similarity (angle-based)

👉 Conclusion: Noise reduced while preserving useful information.

---

## 🧠 Step 2: Sparse Representation (Core Idea)

Each pixel is represented as a **combination of a few important training samples**.

Instead of using all data:

* Only a **small number of relevant samples (sparse)** are used
* This highlights the most important class-specific patterns

---

## ⚡ Step 3: ADMM Optimization

Sparse representation is solved using:

**ADMM (Alternating Direction Method of Multipliers)**

### Why ADMM?

* Efficient for large-scale problems
* Handles sparsity constraints well
* Converges reliably

👉 It finds the best sparse coefficients for each test pixel.

---

## 🎯 Classification Strategy

Classification is done using a **residual-based method**:

1. Each class tries to reconstruct the test pixel
2. Reconstruction error is calculated
3. The class with the **lowest error** is selected

👉 Intuition:

> The correct class reconstructs the signal better.

---

## 📊 Training Strategy

* 20% samples → Training
* 80% samples → Testing
* Balanced across classes

Training data forms a **dictionary of spectral signatures**.

---

## 🔍 Key Insights

* Denoising improves data reliability significantly
* Sparse representation focuses on important features
* ADMM ensures efficient and stable optimization
* Residual-based classification is robust to noise

---

## 🚀 Why This Approach is Interesting

This project shows that:

* You don’t always need deep learning
* Clean data + smart modeling can perform very well
* Sparse methods provide **interpretability**, not just accuracy

---

## 🧠 Core Concepts Used

* Hyperspectral imaging
* Least-Square denoising
* Sparse representation
* L1 optimization
* ADMM
* Residual-based classification

---

## 📌 Final Takeaway

A well-designed pipeline combining:

> **Denoising + Sparse Modeling + Optimization**

can effectively handle high-dimensional noisy data and produce reliable classification results — without relying on black-box models.
