# Numpy

- [Numpy](#numpy)
  - [Some Useful Links](#some-useful-links)
  - [Intro](#intro)
  - [Creating Ndarrays](#creating-ndarrays)
  - [Retrieving Information from Ndarrays](#retrieving-information-from-ndarrays)
  - [Changind Ndarrays](#changind-ndarrays)
  - [Some Numpy Methods](#some-numpy-methods)
  - [Math With Ndarrays](#math-with-ndarrays)
  - [Numpy's Random Module](#numpys-random-module)
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

## Numpy's Random Module

[Numpy's Random Module](./PyN_RandomModule.md)

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
