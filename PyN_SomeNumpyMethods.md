# Some numpy methods

- [Some numpy methods](#some-numpy-methods)
  - [`arange`](#arange)
  - [`linspace`](#linspace)
  - [Transposing Arrays and Swapping Axes](#transposing-arrays-and-swapping-axes)
  - [`concatenate`](#concatenate)
  - [`tile`](#tile)
  - [`np.nan_to_num`](#npnan_to_num)
  - [`np.quantile`](#npquantile)
  - [`np.nanmean`](#npnanmean)
  - [Calculating the range](#calculating-the-range)
  - [`any`, `all`](#any-all)
  - [Set methods](#set-methods)
    - [`numpy.unique`](#numpyunique)
    - [`numpy.isin`](#numpyisin)
  - [Mathematical and Statistical Methods](#mathematical-and-statistical-methods)
    - [List of some mathematical and statistical methods](#list-of-some-mathematical-and-statistical-methods)
    - [`sum`, `mean`](#sum-mean)
    - [`cumsum`, `cumprod`](#cumsum-cumprod)
    - [`std`](#std)

---

---

## `arange`

`numpy.arange` is an array-valued version of the built-in Python `range` function:

```py
import numpy as np

print(list(range(5))) # [0, 1, 2, 3, 4]
print(np.arange(5)) # [0 1 2 3 4]
```

---

---

## `linspace`

`numpy.linspace` also creates an array. It accepts the beginning and ending numbers, and how many numbers should be between the beginning and ending numbers:

```py
import numpy as np

print(np.linspace(3, 27, 9)) # [ 3.  6.  9. 12. 15. 18. 21. 24. 27.]
```

---

---

## Transposing Arrays and Swapping Axes

Transposing is a special form of reshaping that returns a view on the underlying data without copying anything. Arrays have the `transpose` method and the special `T` attribute:

```py
import numpy as np

arr = np.arange(20).reshape((4, 5))

print(arr)
"""
[[ 0  1  2  3  4]
 [ 5  6  7  8  9]
 [10 11 12 13 14]
 [15 16 17 18 19]]
"""

print(arr.T)
"""
[[ 0  5 10 15]
 [ 1  6 11 16]
 [ 2  7 12 17]
 [ 3  8 13 18]
 [ 4  9 14 19]]
"""

print(arr.transpose())
"""
[[ 0  5 10 15]
 [ 1  6 11 16]
 [ 2  7 12 17]
 [ 3  8 13 18]
 [ 4  9 14 19]]
"""
```

---

---

## `concatenate`

`numpy.concatenate` is essential for joining two or more arrays along a specified axis.

Here is an example of joining two ndarrays by row:

```py
import numpy as np

a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6]])

print(a)
"""
[[1 2]
 [3 4]]
"""

print(b)
"""
[[5 6]]
"""

print(np.concatenate((a, b), axis=0))
"""
[[1 2]
 [3 4]
 [5 6]]
"""
```

Here is an example of joining two ndarrays by column:

```py
import numpy as np

a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6]])

print(a)
"""
[[1 2]
 [3 4]]
"""

print(b.T)
"""
[[5]
 [6]]
"""

print(np.concatenate((a, b.T), axis=1))
"""
[[1 2 5]
 [3 4 6]]
"""
```

Here is an example of joining two ndarrays, and flattening them into a one dimensional ndarray:

```py
import numpy as np

a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6]])

print(a)
"""
[[1 2]
 [3 4]]
"""

print(b)
"""
[[5 6]]
"""

print(np.concatenate((a, b.T), axis=None)) # [1 2 3 4 5 6]
```

---

---

## `tile`

The `tile` method constructs an array by repeating an array the number of given times:

```py
import numpy as np

a = np.array([0, 1, 2])

np.tile(a, 2) # array([0, 1, 2, 0, 1, 2])

np.tile(a, (2, 2))
"""
array([[0, 1, 2, 0, 1, 2],
       [0, 1, 2, 0, 1, 2]])
"""

np.tile(a, (2, 1, 2))
"""
array([[[0, 1, 2, 0, 1, 2]],
       [[0, 1, 2, 0, 1, 2]]])
"""

b = np.array([[1, 2], [3, 4]])

np.tile(b, 2)
"""
array([[1, 2, 1, 2],
       [3, 4, 3, 4]])
"""

np.tile(b, (2, 1))
"""
array([[1, 2],
       [3, 4],
       [1, 2],
       [3, 4]])
"""

c = np.array([1,2,3,4])

np.tile(c,(4,1))
"""
array([[1, 2, 3, 4],
       [1, 2, 3, 4],
       [1, 2, 3, 4],
       [1, 2, 3, 4]])
"""
```

---

---

## `np.nan_to_num`

The `np.nan_to_num` function turns `NaN` into 0 and `inf`/`-inf` into specified numbers.

```py
import numpy as np

# Create an array with NaN and inf values
arr = np.array([1, 2, np.nan, np.inf, -np.inf, 4, np.nan])

# Replace NaN values with 0 and inf values with 0
arr = np.nan_to_num(arr, posinf=100, neginf=0)

print(arr) # [  1.   2.   0. 100.   0.   4.   0.]
```

---

---

## `np.quantile`

```py
import numpy as np

numbers = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
quantiles = np.quantile(numbers, [0.25, 0.5, 0.75])
print(quantiles)  # [3.25 5.5  7.75]
```

---

---

## `np.nanmean`

For statistics of arrays which include nan’s, numpy has a number of functions starting with nan... These remove the nan-values from a sample before executing any other computation. For example, `np.nanmean`:

```py
import numpy as np

x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
np.mean(x) # np.float64(4.5)

xWithNan = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, np.nan]
np.mean(xWithNan) # np.float64(nan)

np.nanmean(xWithNan) # np.float64(4.5)
```

---

---

## Calculating the range

The range is simply the difference between the highest and the lowest data value, and can be found with `np.ptp` (ptp stands for “peak-to-peak”):

```py
import numpy as np

x = np.arange(1, 101)
print(np.ptp(x)) # 99
```

---

---

## `any`, `all`

`any` and `all`, are useful especially for Boolean arrays.

- `any` tests whether one or more values in an array is `True`,
- while `all` checks if every value is `True`:

```py
import numpy as np

bools = np.array([False, False, True, False])

print(bools.any()) # True
print(bools.all()) # False
```

These methods also work with non-Boolean arrays, where nonzero elements are treated as `True`.

```py
import numpy as np

arr = np.array([1, 2, 3, 4])

print((arr > 2).any())
print((arr > 0).all())
```

---

---

## Set methods

See below table for a listing of array set operations in NumPy.

| Method              | Description                                                                        |
| ------------------- | ---------------------------------------------------------------------------------- |
| `unique(x)`         | Compute the sorted, unique elements in `x`                                         |
| `intersect1d(x, y)` | Compute the sorted, common elements in `x` and `y`                                 |
| `union1d(x, y)`     | Compute the sorted union of elements                                               |
| `in1d(x, y)`        | Compute a Boolean array indicating whether each element of `x` is contained in `y` |
| `setdiff1d(x, y)`   | Set difference, elements in `x` that are not in `y`                                |
| `setxor1d(x, y)`    | Set symmetric differences; elements that are in either of the arrays, but not both |

---

### `numpy.unique`

NumPy has some basic set operations for one-dimensional ndarrays. A commonly used one is `numpy.unique`, which returns the sorted unique values in an array:

```py
import numpy as np

names = np.array(["Bob", "Will", "Joe", "Bob", "Will", "Joe", "Joe"])
print(np.unique(names)) # ['Bob' 'Joe' 'Will']
```

---

### `numpy.isin`

Another function, `numpy.isin`, tests if the values in one array is present in another array, returning a Boolean array:

```py
import numpy as np

values = np.array([6, 0, 0, 3, 2, 5, 6])
print(np.isin(values, [2, 3, 6])) # [ True False False  True  True False  True]
```

---

---

## Mathematical and Statistical Methods

Numpy provides a set of mathematical functions that compute statistics about an entire array or about the data along an axis. You can use aggregations (sometimes called reductions) like `sum`, `mean`, and `std` (standard deviation) either by calling the array instance method or using the top-level NumPy function.

---

### List of some mathematical and statistical methods

Here is a table of basic array statistical methods

| Method             | Description                                                                          |
| ------------------ | ------------------------------------------------------------------------------------ |
| `sum`              | Sum of all the elements in the array or along an axis; zero-length arrays have sum 0 |
| `mean`             | Arithmetic mean; invalid (returns `NaN`) on zero-length arrays                       |
| `std`, `var`       | Standard deviation and variance, respectively                                        |
| `min`, `max`       | Minimum and maximum                                                                  |
| `argmin`, `argmax` | Indices of minimum and maximum elements, respectively                                |
| `cumsum`           | Cumulative sum of elements starting from 0                                           |
| `cumprod`          | Cumulative product of elements starting from 1                                       |

---

### `sum`, `mean`

```py
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

print(arr.mean()) # 3.0
print(np.mean(arr)) # 3.0

print(arr.sum()) # 15
print(np.sum(arr)) # 15
```

Functions like `mean` and `sum` take an optional axis argument that computes the statistic over the given axis, resulting in an array with one less dimension:

```py
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])

print(arr)
"""
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]]
"""

# compute sum across the rows
print(arr.sum(axis=0)) # [ 7 9 11 13 15]

# compute sum across the columns
print(arr.sum(axis=1)) # [15 40]
```

`sum` is often used as a means of counting `True` values in a Boolean array. In the below example, boolean values are coerced to 1 (`True`) and 0 (`False`):

```py
import numpy as np

arr = np.array([[1, -2, 3, -4, 5], [-6, 7, -8, 9, 10]])

print((arr > 0).sum()) # 6
```

---

### `cumsum`, `cumprod`

Other methods like `cumsum` and `cumprod` do not aggregate, instead producing an array of the intermediate results:

```py
import numpy as np

arr = np.array([1, 2, 3, 4])

print(arr.cumsum()) # [ 1,  3,  6, 10]
print(arr.cumprod()) # [ 1,  2,  6, 24]
```

The expression `arr.cumsum(axis=0)` computes the cumulative sum along the rows, while `arr.cumsum(axis=1)` computes the sums along the columns:

```py
import numpy as np

arr = np.array([[0, 1, 2], [3, 4, 5], [6, 7, 8]])

print(arr)
"""
[[0 1 2]
 [3 4 5]
 [6 7 8]]
"""

# compute cumulative sum across rows
print(arr.cumsum(axis=0))
"""
[[ 0  1  2]
 [ 3  5  7]
 [ 9 12 15]]
"""

# compute cumulative sum across columns
print(arr.cumsum(axis=1))
"""
[[ 0  1  3]
 [ 3  7 12]
 [ 6 13 21]]
"""
```

---

### `std`

When calculating variance and standard deviation in Python, numpy uses the parameter (n-ddof) in the divisor to distinguish between population- and sample-parameters. "ddof" stands for “delta degrees of freedom”.

Attention: In numpy the default value for ddof in the calculation of variance and standard deviation is set to `ddof=0`, while in pandas the default is `ddof=1`!

```py
import numpy as np
import pandas as pd

data = np.arange(7, 14)
print(data) # [ 7  8  9 10 11 12 13]

print(np.std(data, ddof=0)) # np.float64(2.0)
print(np.std(data)) # np.float64(2.0)

print(np.std(data, ddof=1)) # np.float64(2.160246899469287)

df = pd.DataFrame(data)
print(df.std())
"""
0    2.160247
dtype: float64
"""
```

---

---
