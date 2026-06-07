# p_project1

This project contains data science and machine learning work for `p_project1`.

## Overview

- Purpose: Document the structure, goals, and usage of `p_project1`.
- Contents: Add notebooks, scripts, datasets, and analysis as needed.

## Getting Started

1. Clone the repository.
2. Navigate to `machine_learning/p_project1`.
3. Install dependencies if required.
4. Run notebooks or Python scripts.

## Project 1 Complete Guide

Perfect — you know Python and Linux, so environment setup will be smooth. Let me give you a complete beginner-friendly step-by-step guide for Project 1.

---

# Project 1 Complete Guide
## SVD-Based Signal/Image Analysis

---

## STEP 1: Environment Setup

Since you're on Linux, open your terminal and run these one by one:

```bash
# Create a dedicated project folder
mkdir project1_svd
cd project1_svd

# Create a virtual environment
python3 -m venv venv

# Activate it
source venv/bin/activate

# Install required libraries
pip install numpy matplotlib scikit-image jupyter
```

Then launch your workspace:

```bash
jupyter notebook
```

Create a new notebook called `project1_svd.ipynb`

---

## STEP 2: Understand What You Are Building

Before writing a single line of code, understand the goal mentally.

**The idea:** Any matrix (image, signal) can be broken into simpler pieces using SVD. You keep only the most important pieces and throw the rest away. The result is a compressed version.

**EEE analogy:** Think of it like a Fourier Transform. A complex signal is broken into frequency components. You keep the dominant frequencies and discard the noise. SVD does the exact same thing — but for matrices.

The math behind it:

$$A = U \Sigma V^T$$

Where:
- **A** is your original matrix (image or signal)
- **U** contains left singular vectors (patterns in rows)
- **Σ** is a diagonal matrix of singular values (importance of each pattern)
- **V^T** contains right singular vectors (patterns in columns)

You will implement this and *feel* what each piece means.

---

## STEP 3: Phase 1 — Matrix Operations From Scratch

Start your notebook with this. Do not copy blindly — type every line and understand it.

```python
import numpy as np
import matplotlib.pyplot as plt

# ----------------------------
# STEP 3.1: Create a test matrix
# ----------------------------
A = np.array([
    [3, 1, 1],
    [-1, 3, 1]
], dtype=float)

print("Original Matrix A:")
print(A)
print("Shape:", A.shape)
```

Now compute SVD manually using NumPy:

```python
# ----------------------------
# STEP 3.2: Compute SVD
# ----------------------------
U, S, Vt = np.linalg.svd(A, full_matrices=True)

print("\nU matrix (left singular vectors):")
print(U)

print("\nSingular values (S):")
print(S)

print("\nVt matrix (right singular vectors):")
print(Vt)
```

Now reconstruct A from its parts and verify:

```python
# ----------------------------
# STEP 3.3: Reconstruct A and verify
# ----------------------------

# Build full Sigma matrix (same shape as A)
Sigma = np.zeros(A.shape)
Sigma[:min(A.shape), :min(A.shape)] = np.diag(S)

# Reconstruct
A_reconstructed = U @ Sigma @ Vt

print("\nReconstructed A:")
print(A_reconstructed)

print("\nReconstruction error:")
print(np.allclose(A, A_reconstructed)) # Should print True
```

**Checkpoint question before moving on:** What do the singular values in S tell you? Write your answer as a comment in the notebook before continuing.

---

## STEP 4: Phase 2 — Apply SVD to a Real Image

Now we make it real and visual.

```python
# ----------------------------
# STEP 4.1: Load a grayscale image
# ----------------------------
from skimage import data

image = data.camera() # Built-in grayscale image, no download needed
print("Image shape:", image.shape)

plt.imshow(image, cmap='gray')
plt.title("Original Image")
plt.axis('off')
plt.show()
```

Now apply SVD to the image:

```python
# ----------------------------
# STEP 4.2: SVD on the image matrix
# ----------------------------
image_float = image.astype(float)

U, S, Vt = np.linalg.svd(image_float, full_matrices=False)

print("U shape:", U.shape)
print("S shape:", S.shape)
print("Vt shape:", Vt.shape)
print("\nTop 10 singular values:")
print(S[:10])
```

Now compress by keeping only top k components:

