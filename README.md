# Hyperspectral Image Classification on Indian Pines  
*Least-Square Denoising + ADMM-Based Sparse Representation*

---

## Overview
This project investigates hyperspectral image classification on the **Indian Pines dataset**, focusing on improving robustness and accuracy through **explicit denoising and sparse representation**.  
Rather than relying on black-box models, the pipeline is grounded in **signal processing and optimization principles**.

---

## Problem Motivation
Hyperspectral images provide rich spectral information across hundreds of bands, but practical challenges limit classification performance:

- Sensor noise and atmospheric interference
- Redundant and low-information spectral bands
- High dimensionality with limited labeled samples

Without proper preprocessing, these factors severely degrade pixel-wise classification accuracy.

---

## Dataset Preprocessing
To ensure reliable spectral information, the dataset was carefully cleaned and prepared:

- **Dead band removal**  
  Bands with near-zero mean or negligible variance were discarded.
- **Water absorption band removal**  
  Spectral bands affected by atmospheric absorption were excluded.
- **Normalization**  
  Spectral values were scaled to a consistent range for fair comparison.
- **Reshaping**  
  The data cube was transformed from 3D (rows × columns × bands) to a 2D matrix (pixels × bands).

This preprocessing ensured that only informative and physically meaningful bands were retained.

---

## Least-Square Spectral Denoising
Noise reduction was performed using **Least-Square (LS) denoising**, applied directly to the spectral domain.

- Reduces additive noise while preserving spectral shape
- Avoids over-smoothing critical class-discriminative features
- Maintains consistency across neighboring spectral bands

### Validation
Denoising quality was evaluated using:
- Root Mean Squared Error (RMSE)
- Spectral Angle measures

These metrics confirmed that spectral signatures were preserved with minimal distortion.

---

## Sparse Representation & Classification
Classification was performed using **sparse coding solved via ADMM**.

### Training–Testing Strategy
- 20% of samples per class used for training
- 80% reserved for testing
- Class-wise splitting ensured balanced representation

Training samples formed a **dictionary of spectral signatures**, while test samples were treated as unknown spectra.

---

### ADMM-Based Sparse Coding
For each test pixel:

- Sparse coefficients were computed with respect to the training dictionary
- ADMM iteratively enforced:
  - Sparsity of coefficients
  - Consistency with observed spectra
- Resulting representations were highly sparse, activating only a few relevant atoms

This highlighted the most discriminative class-specific signatures.

---

## Residual-Based Decision Rule
Classification was based on **reconstruction residuals**:

- Each class reconstructed the test spectrum using only its coefficients
- Reconstruction error was computed per class
- The class yielding the **minimum residual** was assigned as the label

This decision rule makes the classifier robust to noise and irrelevant features.

---

## Key Results & Insights
- LS denoising significantly improves spectral reliability
- Sparse representation emphasizes class-specific information
- ADMM provides efficient and stable optimization
- The combined pipeline yields **robust and accurate classification** on Indian Pines

---

## Why This Approach Matters
This project demonstrates that:
- Careful signal preprocessing can rival complex models
- Sparse optimization offers interpretability and robustness
- First-principles methods remain highly effective for hyperspectral analysis

---

## Core Concepts Used
- Hyperspectral image processing
- Least-Square denoising
- Sparse representation
- L1 optimization
- Alternating Direction Method of Multipliers (ADMM)
- Residual-based classification

---

## Takeaway
A principled combination of **denoising + sparse modeling** can effectively handle the noise, redundancy, and high dimensionality of hyperspectral data—without resorting to black-box learning models.
