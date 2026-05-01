# Numpy's `random` module

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

---

---

The `numpy.random` module supplements the built-in Python `random` module with functions for efficiently generating whole arrays of sample values from many kinds of probability distributions.

---

---

## Table of some methods from the `numpy.random` module

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

---

---

## Getting an array from a standard normal distribution

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

---

---

## `np.random.permutation`

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

---

---

## `np.random.shuffle`

The `shuffle` method from the `np.random` module is used to randomize the order of elements in an array. It shuffles the elements in-place, meaning it modifies the original array.

```py
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

np.random.shuffle(arr)
print(arr) # [3 4 5 2 1]
```

---

---

## `np.random.uniform`

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

---

---

## `np.random.randint`

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

---

---

## `np.random.standard_normal`

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

---

---

## `np.random.normal`

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

---

---

## `np.random.binomial`

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

---

---

## `np.random.choice`

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

---

---

## `np.random.rand`

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

---

---
