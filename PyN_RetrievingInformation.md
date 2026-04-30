# Retrieving Information from Ndarrays

- [Retrieving Information from Ndarrays](#retrieving-information-from-ndarrays)
  - [Retrieving the number of dimensions in an array](#retrieving-the-number-of-dimensions-in-an-array)
  - [Retrieving the items of one-dimensional arrays](#retrieving-the-items-of-one-dimensional-arrays)
  - [Retrieving the items of multi-dimensional arrays](#retrieving-the-items-of-multi-dimensional-arrays)
  - [Using negative indices](#using-negative-indices)
  - [Retrieving Using Multiple Index Arrays](#retrieving-using-multiple-index-arrays)
  - [Retrieving items with Boolean Indexing](#retrieving-items-with-boolean-indexing)
  - [Logical operators with boolean arrays](#logical-operators-with-boolean-arrays)
  - [Retrieving Items in a Custom Order](#retrieving-items-in-a-custom-order)
  - [Retrieving Items of a Lower Dimension-Ndarray in a Custom Order](#retrieving-items-of-a-lower-dimension-ndarray-in-a-custom-order)

---

---

## Retrieving the number of dimensions in an array

The `ndim` attribute tells the number of dimensions of an ndarray:

```py
import numpy as np

data = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr = np.array(data)

print(arr.ndim) # 2
```

The `shape` attribute returns a tuple indicating the number of dimensions and the size of each dimension:

```py
import numpy as np

data = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr = np.array(data)

print(arr.ndim) # 2
print(arr.shape) # (2, 4)
```

---

---

## Retrieving the items of one-dimensional arrays

Accessing the items of one-dimensional arrays is simple. It is similar to Python lists:

```py
import numpy as np

arr = np.arange(10)
print(arr) # [0 1 2 3 4 5 6 7 8 9]

print(arr[5]) # 5
print(arr[5:8]) # [5 6 7]
```

---

---

## Retrieving the items of multi-dimensional arrays

If we have 2 or higher-dimensional arrays, we can use more square brackets to access deep array items:

```py
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(arr)
"""
[[1 2 3]
 [4 5 6]
 [7 8 9]]
"""

print(arr[0]) # [1 2 3]
print(arr[2]) # [7 8 9]

print(arr[0][1]) # 2
print(arr[2][2]) # 9
```

Instead of using several brackets to access the array items, we can also use the below syntax:

```py
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(arr)
"""
[[[ 1  2  3]
  [ 4  5  6]]

 [[ 7  8  9]
  [10 11 12]]]
"""

print(arr[0][1]) # [4 5 6]
print(arr[0, 1]) # [4 5 6]

print(arr[1][0]) # [7 8 9]
print(arr[1, 0]) # [7 8 9]
```

---

---

## Using negative indices

Using negative indices selects rows from the end:

```py
import numpy as np

arr = np.zeros((5, 4))

for i in range(5):
  arr[i] = i

print(arr)
"""
[[0. 0. 0. 0.]
 [1. 1. 1. 1.]
 [2. 2. 2. 2.]
 [3. 3. 3. 3.]
 [4. 4. 4. 4.]]
"""

print(arr[[-2, -1]])
"""
[[3. 3. 3. 3.]
 [4. 4. 4. 4.]]
"""
```

---

---

## Retrieving Using Multiple Index Arrays

Passing multiple index arrays does something slightly different; it selects a one-dimensional array of elements corresponding to each tuple of indices:

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

print(arr[[2, 1], [3, 4]]) # [13  9]
```

We can also use the index slicing, to retrieve various item combinations from the arrays:

```py
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(arr)
"""
[[[ 1  2  3]
  [ 4  5  6]]

 [[ 7  8  9]
  [10 11 12]]]
"""

# select all the items from the first dimension
# select the zeroth item from the second dimension
# select the items on index 1 and 2 from the third dimension
print(arr[:, 0, 1:3])
"""
[[[2 3]]
 [[8 9]]]
"""
```

---

---

## Retrieving items with Boolean Indexing

Comparisons with a string and an array is also vectorized, just like the arithmetic operations on arrays:

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
boolean_arr = names == "Bob"

print(boolean_arr) # [ True False False  True False False False]
```

In the below example, we have 2 arrays; one with names and the other one is a 2-dimensional array with some data. Let's say, they have some connection to each other. How can we retrieve the items from the second array, corresponding to a particular value in the first array? We can use the boolean array:

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

print(data[names == "Bob"])
"""
[[4 7]
 [0 0]]
"""
```

> Remember for the above to work, the Boolean array must be of the same length as the array axis it’s indexing.

We can combine retrieving the items using a boolean array with indexing and slicing:

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

print(data[names == "Bob"])
"""
[[4 7]
 [0 0]]
"""

# retrieve the items starting from the index 1 from the resulting array
print(data[names == "Bob", 1:])
"""
[[7]
 [0]]
"""

# retrieve the items on the index 1 from the resulting array
print(data[names == "Bob", 1]) # [7 0]
```

To select everything but "Bob" you can either use `!=` or negate the condition using `~`. The `~` operator can be useful when you want to invert a Boolean array referenced by a variable.

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

print(data[~(names == "Bob")])
"""
[[  0   2]
 [ -5   6]
 [  1   2]
 [-12  -4]
 [  3   4]]
"""
```

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

condition = names == "Bob"

print(data[~condition])
"""
[[  0   2]
 [ -5   6]
 [  1   2]
 [-12  -4]
 [  3   4]]
"""
```

> Remember, selecting data from an array by Boolean indexing and assigning the result to a new variable always creates a copy of the data, even if the returned array is unchanged.

---

---

## Logical operators with boolean arrays

The Python keywords `and` and `or` do not work with Boolean arrays. Use `&` (and) and `|` (or) instead.

```py
import numpy as np

names = np.array(["Bob", "Joe", "Will", "Bob", "Will", "Joe", "Joe"])
data = np.array([[4, 7], [0, 2], [-5, 6], [0, 0], [1, 2], [-12, -4], [3, 4]])

condition = (names == "Bob") | (names == "Will")

print(data[~condition])
"""
[[  0   2]
 [-12  -4]
 [  3   4]]
"""
```

---

---

## Retrieving Items in a Custom Order

We can make the arrays in a 2 or multi-dimensional arrays to be outputted in a specified order:

```py
import numpy as np

arr = np.zeros((5, 4))

for i in range(5):
  arr[i] = i

print(arr)
"""
[[0. 0. 0. 0.]
 [1. 1. 1. 1.]
 [2. 2. 2. 2.]
 [3. 3. 3. 3.]
 [4. 4. 4. 4.]]
"""

print(arr[[2, 1]])
"""
[[2. 2. 2. 2.]
 [1. 1. 1. 1.]]
"""
```

---

---

## Retrieving Items of a Lower Dimension-Ndarray in a Custom Order

In addition to reordering arrays in a higher dimension, we can also reorder the items in a lower dimension:

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

print(arr[[3, 2, 1, 0]][:, [1, 0, 3, 2, 4]])
"""
[[16 15 18 17 19]
 [11 10 13 12 14]
 [ 6  5  8  7  9]
 [ 1  0  3  2  4]]
"""
```

> Keep in mind that fancy indexing, unlike slicing, always copies the data into a new array when assigning the result to a new variable.

---

---
