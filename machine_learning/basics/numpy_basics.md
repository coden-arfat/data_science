# NumPy Basics

## 1. Import and Create Arrays

```python
import numpy as np

# Create arrays
a = np.array([1, 2, 3])           # 1D array
b = np.array([[1, 2], [3, 4]])    # 2D array (matrix)
c = np.zeros((3, 3))              # Matrix of zeros
d = np.ones((2, 4))               # Matrix of ones
e = np.random.randn(5, 5)         # Random values
```

## 2. Array Properties

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

arr.shape          # (2, 3) — dimensions
arr.dtype          # data type (int, float, etc.)
arr.ndim           # number of dimensions
arr.size           # total number of elements
len(arr)           # number of rows
```

## 3. Indexing and Slicing

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

arr[0]             # First row → [1, 2, 3]
arr[0, 1]          # Element at row 0, col 1 → 2
arr[:, 0]          # First column → [1, 4]
arr[0:1, 1:3]      # Submatrix
```

## 4. Basic Operations

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

a + b              # Element-wise addition
a * b              # Element-wise multiplication
a @ b              # Dot product (scalar)
a.T                # Transpose
```

## 5. Matrix Operations

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

A @ B              # Matrix multiplication
np.dot(A, B)       # Same as A @ B
np.linalg.inv(A)   # Inverse
np.linalg.det(A)   # Determinant
A.T                # Transpose
```

## 6. Useful Functions

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

np.sum(arr)        # Sum all elements
np.mean(arr)       # Average
np.max(arr)        # Maximum
np.min(arr)        # Minimum
np.linalg.norm(arr) # Frobenius norm (magnitude)
np.reshape(arr, (3, 2))  # Change shape
```

## 7. SVD (Singular Value Decomposition)

```python
A = np.array([[1, 2], [3, 4], [5, 6]], dtype=float)

U, S, Vt = np.linalg.svd(A, full_matrices=False)

print("U shape:", U.shape)     # Left singular vectors
print("S:", S)                 # Singular values
print("Vt shape:", Vt.shape)   # Right singular vectors

# Reconstruct original matrix
A_reconstructed = U @ np.diag(S) @ Vt
```

## 8. Quick Cheat Sheet

| Operation | Code |
|---|---|
| Create array | `np.array([1,2,3])` |
| Zeros matrix | `np.zeros((m, n))` |
| Ones matrix | `np.ones((m, n))` |
| Random matrix | `np.random.randn(m, n)` |
| Matrix multiply | `A @ B` |
| Transpose | `A.T` |
| Inverse | `np.linalg.inv(A)` |
| Determinant | `np.linalg.det(A)` |
| SVD | `np.linalg.svd(A)` |
| Get shape | `arr.shape` |
| Sum | `np.sum(arr)` |
| Mean | `np.mean(arr)` |

