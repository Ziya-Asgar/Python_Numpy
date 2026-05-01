# Numpy

- [Numpy](#numpy)
  - [Some Useful Links](#some-useful-links)
  - [Intro](#intro)
  - [Creating Ndarrays](#creating-ndarrays)
  - [Retrieving Information from Ndarrays](#retrieving-information-from-ndarrays)
  - [Changind Ndarrays](#changind-ndarrays)
  - [Some Numpy Methods](#some-numpy-methods)
  - [Math With Ndarrays](#math-with-ndarrays)
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
  - [File Input and Output with Arrays](#file-input-and-output-with-arrays)
    - [Saving to and Loading from files with `numpy.save` and `numpy.load`](#saving-to-and-loading-from-files-with-numpysave-and-numpyload)
    - [Saving to files with `numpy.savez`](#saving-to-files-with-numpysavez)

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

## Changind Ndarrays

[Changind Ndarrays](./PyN_ChangindNdarrays.md)

<hr>

## Some Numpy Methods

[Some Numpy Methods](./PyN_SomeNumpyMethods.md)

<hr>

## Math With Ndarrays

[Math With Ndarrays](./PyN_MathWithNdarrays.md)

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
