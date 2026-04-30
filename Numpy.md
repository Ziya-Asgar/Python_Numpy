# Numpy

- [Numpy](#numpy)
  - [Some Useful Links](#some-useful-links)
  - [Intro](#intro)
  - [Creating Ndarrays](#creating-ndarrays)
  - [Retrieving Information from Ndarrays](#retrieving-information-from-ndarrays)
  - [Some Operations on Ndarrays](#some-operations-on-ndarrays)
    - [Changing the array items using boolean arrays](#changing-the-array-items-using-boolean-arrays)
    - [Slicing of ndarrays is not like slicing python lists](#slicing-of-ndarrays-is-not-like-slicing-python-lists)
    - [Copying ndarrays, partially or fully](#copying-ndarrays-partially-or-fully)
    - [Assigning the items to the whole ndarray](#assigning-the-items-to-the-whole-ndarray)
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
  - [Arithmetic with Numpy Arrays](#arithmetic-with-numpy-arrays)
    - [Math between 2 ndarrays](#math-between-2-ndarrays)
    - [Math between an ndarray and a single value](#math-between-an-ndarray-and-a-single-value)
    - [Comparisons between ndarrays](#comparisons-between-ndarrays)
  - [Numpy's `random` module](#numpys-random-module)
    - [Table of some methods from the `numpy.random` module](#table-of-some-methods-from-the-numpyrandom-module)
    - [Getting an array from a standard normal distribution](#getting-an-array-from-a-standard-normal-distribution)
    - [`np.random.permutation`](#nprandompermutation)
    - [`np.random.shuffle`](#nprandomshuffle)
    - [`np.random.uniform`](#nprandomuniform)
    - [`np.random.randint`](#nprandomrandint)
    - [`np.random.standard_normal`](#nprandomstandard_normal)
    - [`np.random.normal`](#nprandomnormal)
    - [`np.random.binomial`](#nprandombinomial)
    - [`np.random.choice`](#nprandomchoice)
    - [`np.random.rand`](#nprandomrand)
  - [Universal Functions: Fast Element-Wise Array Functions](#universal-functions-fast-element-wise-array-functions)
    - [Unary ufuncs](#unary-ufuncs)
      - [List of some unary ufuncs](#list-of-some-unary-ufuncs)
      - [`sqrt`](#sqrt)
      - [`sign`](#sign)
    - [Binary ufuncs](#binary-ufuncs)
      - [List of some binary ufuncs](#list-of-some-binary-ufuncs)
      - [`add`](#add)
      - [`maximum`](#maximum)
      - [`modf`](#modf)
    - [Outputing ufuncs to an existing array](#outputing-ufuncs-to-an-existing-array)
  - [Array-Oriented Programming with Arrays](#array-oriented-programming-with-arrays)
    - [`where`](#where)
  - [Mathematical and Statistical Methods](#mathematical-and-statistical-methods)
    - [List of some mathematical and statistical methods](#list-of-some-mathematical-and-statistical-methods)
    - [`sum`, `mean`](#sum-mean)
    - [`cumsum`, `cumprod`](#cumsum-cumprod)
    - [`std`](#std)
    - [Methods for Boolean Arrays](#methods-for-boolean-arrays)
      - [`any`, `all`](#any-all)
    - [Sorting](#sorting)
    - [Set methods](#set-methods)
      - [`numpy.unique`](#numpyunique)
      - [`numpy.isin`](#numpyisin)
  - [File Input and Output with Arrays](#file-input-and-output-with-arrays)
    - [Saving to and Loading from files with `numpy.save` and `numpy.load`](#saving-to-and-loading-from-files-with-numpysave-and-numpyload)
    - [Saving to files with `numpy.savez`](#saving-to-files-with-numpysavez)
  - [Linear Algebra](#linear-algebra)
    - [Matrix multiplication with `dot` or `@`](#matrix-multiplication-with-dot-or-)
    - [Finding inverse and determinant of a matrix](#finding-inverse-and-determinant-of-a-matrix)

<hr>

## Some Useful Links

- https://wesmckinney.com/book/numpy-basics
- https://numpy.org/doc/stable/index.html

<hr>
<hr>

## Intro

NumPy, short for Numerical Python, is one of the most important foundational packages for numerical computing in Python. Many computational packages providing scientific functionality use NumPy's array objects.

While NumPy by itself does not provide modeling or scientific functionality, having an understanding of NumPy arrays and array-oriented computing will help you use tools with array computing semantics, like pandas, much more effectively.

<hr>

## Creating Ndarrays

[Creating Ndarrays](./PyN_CreatingNdarrays.md)

<hr>

## Retrieving Information from Ndarrays

[Retrieving Information from Ndarrays](./PyN_RetrievingInformation.md)

<hr>

## Some Operations on Ndarrays

### Changing the array items using boolean arrays

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

<hr>

### Slicing of ndarrays is not like slicing python lists

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

<hr>

### Copying ndarrays, partially or fully

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

<hr>

### Assigning the items to the whole ndarray

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

<hr>

## Some numpy methods

### `arange`

`numpy.arange` is an array-valued version of the built-in Python `range` function:

```py
import numpy as np

print(list(range(5))) # [0, 1, 2, 3, 4]
print(np.arange(5)) # [0 1 2 3 4]
```

<hr>

### `linspace`

`numpy.linspace` also creates an array. It accepts the beginning and ending numbers, and how many numbers should be between the beginning and ending numbers:

```py
import numpy as np

print(np.linspace(3, 27, 9)) # [ 3.  6.  9. 12. 15. 18. 21. 24. 27.]
```

<hr>

### Transposing Arrays and Swapping Axes

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

<hr>

### `concatenate`

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

<hr>

### `tile`

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

<hr>

### `np.nan_to_num`

The `np.nan_to_num` function turns `NaN` into 0 and `inf`/`-inf` into specified numbers.

```py
import numpy as np

# Create an array with NaN and inf values
arr = np.array([1, 2, np.nan, np.inf, -np.inf, 4, np.nan])

# Replace NaN values with 0 and inf values with 0
arr = np.nan_to_num(arr, posinf=100, neginf=0)

print(arr) # [  1.   2.   0. 100.   0.   4.   0.]
```

<hr>

### `np.quantile`

```py
import numpy as np

numbers = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
quantiles = np.quantile(numbers, [0.25, 0.5, 0.75])
print(quantiles)  # [3.25 5.5  7.75]
```

<hr>

### `np.nanmean`

For statistics of arrays which include nan’s, numpy has a number of functions starting with nan... These remove the nan-values from a sample before executing any other computation. For example, `np.nanmean`:

```py
import numpy as np

x = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
np.mean(x) # np.float64(4.5)

xWithNan = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, np.nan]
np.mean(xWithNan) # np.float64(nan)

np.nanmean(xWithNan) # np.float64(4.5)
```

<hr>

### Calculating the range

The range is simply the difference between the highest and the lowest data value, and can be found with `np.ptp` (ptp stands for “peak-to-peak”):

```py
import numpy as np

x = np.arange(1, 101)
print(np.ptp(x)) # 99
```

<hr>

## Arithmetic with Numpy Arrays

Arrays enable you to express batch operations on data without writing any `for` loops. NumPy users call this **vectorization**.

<hr>

### Math between 2 ndarrays

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

<hr>

### Math between an ndarray and a single value

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

### Comparisons between ndarrays

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

<hr>

## Numpy's `random` module

The `numpy.random` module supplements the built-in Python `random` module with functions for efficiently generating whole arrays of sample values from many kinds of probability distributions.

### Table of some methods from the `numpy.random` module

See below table for a partial list of methods available on the `np.random` module and random generator objects like `rng`.

| Method            | Description                                                                  |
| ----------------- | ---------------------------------------------------------------------------- |
| `permutation`     | Return a random permutation of a sequence, or return a permuted range        |
| `shuffle`         | Randomly permute a sequence in place                                         |
| `uniform`         | Draw samples from a uniform [0, 1) distribution                              |
| `randint`         | Draw random integers from a given low-to-high range                          |
| `standard_normal` | Draw samples from a normal distribution with mean 0 and standard deviation 1 |
| `binomial`        | Draw samples from a binomial distribution                                    |
| `normal`          | Draw samples from a normal (Gaussian) distribution                           |
| `beta`            | Draw samples from a beta distribution                                        |
| `chisquare`       | Draw samples from a chi-square distribution                                  |
| `gamma`           | Draw samples from a gamma distribution                                       |

<hr>

### Getting an array from a standard normal distribution

We can get a 4 × 4 array of samples from the standard normal distribution using `numpy.random.standard_normal`:

```py
import numpy as np

samples = np.random.standard_normal(size=(4, 4))
```

Functions like `numpy.random.standard_normal` use the `numpy.random` module's default random number generator, but your code can be configured to use an explicit generator:

```py
import numpy as np

rng = np.random.default_rng(seed=12345)
data = rng.standard_normal((2, 3))
print(data)
"""
[[-1.42382504  1.26372846 -0.87066174]
 [-0.25917323 -0.07534331 -0.74088465]]
"""
```

<hr>

### `np.random.permutation`

The `permutation` method randomly permutes a sequence, or returns a permuted range. If we pass an integer, it randomly permutes the `np.arange(<int>)`. If we pass a sequence it returns the randomly permuted version of a sequence:

```py
import numpy as np

# returns an array of 10 random numbers
np.random.permutation(10)

# returns the shuffled array based on the provided sequence
np.random.permutation([1, 2, 3, 4, 5]) # array([4, 1, 2, 3, 5])

arr = np.arange(9).reshape((3, 3))
print(arr)
"""
[[0 1 2]
 [3 4 5]
 [6 7 8]]
"""

np.random.permutation(arr)
"""
array([[3, 4, 5],
       [6, 7, 8],
       [0, 1, 2]])
"""
```

### `np.random.shuffle`

The `shuffle` method from the `np.random` module is used to randomize the order of elements in an array. It shuffles the elements in-place, meaning it modifies the original array.

```py
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

np.random.shuffle(arr)
print(arr) # [3 4 5 2 1]
```

### `np.random.uniform`

A uniform distribution is a probability distribution where every possible outcome has an equal probability of occurring. In the context of the `uniform` method, it means that each possible value within the specified range has an equal chance of being selected.

The `uniform` method from the `np.random` module is used to generate random numbers within a specified range.

```py
import numpy as np

# Generate a random number between 0 and 1
random_num = np.random.uniform(0, 1)

print("Random number between 0 and 1:")
print(random_num)
```

The `uniform` method can also return an array when we use the `size` argument:

```py
import numpy as np

# Generate an array of 5 random values
random_nums = np.random.uniform(0, 1, size=5)

print("\nArray of 5 random values between 0 and 1:")
print(random_nums)
```

### `np.random.randint`

The `randint` method in the `np.random` module is used to generate random integers from a specified range.

```py
import numpy as np

# Generate a single random integer between 0 (inclusive) and 10 (exclusive)
random_int = np.random.randint(low=0, high=10)
print("Single random integer:", random_int)

# Generate an array of 5 random integers between 0 (inclusive) and 10 (exclusive)
random_ints = np.random.randint(low=0, high=10, size=5)
print("Array of random integers:", random_ints)

# Generate a 2x3 matrix of random integers between 0 (inclusive) and 10 (exclusive)
random_matrix = np.random.randint(0, 10, (2, 3))
print("2x3 matrix of random integers:\n", random_matrix)
```

### `np.random.standard_normal`

The `standard_normal` method in the `np.random` module is used to generate random numbers from a standard normal distribution (also known as a Gaussian distribution). The standard normal distribution has a mean of 0 and a standard deviation of 1.

```py
import numpy as np

# Generate a single random number from a standard normal distribution
random_number = np.random.standard_normal()
print(random_number)

# Generate an array of 5 random numbers from a standard normal distribution
random_numbers = np.random.standard_normal(size=5)
print(random_numbers)

# Generate a 2x3 matrix of random numbers from a standard normal distribution
random_matrix = np.random.standard_normal(size=(2, 3))
print(random_matrix)
```

### `np.random.normal`

The `normal` method in the `np.random` module is used to generate random numbers from a normal (Gaussian) distribution with a specified mean and standard deviation.

```py
import numpy as np

# Generate a single random number from a normal distribution with mean 0 and standard deviation 1
random_number = np.random.normal(loc=0, scale=1)
print(random_number)

# Generate an array of 5 random numbers from a normal distribution with mean 0 and standard deviation 1
random_numbers = np.random.normal(loc=0, scale=1, size=5)
print(random_numbers)

# Generate a 2x3 matrix of random numbers from a normal distribution with mean 10 and standard deviation 2
random_matrix = np.random.normal(loc=10, scale=2, size=(2, 3))
print(random_matrix)
```

> If you set `loc=0` and `scale=1`, it behaves exactly like `standard_normal`.

### `np.random.binomial`

The `binomial` method in the `np.random` module is used to generate random numbers from a binomial distribution.

```py
import numpy as np

# Generate a single random number from a binomial distribution with 10 trials and success probability 0.5
random_number = np.random.binomial(n=10, p=0.5)
print(random_number)

# Generate an array of 5 random numbers from a binomial distribution with 10 trials and success probability 0.5
random_numbers = np.random.binomial(n=10, p=0.5, size=5)
print(random_numbers)

# Generate a 2x3 matrix of random numbers from a binomial distribution with 10 trials and success probability 0.5
random_matrix = np.random.binomial(n=10, p=0.5, size=(2, 3))
print(random_matrix)
```

### `np.random.choice`

The `choice` method in the `np.random` module is used to generate random samples from a given array or list. It allows you to randomly select elements from the array, either with or without replacement, and optionally with specified probabilities for each element.

```py
import numpy as np

# Input array
elements = ['apple', 'banana', 'cherry', 'date']

# Randomly select one element from the array
random_element = np.random.choice(elements)
print(random_element)

# Randomly select 3 elements with replacement
random_elements_with_replacement = np.random.choice(elements, size=3, replace=True)
print(random_elements_with_replacement)

# Randomly select 3 elements without replacement
random_elements_without_replacement = np.random.choice(elements, size=3, replace=False)
print(random_elements_without_replacement)

# Randomly select elements with specified probabilities
probabilities = [0.5, 0.3, 0.1, 0.1]  # Probabilities for ['apple', 'banana', 'cherry', 'date']
random_elements_with_probabilities = np.random.choice(elements, size=5, p=probabilities)
print(random_elements_with_probabilities)
```

### `np.random.rand`

The `rand` method in the np.random module is used to generate random numbers from a uniform distribution over the interval [0,1). It is a convenient way to create arrays of random floats where each value is equally likely to be any number between 0 (inclusive) and 1 (exclusive).

```py
import numpy as np

# Generate a single random float between 0 and 1
random_float = np.random.rand()
print(random_float)

# Generate a 1D array of 5 random floats
random_array_1d = np.random.rand(5)
print(random_array_1d)

# Generate a 2x3 matrix of random floats
random_matrix = np.random.rand(2, 3)
print(random_matrix)

# Generate a 3D array of shape (2, 2, 2) of random floats
random_3d_array = np.random.rand(2, 2, 2)
print(random_3d_array)
```

<hr>

## Universal Functions: Fast Element-Wise Array Functions

A universal function, or ufunc, is a function that performs element-wise operations on data in ndarrays. You can think of them as fast vectorized wrappers for simple functions that take one or more scalar values and produce one or more scalar results.

### Unary ufuncs

Many ufuncs are simple element-wise transformations. These are referred to as **unary ufuncs**.

#### List of some unary ufuncs

Here are some unary universal functions:

| Function                                                      | Description                                                                                                     |
| ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `abs`, `fabs`                                                 | Compute the absolute value element-wise for integer, floating-point, or complex values                          |
| `sqrt`                                                        | Compute the square root of each element (equivalent to `arr ** 0.5`)                                            |
| `square`                                                      | Compute the square of each element (equivalent to `arr ** 2`)                                                   |
| `exp`                                                         | Compute the exponent ex of each element                                                                         |
| `log`, `log10`, `log2`, `log1p`                               | Natural logarithm (base e), log base 10, log base 2, and log(1 + x), respectively                               |
| `sign`                                                        | Compute the sign of each element: 1 (positive), 0 (zero), or –1 (negative)                                      |
| `ceil`                                                        | Compute the ceiling of each element (i.e., the smallest integer greater than or equal to that number)           |
| `floor`                                                       | Compute the floor of each element (i.e., the largest integer less than or equal to each element)                |
| `rint`                                                        | Round elements to the nearest integer, preserving the `dtype`                                                   |
| `modf`                                                        | Return fractional and integral parts of array as separate arrays                                                |
| `isnan`                                                       | Return Boolean array indicating whether each value is `NaN` (Not a Number)                                      |
| `isfinite`, `isinf`                                           | Return Boolean array indicating whether each element is finite (non-`inf`, non-`NaN`) or infinite, respectively |
| `cos`, `cosh`, `sin`, `sinh`, `tan`, `tanh`                   | Regular and hyperbolic trigonometric functions                                                                  |
| `arccos`, `arccosh`, `arcsin`, `arcsinh`, `arctan`, `arctanh` | Inverse trigonometric functions                                                                                 |
| `logical_not`                                                 | Compute truth value of `not x` element-wise (equivalent to `~arr`)                                              |

#### `sqrt`

Here is an example of using `numpy.sqrt` (a unary ufunc). It calculates the square root of the elements of an array:

```py
import numpy as np

arr = np.array([4, 9, 16, 25])
print(np.sqrt(arr)) # [2. 3. 4. 5.]
```

<hr>

#### `sign`

The `sign` method returns an element-wise indication of the sign of a number.

- If it encounters a negative number, it returns -1,
- for 0 it returns 0, and
- for a positive number it returns 1.

```py
import numpy as np

arr = np.array([-20, -10, 0, 10, 20])
print(np.sign(arr)) # [-1 -1  0  1  1]
```

<hr>

### Binary ufuncs

Some other ufuncs, can take two arrays (thus, **binary ufuncs**) and return a single array as the result

<hr>

#### List of some binary ufuncs

Here are some binary universal functions:

| Function                                                               | Description                                                                                                              |
| ---------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| `add`                                                                  | Add corresponding elements in arrays                                                                                     |
| `subtract`                                                             | Subtract elements in second array from first array                                                                       |
| `multiply`                                                             | Multiply array elements                                                                                                  |
| `divide`, `floor_divide`                                               | Divide or floor divide (truncating the remainder)                                                                        |
| `power`                                                                | Raise elements in first array to powers indicated in second array                                                        |
| `maximum`, `fmax`                                                      | Element-wise maximum; `fmax` ignores `NaN`                                                                               |
| `minimum`, `fmin`                                                      | Element-wise minimum; `fmin` ignores `NaN`                                                                               |
| `mod`                                                                  | Element-wise modulus (remainder of division)                                                                             |
| `copysign`                                                             | Copy sign of values in second argument to values in first argument                                                       |
| `greater`, `greater_equal`, `less`, `less_equal`, `equal`, `not_equal` | Perform element-wise comparison, yielding Boolean array (equivalent to infix operators `>`, `>=`, `<`, `<=`, `==`, `!=`) |
| `logical_and`                                                          | Compute element-wise truth value of AND (`&`) logical operation                                                          |
| `logical_or`                                                           | Compute element-wise truth value of OR (`\|`) logical operation                                                          |
| `logical_xor`                                                          | Compute element-wise truth value of XOR (`^`) logical operation                                                          |

#### `add`

Here is an example of using `numpy.add`:

```py
import numpy as np

arr1 = np.array([4, 9, 16, 25])
arr2 = np.array([10, 20, 30, 40])

print(np.add(arr1, arr2)) # [14 29 46 65]
```

With `numpy.add`, we can add an array and a single value:

```py
import numpy as np

arr1 = np.array([4, 9, 16, 25])

print(np.add(arr1, 10)) # [14 19 26 35]
```

#### `maximum`

The `maximum` method in the numpy module is used to compute the element-wise maximum of two arrays. It compares corresponding elements of the input arrays and returns a new array containing the maximum values at each position.

```py
import numpy as np

arr1 = np.array([4, 9, 30, 40])
arr2 = np.array([10, 20, 16, 25])

print(np.maximum(arr1, arr2)) # [10 20 30 40]
```

#### `modf`

While not common, a ufunc can return multiple arrays. `numpy.modf` is a vectorized version of the built-in Python `math.modf`, it returns the fractional and integral parts of a floating-point array:

```py
import numpy as np

rng = np.random.default_rng(seed=12345)
arr = rng.standard_normal(7) * 5
print(arr) # [-7.11912518  6.31864229 -4.35330869 -1.29586617 -0.37671654 -3.70442326 -6.83896351]

remainder, whole_part = np.modf(arr)
print(remainder) # [-0.11912518  0.31864229 -0.35330869 -0.29586617 -0.37671654 -0.70442326 -0.83896351]
print(whole_part) # [-7.  6. -4. -1. -0. -3. -6.]
```

<hr>

### Outputing ufuncs to an existing array

Ufuncs accept an optional `out` argument that allows them to assign their results into an existing array rather than create a new one:

```py
import numpy as np

arr1 = np.array([4, 9, 16, 25])
arr2 = np.zeros_like(arr1)

np.add(arr1, 10, out=arr2)

print(arr1) # [ 4  9 16 25]
print(arr2) # [14 19 26 35]
```

<hr>

## Array-Oriented Programming with Arrays

### `where`

The `numpy.where` function is a vectorized version of the ternary expression `x if condition else y`:

```py
import numpy as np

xarr = np.array([1.1, 1.2, 1.3, 1.4, 1.5])
yarr = np.array([2.1, 2.2, 2.3, 2.4, 2.5])
cond = np.array([True, False, True, True, False])

result = np.where(cond, xarr, yarr)

print(result) # [1.1 2.2 1.3 1.4 2.5]
```

The second and third arguments to `numpy.where` don’t need to be arrays; one or both of them can be scalars.

```py
import numpy as np

arr = np.array([
  [ 10.0,  10.0,  10.0, -10.0],
  [-10.0, -10.0,  10.0,  10.0],
  [-10.0, -10.0,  10.0,  10.0],
  [-10.0,  10.0, -10.0 , -10.0]
])

result = np.where(arr > 0, 2, -2)

print(result)
"""
[[ 2  2  2 -2]
 [-2 -2  2  2]
 [-2 -2  2  2]
 [-2  2 -2 -2]]
"""
```

```py
import numpy as np

arr = np.array([
  [ 10.0,  10.0,  10.0, -10.0],
  [-10.0, -10.0,  10.0,  10.0],
  [-10.0, -10.0,  10.0,  10.0],
  [-10.0,  10.0, -10.0 , -10.0]
])

result = np.where(arr > 0, 2, arr)

print(result)
"""
[[  2.   2.   2. -10.]
 [-10. -10.   2.   2.]
 [-10. -10.   2.   2.]
 [-10.   2. -10. -10.]]
"""
```

Using `numpy.where` does not check whether the index labels are aligned or not (and does not even require the objects to be the same length).

<hr>

## Mathematical and Statistical Methods

Numpy provides a set of mathematical functions that compute statistics about an entire array or about the data along an axis. You can use aggregations (sometimes called reductions) like `sum`, `mean`, and `std` (standard deviation) either by calling the array instance method or using the top-level NumPy function.

<hr>

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

<hr>

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

<hr>

### Methods for Boolean Arrays

#### `any`, `all`

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

<hr>

### Sorting

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

<hr>

### Set methods

See below table for a listing of array set operations in NumPy.

| Method              | Description                                                                        |
| ------------------- | ---------------------------------------------------------------------------------- |
| `unique(x)`         | Compute the sorted, unique elements in `x`                                         |
| `intersect1d(x, y)` | Compute the sorted, common elements in `x` and `y`                                 |
| `union1d(x, y)`     | Compute the sorted union of elements                                               |
| `in1d(x, y)`        | Compute a Boolean array indicating whether each element of `x` is contained in `y` |
| `setdiff1d(x, y)`   | Set difference, elements in `x` that are not in `y`                                |
| `setxor1d(x, y)`    | Set symmetric differences; elements that are in either of the arrays, but not both |

#### `numpy.unique`

NumPy has some basic set operations for one-dimensional ndarrays. A commonly used one is `numpy.unique`, which returns the sorted unique values in an array:

```py
import numpy as np

names = np.array(["Bob", "Will", "Joe", "Bob", "Will", "Joe", "Joe"])
print(np.unique(names)) # ['Bob' 'Joe' 'Will']
```

<hr>

#### `numpy.isin`

Another function, `numpy.isin`, tests if the values in one array is present in another array, returning a Boolean array:

```py
import numpy as np

values = np.array([6, 0, 0, 3, 2, 5, 6])
print(np.isin(values, [2, 3, 6])) # [ True False False  True  True False  True]
```

<hr>

## File Input and Output with Arrays

NumPy is able to save and load data to and from disk in some text or binary formats.

### Saving to and Loading from files with `numpy.save` and `numpy.load`

`numpy.save` and `numpy.load` are the two workhorse functions for efficiently saving and loading array data on disk. Arrays are saved by default in an uncompressed raw binary format with file extension "**.npy**":

```py
import numpy as np

arr = np.arange(10)
np.save("some_array", arr)
```

The array on disk can then be loaded with `numpy.load`:

```py
import numpy as np

print(np.load("some_array.npy"))
```

<hr>

### Saving to files with `numpy.savez`

You can save multiple arrays in an uncompressed archive using `numpy.savez` and passing the arrays as keyword arguments:

```py
import numpy as np

arr = np.arange(10)

np.savez("array_archive.npz", a=arr, b=arr)
arch = np.load("array_archive.npz")

print(arch["b"]) # [0 1 2 3 4 5 6 7 8 9]
```

If your data compresses well, you may wish to use `numpy.savez_compressed` instead:

```py
import numpy as np

arr1 = np.arange(10)
arr2 = np.arange(10, 20)

np.savez("arr_archive.npz", a=arr1, b=arr2)
arch = np.load("arr_archive.npz")

print(arch) # NpzFile 'arr_archive.npz' with keys: a, b
print(arch["b"]) # [0 1 2 3 4 5 6 7 8 9]
```

<hr>

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

<hr>

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

<hr>
````
