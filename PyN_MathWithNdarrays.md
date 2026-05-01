# Math with Ndarrays

- [Math with Ndarrays](#math-with-ndarrays)
  - [Math between 2 ndarrays](#math-between-2-ndarrays)
  - [Math between an ndarray and a single value](#math-between-an-ndarray-and-a-single-value)
  - [Comparisons between ndarrays](#comparisons-between-ndarrays)
  - [Linear Algebra](#linear-algebra)
    - [Matrix multiplication with `dot` or `@`](#matrix-multiplication-with-dot-or-)
    - [Finding inverse and determinant of a matrix](#finding-inverse-and-determinant-of-a-matrix)

---

---

Arrays enable you to express batch operations on data without writing any `for` loops. NumPy users call this **vectorization**.

---

---

## Math between 2 ndarrays

Any arithmetic operations between equal-size arrays apply the operation element-wise:

```py
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr)
"""
[[1 2 3]
 [4 5 6]]
"""

print(arr * arr)
"""
[[ 1  4  9]
 [16 25 36]]
"""

print(arr - arr)
"""
[[0 0 0]
 [0 0 0]]
"""
```

---

---

## Math between an ndarray and a single value

If we do an arithmetic operation using a scalar (single value data type) and an array, the operation will be applied to every array item:

```py
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr)
"""
[[1 2 3]
 [4 5 6]]
"""

print(10 * arr)
"""
[[10 20 30]
 [40 50 60]]
"""
```

---

---

## Comparisons between ndarrays

Comparisons between arrays of the same size yield Boolean arrays:

```py
import numpy as np

arr1 = np.array([[1, 2, 3], [4, 5, 6]])
arr2 = np.array([[1, 3, 2], [6, 5, 4]])

print(arr1 > arr2)
"""
[[False False  True]
 [False False  True]]
"""
```

---

---

## Linear Algebra

Here is a table of commonly used `numpy.linalg` functions

| Function | Description                                                                                                                                                |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `diag`   | Return the diagonal (or off-diagonal) elements of a square matrix as a 1D array, or convert a 1D array into a square matrix with zeros on the off-diagonal |
| `dot`    | Matrix multiplication                                                                                                                                      |
| `trace`  | Compute the sum of the diagonal elements                                                                                                                   |
| `det`    | Compute the matrix determinant                                                                                                                             |
| `eig`    | Compute the eigenvalues and eigenvectors of a square matrix                                                                                                |
| `inv`    | Compute the inverse of a square matrix                                                                                                                     |
| `pinv`   | Compute the Moore-Penrose pseudoinverse of a matrix                                                                                                        |
| `qr`     | Compute the QR decomposition                                                                                                                               |
| `svd`    | Compute the singular value decomposition (SVD)                                                                                                             |
| `solve`  | Solve the linear system Ax = b for x, where A is a square matrix                                                                                           |
| `lstsq`  | Compute the least-squares solution to Ax = b                                                                                                               |

---

### Matrix multiplication with `dot` or `@`

Multiplying two two-dimensional arrays with `*` is an element-wise product, while matrix multiplications require either using the `dot` function or the `@` infix operator:

```py
import numpy as np

x = np.array([[1., 2., 3.], [4., 5., 6.]])
y = np.array([[6., 23.], [-1, 7], [8, 9]])

print(x)
"""
[[1. 2. 3.]
 [4. 5. 6.]]
"""

print(y)
"""
[[ 6. 23.]
 [-1.  7.]
 [ 8.  9.]]
"""

print(x.dot(y))
"""
[[ 28.  64.]
 [ 67. 181.]]
"""
```

`dot` is both an array method and a function in the numpy namespace for doing matrix multiplication. Instead of `x.dot(y)`, we can also use `np.dot(x, y)`:

```py
import numpy as np

x = np.array([[1., 2., 3.], [4., 5., 6.]])
y = np.array([[6., 23.], [-1, 7], [8, 9]])

print(x)
"""
[[1. 2. 3.]
 [4. 5. 6.]]
"""

print(y)
"""
[[ 6. 23.]
 [-1.  7.]
 [ 8.  9.]]
"""

print(np.dot(x, y))
"""
[[ 28.  64.]
 [ 67. 181.]]
"""
```

In NumPy, the `@` infix operator also means matrix multiplication.

```py
import numpy as np

x = np.array([[1., 2., 3.], [4., 5., 6.]])
y = np.array([[6., 23.], [-1, 7], [8, 9]])

print(x)
"""
[[1. 2. 3.]
 [4. 5. 6.]]
"""

print(y)
"""
[[ 6. 23.]
 [-1.  7.]
 [ 8.  9.]]
"""

print(x @ y)
"""
[[ 28.  64.]
 [ 67. 181.]]
"""
```

One more way to calculate a matrix multiplication is to use the `np.matmul()` method:

```py
import numpy as np

x = np.array([[1., 2., 3.], [4., 5., 6.]])
y = np.array([[6., 23.], [-1, 7], [8, 9]])

print(x)
"""
[[1. 2. 3.]
 [4. 5. 6.]]
"""

print(y)
"""
[[ 6. 23.]
 [-1.  7.]
 [ 8.  9.]]
"""

print(np.matmul(x, y))
"""
[[ 28.  64.]
 [ 67. 181.]]
"""
```

---

### Finding inverse and determinant of a matrix

`numpy.linalg` has a standard set of matrix decompositions and things like inverse and determinant:

````py
import numpy as np
from numpy.linalg import inv

rng = np.random.default_rng(seed=12345)
X = rng.standard_normal((5, 5))

print(inv(X))
print(X @ inv(X))
```                                                                                                          |

---

---
````
