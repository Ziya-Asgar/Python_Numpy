# Changing Ndarrays

- [Changing Ndarrays](#changing-ndarrays)
  - [Sorting](#sorting)
  - [Changing the array items using boolean arrays](#changing-the-array-items-using-boolean-arrays)
  - [Slicing Ndarrays is not like slicing python lists](#slicing-ndarrays-is-not-like-slicing-python-lists)
  - [Copying ndarrays, partially or fully](#copying-ndarrays-partially-or-fully)
  - [Assigning the items to the whole ndarray](#assigning-the-items-to-the-whole-ndarray)

---

---

## Sorting

Like Python’s built-in list type, NumPy arrays can be sorted in place with the `sort` method:

```py
import numpy as np

arr = np.array([[1, -2, 3, -4, 5], [-6, 7, -8, 9, 10]])

print(arr)
"""
[[ 1 -2  3 -4  5]
 [-6  7 -8  9 10]]
"""

arr.sort()
print(arr)
"""
[[-4 -2  1  3  5]
 [-8 -6  7  9 10]]
"""
```

You can sort each one-dimensional section of values in a multidimensional array in place along an axis by passing the axis number to `sort`. `arr.sort(axis=0)` sorts the values within each column, while `arr.sort(axis=1)` sorts across each row:

```py
import numpy as np

arr = np.array([[1, -2, 3, -4, 5], [-6, 7, -8, 9, 10]])

print(arr)
"""
[[ 1 -2  3 -4  5]
 [-6  7 -8  9 10]]
"""

# sort by row
arr.sort(axis=0)
print(arr)
"""
[[-6 -2 -8 -4  5]
 [ 1  7  3  9 10]]
"""
```

```py
import numpy as np

arr = np.array([[1, -2, 3, -4, 5], [-6, 7, -8, 9, 10]])

print(arr)
"""
[[ 1 -2  3 -4  5]
 [-6  7 -8  9 10]]
"""

# sort by column
arr.sort(axis=1)
print(arr)
"""
[[-4 -2  1  3  5]
 [-8 -6  7  9 10]]
"""
```

Note that the top-level method `numpy.sort` returns a sorted copy of an array (like the Python built-in function `sorted`) instead of modifying the array in place.

---

---

## Changing the array items using boolean arrays

In addition to retrieving data using the boolean indexing, we can also change the values in arrays based on a condition:

```py
import numpy as np

data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

# turn all the negative values to 0
data[data < 0] = 0
print(data)
"""
[[4 7]
 [0 2]
 [0 6]
 [0 0]
 [1 2]
 [0 0]
 [3 4]]
"""
```

Here is another example:

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

data[names == "Joe"] = 100
print(data)
"""
[[  4   7]
 [100 100]
 [ -5   6]
 [  0   0]
 [  1   2]
 [100 100]
 [100 100]]
"""
```

---

---

## Slicing Ndarrays is not like slicing python lists

An important distinction from Python's built-in lists is that array slices are views on the original array. This means that the data is not copied, and any modifications to the view will be reflected in the source array.

```py
import numpy as np

arr = np.arange(10)
print(arr) # [0 1 2 3 4 5 6 7 8 9]

arr_slice = arr[5:8]
print(arr_slice) # [5 6 7]

arr_slice[1] = 100
print(arr_slice) # [  5 100   7]
print(arr) # [  0   1   2   3   4   5 100   7   8   9]

# compare this to built-in Python lists
listVariable = [1, 2, 3, 4]
newList = listVariable[:4]
newList[0] = 10

print(listVariable) # [1, 2, 3, 4]
print(newList) # [10, 2, 3, 4]
```

---

---

## Copying ndarrays, partially or fully

If you want a copy of a slice of an ndarray instead of a view, you will need to explicitly copy using the `copy()` method:

```py
import numpy as np

arr = np.arange(10)
print(arr) # [0 1 2 3 4 5 6 7 8 9]

arr_slice = arr[5:8].copy()
print(arr_slice) # [5 6 7]

arr_slice[1] = 100
print(arr_slice) # [  5 100   7]
print(arr) # [0 1 2 3 4 5 6 7 8 9]
```

---

---

## Assigning the items to the whole ndarray

The assignment for the whole array in a multidimensional ndarray is also possible:

```py
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])

arr[0] = 100
arr[1][0] = 1000

print(arr)
"""
[[[ 100  100  100]
  [ 100  100  100]]

 [[1000 1000 1000]
  [  10   11   12]]]
"""
```

---

---
