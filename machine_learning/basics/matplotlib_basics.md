# Matplotlib Basics

## 1. Basic Plotting

```python
import matplotlib.pyplot as plt

# Simple line plot
x = [1, 2, 3, 4, 5]
y = [1, 4, 9, 16, 25]

plt.plot(x, y)
plt.xlabel("X axis")
plt.ylabel("Y axis")
plt.title("My Plot")
plt.show()
```

## 2. Multiple Lines

```python
x = [1, 2, 3, 4, 5]
y1 = [1, 4, 9, 16, 25]
y2 = [1, 2, 3, 4, 5]

plt.plot(x, y1, label="y = x²")
plt.plot(x, y2, label="y = x")
plt.legend()
plt.show()
```

## 3. Subplots

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot(x, y1)
axes[0].set_title("Plot 1")

axes[1].plot(x, y2)
axes[1].set_title("Plot 2")

plt.tight_layout()
plt.show()
```

## 4. Image Display

```python
import numpy as np
from skimage import data

image = data.camera()  # Load sample image

plt.imshow(image, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')  # Hide axes
plt.show()
```

## 5. Scatter Plot

```python
x = np.random.randn(100)
y = np.random.randn(100)

plt.scatter(x, y, c='red', marker='o', s=50)
plt.title("Scatter Plot")
plt.show()
```

## 6. Histogram

```python
data = np.random.randn(1000)

plt.hist(data, bins=30, edgecolor='black')
plt.title("Histogram")
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.show()
```

## 7. Grid and Styling

```python
x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y, 'b-', linewidth=2, label='sin(x)')
plt.grid(True, alpha=0.3)
plt.legend()
plt.show()
```

## 8. Figure Size and Resolution

```python
plt.figure(figsize=(12, 6))  # Width=12, Height=6 inches

plt.plot(x, y)
plt.dpi = 100  # Dots per inch
plt.show()
```

## 9. Saving Figures

```python
plt.plot(x, y)
plt.savefig('my_plot.png', dpi=300, bbox_inches='tight')
plt.show()
```

## 10. Colormaps

```python
image = data.camera()

plt.imshow(image, cmap='gray')      # Grayscale
plt.imshow(image, cmap='hot')       # Hot colors
plt.imshow(image, cmap='viridis')   # Viridis colormap
plt.show()
```

## 11. Plot Styles and Colors

```python
# Line styles
plt.plot(x, y, 'r-')      # Red solid line
plt.plot(x, y, 'b--')     # Blue dashed line
plt.plot(x, y, 'g:')      # Green dotted line
plt.plot(x, y, 'ko')      # Black circles

# Markers
plt.plot(x, y, marker='o')   # Circle
plt.plot(x, y, marker='s')   # Square
plt.plot(x, y, marker='^')   # Triangle
plt.plot(x, y, marker='*')   # Star
```

## 12. Quick Cheat Sheet

| Task | Code |
|---|---|
| Line plot | `plt.plot(x, y)` |
| Scatter plot | `plt.scatter(x, y)` |
| Histogram | `plt.hist(data, bins=30)` |
| Image display | `plt.imshow(image, cmap='gray')` |
| Multiple subplots | `plt.subplots(rows, cols)` |
| Add title | `plt.title("Title")` |
| Add labels | `plt.xlabel("X"), plt.ylabel("Y")` |
| Add legend | `plt.legend()` |
| Add grid | `plt.grid(True)` |
| Set figure size | `plt.figure(figsize=(w, h))` |
| Save figure | `plt.savefig('filename.png')` |
| Show plot | `plt.show()` |

