# Files

- [Files](#files)
  - [Saving to and Loading from files with `numpy.save` and `numpy.load`](#saving-to-and-loading-from-files-with-numpysave-and-numpyload)
  - [Saving to files with `numpy.savez`](#saving-to-files-with-numpysavez)

---

---

NumPy is able to save and load data to and from disk in some text or binary formats.

---

---

## Saving to and Loading from files with `numpy.save` and `numpy.load`

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

---

---

## Saving to files with `numpy.savez`

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

---

---
