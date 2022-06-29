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

## Distance
`numpy` makes it easy to compute distances:

```python
def distance(pt1,pt2): return np.linalg.norm(pt1-pt2)
```

Here we use the `norm` method of numpy arrays to compute the *2-norm* of the difference between the two vectors, corresponding to the normal distance computed via the Pythagorean theorem
$$ r_{12} = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2 + (z_1-z_2)^2}.$$


We have not specified units for the distance function. If the xyz-coordinates correspond to meters, `distance` will return meters; if they correspond to Angstroms ($=10^{-10} m$), `distance` will return Angstroms. This ambiguity is a both a convenient polymorphism, in that we don't have to define different functions for different units, and a future source of errors if we try to compute distances between one point that has meter units and another that uses Angstroms.

A rigorous *type system* can substantially reduce the ambiguity, often without reducing the polymorphism, but is beyond the scope of the current work.


## Neighbor lists

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


To show how these functions work, let's function to create a cube of atoms using the `numpy` `rand` function:

```python
def pointcube(N,D):
    pts = []
    for _ in range(N):
        pt = np.random.rand(3)
        pts.append(D*(pt-0.5)) # Uses broadcasting to subtract 0.5 from each coordinate
    return pts
```

`pointcube` can be rewritten using list comprehensions to simplify:

```python
def pointcube(N,D): return [D*(np.random.rand(3)-0.5) for _ in range(N)]
```

We can use this function to create a $10\times 10\times 10$ cube of 20 points:

```python
pts = pointcube(20,10)
pts # Convenient way to print out the return value
```

**TODO: Illustration of points**

Compute distances from the point of interest (at the origin) to this new set of points:

```python
origin = coord(0,0,0)
ds = distances(origin,pts)
ds
```

Filter out the points close to the origin:

```python
ns = neighbors(ds,3)
ns
```

**TODO: Illustration of origin (red) and neighbors (blue)**


## Faster calculation of neighbor lists

Computing neighbor lists for all $N$ points requires $N(N-1)/2$ distance evaluations, and can become expensive for calculations on millions of points. We can do this calculation more rapidly by first binning the atoms into cells, and then only looping over the cells that are nearby.

We first want to determine the *bounding box* for the set of atoms which is the x, y, and z minimum and maximum coordinates. If we're using `pointcube` to generate the points this is trivial (and equal to $\pm D$ in each dimension). In general, however, the point cloud generated is more irregular, and finding the boundaries is important.

```python
def bounding_box(points,BIG=1_000_000):
    xmin=ymin=zmin=BIG
    xmax=ymax=zmax=-BIG
    for (x,y,z) in points: # automatically unpack the points into variabls
        xmin = min(xmin,x)
        xmax = max(xmax,x)
        ymin = min(ymin,y)
        ymax = max(ymax,y)
        zmin = min(zmin,z)
        zmax = max(zmax,z)
    return xmin,xmax,ymin,ymax,zmin,zmax
```

Running `bounding_box` on our earlier point cloud gives predictable results:

```python
bounding_box(pts)
```

**TODO: Illustration of bounding box**

Once we know the limits of the point cloud, we can bin them into groups of points. We will have $N_x, N_y, N_z$ bins in each dimension, and use a function to determine the index of the bins in each dimension:

```python
import math
def bin_index(x,xmin,xmax,Nx): return math.floor(Nx*(x-xmin)/(xmax-xmin))
```

We can take a pass through the points and put them into bins. First, create a dictionary that creates references to each of the bins, and then put each point into the relevant bins.

**TODO: Illustration of bins**

```python
def bin_points(pts,Nx,Ny,Nz):
    xmin,xmax,ymin,ymax,zmin,zmax = bounding_box(pts)
    binned = {(I,J,K):[] for I in range Nx J in range Ny K in range Nz}
    for pt in pts:
        I = map(bin_index(pt[0],xmin,xmax,Nx)
        J = map(bin_index(pt[1],ymin,ymax,Ny)
        K = map(bin_index(pt[2],zmin,zmax,Nz)
        binned[I,J,K].append(pt)
    return binned
```

**TODO: Compute neighbor lists**

## Representing atoms

At the most basic level, atoms require a position in space and an identity to the atom, and can be simply created using a python tuple:

```python
def atom(atno,coord): (atno,coord)
```

There are instances when more information is required. It is often convenient to have *labels* for atoms in order to be able to refer to a specific atom in a sea of many atoms of the same type. Molecular mechanics programs often need to define an *atom type*, since often the force-field for a $sp^3$ C is generally defined to be different from an $sp^2$ C. Quantum mechanics programs often define *counterpoise* atoms for basis set corrections. We will skip these additional features until we need them.

Rather than refer to the atomic number and the coordinate separately, we can either write helper functions to access these:

```python
def atom_atno(atom): return atom[0]
def atom_coord(atom): return atom[1]
```

Alternately, we can use Python's
[named tuples](https://docs.python.org/3.6/library/collections.html?highlight=namedtuple#collections.namedtuple)
to refer to these fields directly:

```python
import collections
Atom = collections.namedtuple('atom',('atno','coord'))
```

`namedtuple` allows the atoms to be defined and the fields to be accessed via:

```python
at1 = Atom(6,coord(0,0,0))
at1.atno, at1,coord
```

The routines for computing distances and binning points from the previous section can be trivially used for atomic coordinates. Often neighbor calculations make use of atomic-number-specific *atomic radii* to estimate when two atoms might be bonded.

```python
def bonded(at1,at2):
    return distance(at1.coord,at2,coord) < Rb[at1.atno]+Rb[at2.atno]
```

Typical bond radii through Xe are below:

```python
Rb = [1.000, 1.200, 1.400, 1.820, 1.372, # Be, 4
      0.795, 1.700, 1.550, 1.520, 1.470, # F,  9
      1.540, 2.270, 1.730, 1.700, 2.100, # Si, 14
      1.800, 1.800, 1.750, 1.880, 2.750, # K,  19
      2.450, 1.370, 1.370, 1.370, 1.370, # Cr, 24
      1.370, 1.456, 0.880, 0.690, 0.720, # Cu, 29
      0.740, 1.370, 1.950, 1.850, 1.900, # Se, 34
      1.850, 2.020, 1.580, 2.151, 1.801, # Y,  39
      1.602, 1.468, 1.526, 1.360, 1.339, # Ru, 44
      1.345, 1.376, 1.270, 1.424, 1.663, # In, 49
      2.100, 2.050, 2.060, 1.980, 2.000] # Xe, 54
```

## Computing Coulomb repulsion


