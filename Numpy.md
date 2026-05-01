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
  - [Unversal Functions](#unversal-functions)
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

## Unversal Functions

[Unversal Functions](./PyN_Ufuncs.md)

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