```python
# ----------------------------
# STEP 4.3: Compress by keeping top k singular values
# ----------------------------
def compress_image(U, S, Vt, k):
    # Keep only top k components
    U_k = U[:, :k]
    S_k = np.diag(S[:k])
    Vt_k = Vt[:k, :]
    return U_k @ S_k @ Vt_k

# Try different values of k
k_values = [5, 20, 50, 100, 200]

fig, axes = plt.subplots(1, len(k_values) + 1, figsize=(18, 4))

axes[0].imshow(image, cmap='gray')
axes[0].set_title("Original")
axes[0].axis('off')

for i, k in enumerate(k_values):
    compressed = compress_image(U, S, Vt, k)
    axes[i+1].imshow(compressed, cmap='gray')
    axes[i+1].set_title(f"k={k}")
    axes[i+1].axis('off')

plt.suptitle("SVD Image Compression at Different Ranks")
plt.tight_layout()
plt.show()
```

**What you should observe:** At k=5 the image is barely recognizable. At k=200 it looks almost identical to the original. This is the core insight of SVD.

---

## STEP 5: Phase 3 — Visualize and Analyze

```python
# ----------------------------
# STEP 5.1: Plot singular values to see information decay
# ----------------------------
plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.plot(S[:50])
plt.title("Top 50 Singular Values")
plt.xlabel("Index")
plt.ylabel("Value")
plt.grid(True)

plt.subplot(1, 2, 2)
plt.plot(np.cumsum(S) / np.sum(S) * 100)
plt.title("Cumulative Energy Captured (%)")
plt.xlabel("Number of Components")
plt.ylabel("Energy (%)")
plt.axhline(y=90, color='r', linestyle='--', label='90% energy')
plt.axhline(y=99, color='g', linestyle='--', label='99% energy')
plt.legend()
plt.grid(True)

plt.tight_layout()
plt.show()
```

```python
# ----------------------------
# STEP 5.2: Compute reconstruction error vs k
# ----------------------------
errors = []
k_range = range(1, 201, 10)

for k in k_range:
    compressed = compress_image(U, S, Vt, k)
    error = np.linalg.norm(image_float - compressed, 'fro') # Frobenius norm
    errors.append(error)

plt.figure(figsize=(8, 4))
plt.plot(list(k_range), errors, marker='o')
plt.title("Reconstruction Error vs Number of Components")
plt.xlabel("k (components kept)")
plt.ylabel("Frobenius Norm Error")
plt.grid(True)
plt.show()
```

**EEE connection:** The Frobenius norm error is like measuring signal distortion. The more components you keep, the lower the distortion — exactly like increasing bit depth in a DAC.

---

## STEP 6: Stretch Challenge — PCA on a Multi-Feature Dataset

```python
# ----------------------------
# PCA from scratch using SVD
# ----------------------------
from sklearn.datasets import load_iris # Only for data, not for PCA itself

iris = load_iris()
X = iris.data # Shape: (150, 4) — 4 features

# Step 1: Center the data (subtract mean)
X_centered = X - np.mean(X, axis=0)

# Step 2: Apply SVD
U, S, Vt = np.linalg.svd(X_centered, full_matrices=False)

# Step 3: Project onto top 2 principal components
X_pca = X_centered @ Vt[:2].T

# Step 4: Plot
plt.figure(figsize=(7, 5))
for label, color, name in zip([0,1,2], ['red','green','blue'], iris.target_names):
    mask = iris.target == label
    plt.scatter(X_pca[mask, 0], X_pca[mask, 1], c=color, label=name)

plt.title("PCA via SVD — Iris Dataset")
plt.xlabel("Principal Component 1")
plt.ylabel("Principal Component 2")
plt.legend()
plt.grid(True)
plt.show()
```

---

## STEP 7: Final Deliverables Checklist

Before you consider Project 1 complete, make sure you have:

- [ ] SVD computed and verified on a small matrix manually
- [ ] Image compressed and reconstructed at 5 different k values
- [ ] Singular value decay plot showing energy capture
- [ ] Reconstruction error vs k plot
- [ ] PCA stretch challenge completed
- [ ] Every function written by you — no black box library calls for the core math

---

## Summary of What You Learned

| Concept | Where it appeared |
|---|---|
| Vector spaces | U and Vt column spaces |
| Eigenvalues | Singular values in S |
| SVD | Core of every phase |
| Orthogonality | U and Vt are orthogonal matrices |
| Projections | PCA projection in stretch challenge |
| Numpy vectorization | compress_image function |
| Complexity awareness | Why large k is expensive |

## Notes

- Update this README with project-specific instructions, dataset descriptions, and execution steps.
