# Creating ndarrays

- [Creating ndarrays](#creating-ndarrays)
  - [The NumPy ndarray: A Multidimensional Array Object](#the-numpy-ndarray-a-multidimensional-array-object)
  - [Creating ndarrays from a list](#creating-ndarrays-from-a-list)
  - [Creating ndarrays from a nested list](#creating-ndarrays-from-a-nested-list)
  - [Creating ndarrays with the specific data type](#creating-ndarrays-with-the-specific-data-type)
  - [Creating ndarrays consisting of zeros or ones](#creating-ndarrays-consisting-of-zeros-or-ones)
  - [Creating empty ndarrays](#creating-empty-ndarrays)
  - [Creating ndarrays filled with the specific value](#creating-ndarrays-filled-with-the-specific-value)
  - [Creating ndarrays of zeros based on the shape and data type of another array](#creating-ndarrays-of-zeros-based-on-the-shape-and-data-type-of-another-array)
  - [Creating ndarrays of ones based on the shape and data type of another array](#creating-ndarrays-of-ones-based-on-the-shape-and-data-type-of-another-array)
  - [Creating empty ndarrays based on the shape and data type of another array](#creating-empty-ndarrays-based-on-the-shape-and-data-type-of-another-array)
  - [Creating ndarrays full of a specific value based on the shape and data type of another array](#creating-ndarrays-full-of-a-specific-value-based-on-the-shape-and-data-type-of-another-array)
  - [Create ndarrays with the `np.eye` method](#create-ndarrays-with-the-npeye-method)
  - [Create ndarrays with the `np.identity` method](#create-ndarrays-with-the-npidentity-method)
  - [Create ndarrays with the `np.tri` method](#create-ndarrays-with-the-nptri-method)

---

---

## The NumPy ndarray: A Multidimensional Array Object

**ndarray** is an N-dimensional array object. An ndarray is a generic multidimensional container for homogeneous data; that is, **all of the elements must be the same type**. We can use the below 2 methods on every array instance to learn the dimension and the data type of ndarray:

- a `shape`, a tuple indicating the size of each dimension, and
- a `dtype`, an object describing the data type of the array.

The easiest way to create an array is to use the `array` function. This function accepts any sequence-like object (including other arrays) and produces a new NumPy array containing the passed data.

---

---

## Creating ndarrays from a list

Here is an example of creating an ndarray from a list:

```py
import numpy as np

data = [6, 7.5, 8, 0, 1]
arr = np.array(data)

print(arr) # [6.  7.5 8.  0.  1. ]
```

---

---

## Creating ndarrays from a nested list

Nested sequences, like a list of equal-length lists, will be converted into a multidimensional array:

```py
import numpy as np

data = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr = np.array(data)

print(arr)
"""
[[1 2 3 4]
 [5 6 7 8]]
"""
```

---

---

## Creating ndarrays with the specific data type

Unless explicitly specified, `numpy.array` tries to infer a good data type for the array that it creates. The data type is stored in a special `dtype` metadata object.

```py
import numpy as np

data1 = [6, 7.5, 8, 0, 1]
arr1 = np.array(data1)

print(arr1.dtype) # float64

data2 = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr2 = np.array(data2)

print(arr2.dtype) # int64
```

If we want to specify the `dtype`, instead of letting numpy infer it, we can use the `dtype` keyword argument of the `array` numpy method:

```py
import numpy as np

data1 = [6, 7.5, 8, 0, 1]
arr1 = np.array(data1, dtype=np.float64)

print(arr1.dtype) # float64

data2 = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr2 = np.array(data2, dtype=np.int32)

print(arr2.dtype) # int32
```

If we cast some floating-point numbers to be of integer data type, the decimal part will be truncated:

```py
import numpy as np

arr = np.array([1.1, 2.2, 3.3, 4.4, 5.5], dtype=np.int64)
print(arr) # [1 2 3 4 5]
```

---

You can explicitly convert or cast an array from one data type to another using ndarray’s `astype` method. Calling `astype` always creates a new array (a copy of the data), even if the new data type is the same as the old data type.:

```py
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr.dtype) # int64

float_arr64 = arr.astype(np.float64)
print(float_arr64) # [1. 2. 3. 4. 5.]
print(float_arr64.dtype) # float64

float_arr32 = arr.astype(np.float32)
print(float_arr32) # [1. 2. 3. 4. 5.]
print(float_arr32.dtype) # float32
```

If you have an array of strings representing numbers, you can use `astype` to convert them to numeric form:

```py
import numpy as np

stringArr = np.array(["1.1", "2.2", "3"])
print(stringArr) # ['1.1' '2.2' '3']

numericArr = stringArr.astype(np.float64)
print(numericArr) # [1.1 2.2 3. ]
```

---

---

## Creating ndarrays consisting of zeros or ones

In addition to `numpy.array`, there are number of other functions for creating new arrays. `numpy.zeros` and `numpy.ones` create arrays of 0s or 1s, respectively, with a given length or shape.

```py
import numpy as np

print(np.zeros(5)) # [0. 0. 0. 0. 0.]
print(np.ones(5)) # [1. 1. 1. 1. 1.]
```

To create a higher dimensional array with these methods, we need to pass a tuple for the shape.

```py
import numpy as np

print(np.zeros((3, 4)))
"""
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
"""

print(np.ones((3, 6)))
"""
[[1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1. 1.]]
"""
```

---

---

## Creating empty ndarrays

`numpy.empty` returns a new array of a given shape and type, without initializing entries. As the entries corresponding to the members are not initialized, they are arbitrary (random).

```py
import numpy as np

np.empty(5)
np.empty((2, 3))

np.empty((2, 3, 4))
```

> It’s not safe to assume that `numpy.empty` will return an array of all zeros. This function returns uninitialized memory and thus may contain nonzero "garbage" values. You should use this function only if you intend to populate the new array with data.

---

---

## Creating ndarrays filled with the specific value

`full` produces an array of the given shape and data type with all values set to the indicated "fill value":

```py
import numpy as np

arr1 = np.full(2, 5)
arr2 = np.full((2, 3), 5)

print(arr1) # [5 5]
print(arr2)
"""
[[5 5 5]
 [5 5 5]]
"""
```

---

---

## Creating ndarrays of zeros based on the shape and data type of another array

`zeros_like` takes another array and produces an array of the same shape and data type, butt filled with zeros:

```py
import numpy as np

data1 = [1, 2, 3, 4]
data2 = [[1.01, 2.01, 3.01, 4], [5.01, 6.01, 7.01, 8.01]]

arr1 = np.zeros_like(data1)
arr2 = np.zeros_like(data2)

print(arr1) # [0 0 0 0]
print(arr2)
"""
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]]
"""
```

---

---

## Creating ndarrays of ones based on the shape and data type of another array

`ones_like` takes another array as an argument and produces a ones array of the same shape and data type:

```py
import numpy as np

data1 = [1, 2, 3, 4]
data2 = [[1.01, 2.01, 3.01, 4], [5.01, 6.01, 7.01, 8]]

arr1 = np.ones_like(data1)
arr2 = np.ones_like(data2)

print(arr1) # [1 1 1 1]
print(arr2)
"""
[[1. 1. 1. 1.]
 [1. 1. 1. 1.]]
"""
```

---

---

## Creating empty ndarrays based on the shape and data type of another array

`empty_like` takes another array and produces an empty array of the same shape:

```py
import numpy as np

data1 = [1, 2, 3, 4]
data2 = [[1.01, 2.01, 3.01, 4], [5.01, 6.01, 7.01, 8.01]]

arr1 = np.empty_like(data1)
arr2 = np.empty_like(data2)

print(arr1)
print(arr2)
```

---

---

## Creating ndarrays full of a specific value based on the shape and data type of another array

`full_like` takes another array and produces a filled array of the same shape and data type:

```py
import numpy as np

data1 = [1, 2, 3, 4]
data2 = [[1, 2, 3, 4], [5, 6, 7, 8]]

arr1 = np.full_like(data1, 5)
arr2 = np.full_like(data2, 5)

print(arr1) # [5 5 5 5]
print(arr2)
"""
[[5 5 5 5]
 [5 5 5 5]]
"""
```

---

---

## Create ndarrays with the `np.eye` method

We can create an identity matrix using `np.eye` method:

```py
import numpy as np

print(np.eye(4))
"""
[[1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]]
"""
```

You can change the position of the index of the diagonal. The default is 0, which refers to the main diagonal. A positive value means an upper diagonal. A negative value means a lower diagonal.

```py
import numpy as np

print(np.eye(4, dtype=np.uint8, k=1))
"""
 [[0 1 0 0]
 [0 0 1 0]
 [0 0 0 1]
 [0 0 0 0]]
"""

print(np.eye(4, dtype=np.uint8, k=-1))
"""
[[0 0 0 0]
 [1 0 0 0]
 [0 1 0 0]
 [0 0 1 0]]
"""
```

---

---

## Create ndarrays with the `np.identity` method

An identity matrix is a matrix where all the elements at the diagonal are 1 and the rest of the elements are 0. The function `np.identity()` returns an identity matrix of the specified size.

```py
import numpy as np

x = np.identity(4, dtype=np.uint8)
print(x)
"""
[[1 0 0 0]
 [0 1 0 0]
 [0 0 1 0]
 [0 0 0 1]]
"""
```

---

---

## Create ndarrays with the `np.tri` method

A lower triangular matrix is where the diagonal and all the elements below the diagonal are 1 and the rest of the elements are 0. The function `np.tri()` returns a lower triangular matrix of a given size

```py
import numpy as np

x = np.tri(4, 4, k=0, dtype=np.uint16)
print(x)
"""
[[1 0 0 0]
 [1 1 0 0]
 [1 1 1 0]
 [1 1 1 1]]
"""
```

---

---
