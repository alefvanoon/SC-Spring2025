# Linear Algebra Web Tools

![Project Screenshot](assets/img/screenshot.png)

A web-based application for performing fundamental linear algebra operations, built for the Scientific Computing course.


## Features

- **Row Echelon Form (REF) Calculator**:
  - Performs Gaussian elimination with partial pivoting
  - Handles matrices of any dimension
  - Cleans up small values to zero for readability

- **Determinant Calculator**:
  - Computes determinants for square matrices
  - Uses NumPy's efficient LU decomposition method
  - Provides accurate results even for large matrices

## Live Demo

The application is hosted on GitHub Pages:  
[View Live Demo](https://alefvanoon.github.io/SC-Spring2025/)

## Technologies Used

- **Frontend**:
  - HTML5, CSS3, JavaScript
  - [Pyodide](https://pyodide.org/) v0.25.1 (Python in WebAssembly)
  
- **Scientific Computing**:
  - [NumPy](https://numpy.org/) for matrix operations
  - Gaussian elimination algorithm


## How to Use

1. **Row Echelon Form**:
   - Enter matrix dimensions (rows and columns)
   - Fill in the matrix values
   - Click "Calculate REF" to see the result

2. **Determinant Calculator**:
   - Enter matrix size (n for n×n matrix)
   - Fill in the matrix values
   - Click "Calculate Determinant" to see the result

## Implementation Highlights

The application runs entirely in the browser using WebAssembly.

Row Echelon Form Algorithm:
```python
import numpy as np

def ref(matrix):
    mat = np.array(matrix, dtype=float)
    rows, cols = mat.shape
    r = 0  # current row index
    tolerance = 1e-10
    
    for c in range(cols):
        if r >= rows: break
            
        # Find pivot row
        pivot_row = r
        for i in range(r, rows):
            if abs(mat[i, c]) > tolerance:
                pivot_row = i
                break
        
        if abs(mat[pivot_row, c]) < tolerance:
            continue
            
        # Swap rows if needed
        if pivot_row != r:
            mat[[r, pivot_row]] = mat[[pivot_row, r]]
        
        # Eliminate below
        for i in range(r + 1, rows):
            factor = mat[i, c] / mat[r, c]
            mat[i] = mat[i] - factor * mat[r]
            
        r += 1
    
    # Clean up small values
    mat = np.where(np.abs(mat) < tolerance, 0, mat)
    return mat.tolist()
```

