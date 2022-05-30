---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.13.8
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Atoms and Molecular Geometry


## Geometry and Coordinates in 3D Space


We can use the `numpy` library to create double-precision 3-vectors to use for coordinates:

```python
import numpy as np
def coord(x,y,z): return np.array([x,y,z],np.double)
```

Double precision variables, 64-bit precision floating-point numbers, are the standard datatype for most scientific programming applications, and will be used throughout the rest of the course.


`numpy` makes it easy to compute distances:

```python
def distance(pt1,pt2): return np.linalg.norm(pt1-pt2)
```

Here we use the `norm` method of numpy arrays to compute the *2-norm* of the difference between the two vectors, corresponding to the normal distance computed via the Pythagorean theorem
$$ r_{12} = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2 + (z_1-z_2)^2}.$$


We have not specified units for the distance function. If the xyz-coordinates correspond to meters, `distance` will return meters; if they correspond to Angstroms ($=10^{-10} m$), `distance` will return Angstroms. This ambiguity is a both a convenient polymorphism, in that we don't have to define different functions for different units, and a future source of errors if we try to compute distances between one point that has meter units and another that uses Angstroms.

A rigorous *type system* can substantially reduce the ambiguity, often without reducing the polymorphism, but is beyond the scope of the current work.


## Computing neighbor lists


Many of the forces encountered in computational chemistry are *pairwise*, and computing distances to other atoms is a common operation.

```python
def distances(pt,others):
    ds = []
    for other in others:
        ds.append(distance(pt,other))
    return ds
```

We can make this syntax somewhat easier using Python's [list comprehensions](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions):

```python
def distances(pt,others): return [distance(pt,other) for other in others]
```

As we strive here for the *simplest readable code*, we will choose to use list comprehensions in cases such as this one where they more directly communicate our intentions.


We often want to select only the atoms that are nearby another atom. We can *filter* our list for distances that are less than a certain amount:

```python
def neighbors(distances,cutoff):
    def close(d): return d<cutoff
    return list(filter(close,distances))
```

Here we define an inline function `close` that returns `True` for values less than the cutoff. `filter` then selects values from the `distances` where that function is true. We use the `list` function on the result to return a normal Python list rather than an interator, which is slightly less efficient, but more convenient for interactive work such as we're doing in this notebook.

We could have also used an [anonymous function](https://docs.python.org/3/tutorial/controlflow.html#lambda-expressions) `lambda` to define the `close` function:

```python
def neighbors(distances,cutoff): return list(filter(lambda d: d<cutoff,distances))
```

You can decide for yourself what makes the simplest readable code; the author somewhat prefers the inline function.


To show how these functions work, let's create a cube of atoms $10\times 10\times 10$ centered at the origin, using the `numpy` `rand` function:

```python
def pointcube(N,D):
    pts = []
    for _ in range(N):
        pt = np.random.rand(3)
        pts.append(D*(pt-0.5)) # Uses broadcasting to subtract 0.5 from each coordinate
    return pts
```

```python
pts = pointcube(20,10)
pts # Convenient way to print out the return value
```

```python
origin = coord(0,0,0)
ds = distances(origin,pts)
ds
```

```python
ns = neighbors(ds,3)
ns
```

```python
raise Exception("finish fast neighbor list calculation")
```

## Representing atoms


## Fast methods of computing Coulomb repulsion

```python

```
