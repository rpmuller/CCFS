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

# Python Programming Basics


Python is the programming language of choice for many scientists to a large degree because it offers a great deal of power to analyze and model scientific data with relatively little overhead in terms of learning, installation or development time. It is a language you can pick up in a weekend, and use for the rest of your life.

The [Python Tutorial](https://docs.python.org/3/tutorial/) is a great place to start getting a feel for the language. To complement this material, I taught a Python Short Course years ago to a group of computational chemists during a time that I was worried the field was moving too much in the direction of using canned software rather than developing one's own methods. I wanted to focus on what working scientists needed to be more productive: parsing output of other programs, building simple models, experimenting with object oriented programming, extending the language with C, and simple GUIs.


This chapter will out of necessity just touch on the basics. For a thorough introduction to Python and the environment the book will be using, please consider carefully working through:
* [Python Tutorial](https://docs.python.org/3/tutorial/)
* [Jupyter Introduction](https://jupyter.org/try-jupyter/retro/notebooks/?path=notebooks/Intro.ipynb)
* [Matplotlib's Introduction to PyPlot](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)


## Installation


### Using Google Colab

The easiest way to load and experiment with these notebooks is using [Google Colaboratory](https://colab.research.google.com). You can load the various chapters using these links:

* [Python Programming Basics](https://colab.research.google.com/github/rpmuller/CCFS/blob/main/PythonBasics.ipynb)
* [Atoms and Molecular Geometry](https://colab.research.google.com/github/rpmuller/CCFS/blob/main/Geometry.ipynb)
* [Molecular Mechanics and Dynamics](https://colab.research.google.com/github/rpmuller/CCFS/blob/main/MechanicsDynamics.ipynb)
* [Quantum Chemistry](https://colab.research.google.com/github/rpmuller/CCFS/blob/main/QuantumChemistry.ipynb)
* [Molecular Graphics](https://colab.research.google.com/github/rpmuller/CCFS/blob/main/Graphics.ipynb)
* [Advanced Topics](https://colab.research.google.com/github/rpmuller/CCFS/blob/main/Advanced.ipynb)

Once instide Colab, you can edit and evaluate the code cells and experiment with changing the code.


### Using Anaconda
For working with the code in more depth, you will likely want to install your own Python environment. [Anaconda](https://docs.conda.io/en/latest/) is the standard way to maintain a variety of different Python environments for scientific programming. You can find installers on the [Miniconda](https://docs.conda.io/en/latest/miniconda.html) web site.

You can then install a suitable environment via

    % conda create -n CCFS python=3 numpy jupyter-lab matplotlib

activate the environment via

    % conda activate CCFS

You can clone the github repository using

    % git clone https://github.com/rpmuller/CCFS.git

enter the resulting `CCFS` directory, and start jupyter lab via

    % jupyter-lab

at which point you can open and edit the various notebooks.

## Introduction to Python

### Basic math and the python REPL

Jupyter provides a Read-Evaluator-Print-Loop (REPL) interface, where you can evaluate python expressions and perform many of the functions you would use a calculator to determine.

```python
2+2
```

```python
(50-5*6)/4
```

In the last few lines, we have sped by a lot of things that we should stop for a moment and explore a little more fully. We've seen, however briefly, two different data types: *integers*, also known as *whole numbers* to the non-programming world, and *floating point numbers*, also known (incorrectly) as *decimal numbers* to the rest of the world.

As of Python 3, division of two integers returns a floating point number, which is why the result of the previous cell is 5.0 instead of 5 as the quotient of 20 and 4.


Python has a huge number of libraries included with the distribution. To keep things simple, most of these variables and functions are not accessible from a normal Python interactive session. Instead, you have to import the name. For example, there is a `math` module containing many useful functions. To access, say, the square root function, you can either first import the `math` module

```python
import math
```

and then use a variety of math functions

```python
math.sqrt(3*3+4*4)
```

One could have alternately imported the `sqrt` function directly into the main scope and use the function without the `math` prefix:

```python
from math import sqrt
sqrt(3*3+4*4)
```

You can define variables using the equals sign:

```python
height = 3.0
width = 4.0
diagonal = sqrt(height*height + width*width)
area = height * width
```

If you try to access a variable that you haven't yet defined, you get an error:

```python
volume
```

and you need to define it:

```python
depth = 20
volume = area*depth
```

You can name a variable *almost* anything you want. It needs to start with an alphabetical character or "\_", can contain alphanumeric charcters plus underscores ("\_"). Certain words, however, are reserved for the language:

    and, as, assert, break, class, continue, def, del, elif, else, except, 
    exec, finally, for, from, global, if, import, in, is, lambda, not, or,
    pass, print, raise, return, try, while, with, yield

Trying to define a variable using one of these will result in a syntax error:

```python
del = 0
```

### Strings

Strings are lists of printable characters, and can be defined using either single quotes:

```python
'Hello, World!'
```

or double quotes:

```python
"Hello, Python world!"
```

But not both at the same time, unless you want one of the symbols to be part of the string.

```python
"He's a Rebel"
```

```python
'She asked, "How are you today?"'
```

Just like the other two data objects we're familiar with (ints and floats), you can assign a string to a variable:

```python
greeting = "Hello, World!"
```

The `print` statement is often used for printing character strings:

```python
print(greeting)
```

But it can also print data types other than strings:

```python
print("The area of the rectangle is ",area)
```

In the above snippet, the number `12.0` (stored in the variable `area`) is converted into a string before being printed out.


You can use the + operator to concatenate strings together:

```python
statement = "Hello," + " World!"
print(statement)
```

### Lists

Very often in a programming language, one wants to keep a group of similar items together. Python does this using a data type called **lists**.

```python
days_of_the_week = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"]
```

Python lists, like C, but unlike Fortran, use 0 as the index of the first element of a list. Thus, in this example, the 0 element is "Sunday", 1 is "Monday", and so on. If you need to access the *n*th element from the end of the list, you can use a negative index. For example, the -1 element of a list is the last element:

```python
days_of_the_week[-1]
```

You can add additional items to a list using the `.append()` method on an existing list:

```python
languages = ["Fortran","C","C++"]
languages.append("Python")
print(languages)
```

The `range` command is a convenient way to make sequential lists of numbers:

```python
list(range(10))
```

Note that range(n) starts at 0 and gives the sequential list of integers less than `n`. If you want to start at a different number, use `range(start,stop)`:

```python
list(range(2,8))
```

The lists created above with range have a default *step* of 1 between elements. You can also give a fixed step size via a third command:

```python
list(range(0,20,2))
```

Lists do not have to hold the same data type. For example,

```python
["Today",7,99.3,""]
```

However, it's good (but not essential) to use lists for similar objects that are somehow logically connected. If you want to group different data types together into a composite data object, it's best to use **tuples**, which we will learn about below.

You can find out how long a list is using the `len()` command:

```python
help(len)
```

```python
len(range(2,20,2))
```

### Iteration, Indentation, and Blocks
One of the most useful things you can do with lists is to *iterate* through them, i.e. to go through each element one at a time. To do this in Python, we use the `for` statement:

```python
for day in days_of_the_week:
    print(day)
```

This code snippet goes through each element of the list called `days_of_the_week` and assigns it to the variable `day`. It then executes everything in the indented block (in this case only one line of code, the print statement) using those variable assignments. When the program has gone through every element of the list, it exists the block.

(Almost) every programming language defines blocks of code in some way. In Fortran, one uses END statements (ENDDO, ENDIF, etc.) to define code blocks. In C, C++, and Perl, one uses curly braces {} to define these blocks.

Python uses a colon (":"), followed by indentation level to define code blocks. Everything at a higher level of indentation is taken to be in the same block. In the above example the block was only a single line, but we could have had longer blocks as well:

```python
for day in days_of_the_week:
    statement = "Today is " + day
    print(statement)
```

The `range` command is particularly useful with the `for` statement to execute loops of a specified length:

```python
for i in range(20):
    print("The square of ",i," is ",i*i)
```

### Slicing
Lists and strings have something in common that you might not suspect: they can both be treated as sequences. You already know that you can iterate through the elements of a list. You can also iterate through the letters in a string:

```python
for letter in "Sunday":
    print(letter)
```

This is only occasionally useful. Slightly more useful is the *slicing* operation, which you can also use on any sequence. We already know that we can use *indexing* to get the first element of a list:

```python
days_of_the_week[0]
```

If we want the list containing the first two elements of a list, we can do this via

```python
days_of_the_week[0:2]
```

or simply

```python
days_of_the_week[:2]
```

If we want the last items of the list, we can do this with negative slicing:

```python
days_of_the_week[-2:]
```

which is somewhat logically consistent with negative indices accessing the last elements of the list.

You can do:

```python
workdays = days_of_the_week[1:6]
print(workdays)
```

Since strings are sequences, you can also do this to them:

```python
day = "Sunday"
abbreviation = day[:3]
print(abbreviation)
```

If we really want to get fancy, we can pass a third element into the slice, which specifies a step length (just like a third argument to the `range` function specifies the step):

```python
numbers = range(0,40)
evens = numbers[2::2]
evens
```

Note that in this example I was even able to omit the second argument, so that the slice started at 2, went to the end of the list, and took every second element, to generate the list of even numbers less that 40.


### Booleans and Truth Testing
We have now learned a few data types. We have integers and floating point numbers, strings, and lists to contain them. We have also learned about lists, a container that can hold any data type. We have learned to print things out, and to iterate over items in lists. We will now learn about **boolean** variables that can be either True or False.

We invariably need some concept of *conditions* in programming to control branching behavior, to allow a program to react differently to different situations. If it's Monday, I'll go to work, but if it's Sunday, I'll sleep in. To do this in Python, we use a combination of **boolean** variables, which evaluate to either True or False, and `if` statements, that control branching based on boolean values.


For example:

```python
if day == "Sunday":
    print("Sleep in")
else:
    print("Go to work")
```

(Quick quiz: why did the snippet print "Go to work" here? What is the variable "day" set to?)

Let's take the snippet apart to see what happened. First, note the statement

```python
day == "Sunday"
```

If we evaluate it by itself, as we just did, we see that it returns a boolean value, False. The "==" operator performs *equality testing*. If the two items are equal, it returns True, otherwise it returns False. In this case, it is comparing two variables, the string "Sunday", and whatever is stored in the variable "day", which, in this case, is the other string "Saturday". Since the two strings are not equal to each other, the truth test has the false value.


The if statement that contains the truth test is followed by a code block (a colon followed by an indented block of code). If the boolean is true, it executes the code in that block. Since it is false in the above example, we don't see that code executed.

The first block of code is followed by an `else` statement, which is executed if nothing else in the above if statement is true. Since the value was false, this code is executed, which is why we see "Go to work".

You can compare any data types in Python:

```python
1 == 2
```

```python
50 == 2*25
```

```python
3 < 3.14159
```

```python
1 == 1.0
```

```python
1 != 0
```

```python
1 <= 2
```

```python
1 >= 1
```

We see a few other boolean operators here, all of which which should be self-explanatory. Less than, equality, non-equality, and so on.

Particularly interesting is the 1 == 1.0 test, which is true, since even though the two objects are different data types (integer and floating point number), they have the same *value*. There is another boolean operator `is`, that tests whether two objects are the same object:

```python
a = 1
b = 1.0
a is b
```

We can do boolean tests on lists as well:

```python
[1,2,3] == [1,2,4]
```

```python
[1,2,3] < [1,2,4]
```

Finally, note that you can also string multiple comparisons together, which can result in very intuitive tests:

```python
hours = 5
0 < hours < 24
```

If statements can have `elif` parts ("else if"), in addition to if/else parts. For example:

```python
if day == "Sunday":
    print("Sleep in")
elif day == "Saturday":
    print("Do chores")
else:
    print("Go to work")
```

Of course we can combine if statements with for loops, to make a snippet that is almost interesting:

```python
for day in days_of_the_week:
    statement = "Today is " + day
    print(statement)
    if day == "Sunday":
        print("   Sleep in")
    elif day == "Saturday":
        print("   Do chores")
    else:
        print("   Go to work")
```

This is something of an advanced topic, but ordinary data types have boolean values associated with them, and, indeed, in early versions of Python there was not a separate boolean object. Essentially, anything that was a 0 value (the integer or floating point 0, an empty string "", or an empty list []) was False, and everything else was true. You can see the boolean value of any data object using the `bool` function.

```python
bool(1)
```

```python
bool(0)
```

```python
bool(["This "," is "," a "," list"])
```

### Code Example: The Fibonacci Sequence
The [Fibonacci sequence](http://en.wikipedia.org/wiki/Fibonacci_number) is a sequence in math that starts with 0 and 1, and then each successive entry is the sum of the previous two. Thus, the sequence goes 0,1,1,2,3,5,8,13,21,34,55,89,...

A very common exercise in programming books is to compute the Fibonacci sequence up to some number `n`. First I'll show the code, then I'll discuss what it is doing.

```python
n = 10
sequence = [0,1]
for i in range(2,n): # This is going to be a problem if we ever set n <= 2!
    sequence.append(sequence[i-1]+sequence[i-2])
print(sequence)
```

Let's go through this line by line. First, we define the variable `n`, and set it to the integer 20. `n` is the length of the sequence we're going to form, and should probably have a better variable name. We then create a variable called `sequence`, and initialize it to the list with the integers 0 and 1 in it, the first two elements of the Fibonacci sequence. We have to create these elements "by hand", since the iterative part of the sequence requires two previous elements.

We then have a for loop over the list of integers from 2 (the next element of the list) to `n` (the length of the sequence). After the colon, we see a hash tag "#", and then a **comment** that if we had set `n` to some number less than 2 we would have a problem. Comments in Python start with #, and are good ways to make notes to yourself or to a user of your code explaining why you did what you did. Better than the comment here would be to test to make sure the value of `n` is valid, and to complain if it isn't; we'll try this later.

In the body of the loop, we append to the list an integer equal to the sum of the two previous elements of the list.

After exiting the loop (ending the indentation) we then print out the whole list. That's it!


### Functions
We might want to use the Fibonacci snippet with different sequence lengths. We could cut an paste the code into another cell, changing the value of `n`, but it's easier and more useful to make a function out of the code. We do this with the `def` statement in Python:

```python
def fibonacci(sequence_length):
    "Return the Fibonacci sequence of length *sequence_length*"
    sequence = [0,1]
    if sequence_length < 1:
        print("Fibonacci sequence only defined for length 1 or greater")
        return
    if 0 < sequence_length < 3:
        return sequence[:sequence_length]
    for i in range(2,sequence_length): 
        sequence.append(sequence[i-1]+sequence[i-2])
    return sequence
```

We can now call `fibonacci` for different sequence_lengths:

```python
fibonacci(2)
```

```python
fibonacci(12)
```

We've introduced a several new features here. First, note that the function itself is defined as a code block (a colon followed by an indented block). This is the standard way that Python delimits things. Next, note that the first line of the function is a single string. This is called a **docstring**, and is a special kind of comment that is often available to people using the function through the python command line:

```python
help(fibonacci)
```

If you define a docstring for all of your functions, it makes it easier for other people to use them, since they can get help on the arguments and return values of the function.

Next, note that rather than putting a comment in about what input values lead to errors, we have some testing of these values, followed by a warning if the value is invalid, and some conditional code to handle special cases.


### Recursion and Factorials
Functions can also call themselves, something that is often called *recursion*. We're going to experiment with recursion by computing the factorial function. The factorial is defined for a positive integer `n` as
    
$$ n! = n(n-1)(n-2)\cdots 1 $$

First, note that we don't need to write a function at all, since this is a function built into the standard math library. Let's use the help function to find out about it:

```python
from math import factorial
help(factorial)
```

This is clearly what we want.

```python
factorial(20)
```

However, if we did want to write a function ourselves, we could do recursively by noting that

$$ n! = n(n-1)!$$

The program then looks something like:

```python
def fact(n):
    if n <= 0:
        return 1
    return n*fact(n-1)
```

```python
fact(20)
```

Recursion can be very elegant, and can lead to very simple programs.


### Two More Data Structures: Tuples and Dictionaries
Before we end the Python overview, I wanted to touch on two more data structures that are very useful (and thus very common) in Python programs.

A **tuple** is a sequence object like a list or a string. It's constructed by grouping a sequence of objects together with commas, either without brackets, or with parentheses:

```python
t = (1,2,'hi',9.0)
t
```

Tuples are like lists, in that you can access the elements using indices:

```python
t[1]
```

However, tuples are *immutable*, you can't append to them or change the elements of them:

```python
t.append(7)
```

```python
t[1]=77
```

Tuples are useful anytime you want to group different pieces of data together in an object, but don't want to create a full-fledged class (see below) for them. For example, let's say you want the Cartesian coordinates of some objects in your program. Tuples are a good way to do this:

```python
('Bob',0.0,21.0)
```

Again, it's not a necessary distinction, but one way to distinguish tuples and lists is that tuples are a collection of different things, here a name, and x and y coordinates, whereas a list is a collection of similar things, like if we wanted a list of those coordinates:

```python
positions = [
             ('Bob',0.0,21.0),
             ('Cat',2.5,13.1),
             ('Dog',33.0,1.2)
             ]
```

Tuples can be used when functions return more than one value. Say we wanted to compute the smallest x- and y-coordinates of the above list of objects. We could write:

```python
def minmax(objects):
    minx = 1e20 # These are set to really big numbers
    miny = 1e20
    for obj in objects:
        name,x,y = obj
        if x < minx: 
            minx = x
        if y < miny:
            miny = y
    return minx,miny

x,y = minmax(positions)
print(x,y)
```

Here we did two things with tuples you haven't seen before. First, we unpacked an object into a set of named variables using *tuple assignment*:

    name,x,y = obj

We also returned multiple values (minx,miny), which were then assigned to two other variables (x,y), again by tuple assignment. This makes what would have been complicated code in C++ rather simple.

Tuple assignment is also a convenient way to swap variables:

```python
x,y = 1,2
y,x = x,y
x,y
```

**Dictionaries** are an object called "mappings" or "associative arrays" in other languages. Whereas a list associates an integer index with a set of objects:

```python
mylist = [1,2,9,21]
```

The index in a dictionary is called the *key*, and the corresponding dictionary entry is the *value*. A dictionary can use (almost) anything as the key. Whereas lists are formed with square brackets [], dictionaries use curly brackets {}:

```python
ages = {"Rick": 46, "Bob": 86, "Fred": 21}
print("Rick's age is ",ages["Rick"])
```

There's also a convenient way to create dictionaries without having to quote the keys.

```python
dict(Rick=46,Bob=86,Fred=20)
```

The `len` command works on both tuples and dictionaries:

```python
t = ('Bob',0.0,21.0)
len(t)
```

```python
len(ages)
```

### Plotting with Matplotlib
One of the things Jupyter notebooks lets you do is have plots in-lined

We can generally understand trends in data by using a plotting program to chart it. Python has a wonderful plotting library called [Matplotlib](http://matplotlib.org). The Jupyter notebook interface we are using for these notes has that functionality built in.

To import matplotlib, do:

```python
from matplotlib import pyplot as plt
```

As an example, we have looked at two different functions, the Fibonacci function, and the factorial function, both of which grow faster than polynomially. Which one grows the fastest? Let's plot them. First, let's generate the Fibonacci sequence of length 20:

```python
fibs = fibonacci(10)
```

Next lets generate the factorials.

```python
facts = []
for i in range(10):
    facts.append(factorial(i))
```

Now we use the Matplotlib function `plot` to compare the two.

```python
plt.plot(facts,label="factorial")
plt.plot(fibs,label="Fibonacci")
plt.xlabel("n")
plt.legend()
plt.title("Comparison of factorial and Fibonacci series")
```

The factorial function grows much faster. In fact, you can't even see the Fibonacci sequence. It's not entirely surprising: a function where we multiply by n each iteration is bound to grow faster than one where we add (roughly) n each iteration.

Let's plot these on a semilog plot so we can see them both a little more clearly:

```python
plt.semilogy(facts,label="factorial")
plt.semilogy(fibs,label="Fibonacci")
plt.xlabel("n")
plt.legend()
```

There are many more things you can do with Matplotlib. We'll be looking at some of them in the sections to come. In the meantime, if you want an idea of the different things you can do, look at the Matplotlib [Gallery](http://matplotlib.org/gallery.html). Rob Johansson's IPython notebook [Introduction to Matplotlib](http://nbviewer.ipython.org/urls/raw.github.com/jrjohansson/scientific-python-lectures/master/Lecture-4-Matplotlib.ipynb) is also particularly good.

## Numpy and Scipy

[Numpy](http://numpy.org) contains core routines for doing fast vector, matrix, and linear algebra-type operations in Python. [Scipy](http://scipy) contains additional routines for optimization, special functions, and so on. Both contain modules written in C and Fortran so that they're as fast as possible. Together, they give Python roughly the same capability that the [Matlab](http://www.mathworks.com/products/matlab/) program offers. (In fact, if you're an experienced Matlab user, there a [guide to Numpy for Matlab users](http://www.scipy.org/NumPy_for_Matlab_Users) just for you.)

Assuming everything is properly installed, you can import the numpy module via the command
```python
import numpy as np
```
It is standard to use the shorthand `np` for the numpy library to save typing.

Fundamental to both Numpy and Scipy is the ability to work with vectors and matrices. You can create vectors from lists using the `array` command:

```python
array([1,2,3,4,5,6])
```

You can pass in a second argument to `array` that gives the numeric type. There are a number of types [listed here](http://docs.scipy.org/doc/numpy/user/basics.types.html) that your matrix can be. Some of these are aliased to single character codes. The most common ones are np.double (double precision floating point number), np.cdouble (double precision complex number), and np.int_ (long int). Examples of arrays created with specific types are:

```python
array([1,2,3,4,5,6],np.double)
```

```python
array([1,2,3,4,5,6],np.cdouble)
```

```python
array([1,2,3,4,5,6],np.int_)
```

To build matrices, you can either use the array command with lists of lists:

```python
array([[0,1],[1,0]],np.double)
```

You can also form all-zero matrices of arbitrary shape (including vectors, which Numpy treats as vectors with one row), using the `zeros` command:

```python
zeros((3,3),np.double)
```

The first argument is a tuple containing the shape of the matrix, and the second is the data type argument, which follows the same conventions as in the array command. Thus, you can make row vectors:

```python
zeros(3,np.double)
```

```python
zeros((1,3),np.double)
```

or column vectors:

```python
zeros((3,1),np.double)
```

There's also an `identity` command that behaves as you'd expect:

```python
identity(4,np.double)
```

as well as a similar `ones` command.

## Linspace, matrix functions, and plotting
The `linspace` command makes a linear array of points from a starting to an ending value.

```python
linspace(0,1)
```

If you provide a third argument, it takes that as the number of points in the space. If you don't provide the argument, it gives a length 50 linear space.

```python
linspace(0,1,11)
```

`linspace` is an easy way to make coordinates for plotting. Functions in the numpy library (all of which are imported into IPython notebook) can act on an entire vector (or even a matrix) of points at once. Thus,

```python
x = linspace(0,2*pi)
sin(x)
```

In conjunction with `matplotlib`, this is a nice way to plot things:

```python
plot(x,sin(x))
```

## Matrix operations
Matrix objects act sensibly when multiplied by scalars:

```python
0.125*identity(3,'d')
```

as well as when you add two matrices together. (However, the matrices have to be the same shape.)

```python
identity(2,'d') + array([[1,1],[1,2]])
```

Something that confuses Matlab users is that the times (*) operator give element-wise multiplication rather than matrix multiplication:

```python
identity(2)*ones((2,2))
```

To get matrix multiplication, you need the `dot` command:

```python
dot(identity(2),ones((2,2)))
```

`dot` can also do dot products (duh!):

```python
v = array([3,4],'d')
sqrt(dot(v,v))
```

as well as matrix-vector products.


There are `determinant`, `inverse`, and `transpose` functions that act as you would suppose. Transpose can be abbreviated with ".T" at the end of a matrix object:

```python
m = array([[1,2],[3,4]])
m.T
```

There's also a `diag` function that takes a list or a vector and puts it along the diagonal of a square matrix. 

```python
diag([1,2,3,4,5])
```

We'll find this useful later on.


## Matrix Solvers
You can solve systems of linear equations using the `solve` command:

```python
A = array([[1,1,1],[0,2,5],[2,5,-1]])
b = array([6,-4,27])
solve(A,b)
```

There are a number of routines to compute eigenvalues and eigenvectors

* `eigvals` returns the eigenvalues of a matrix
* `eigvalsh` returns the eigenvalues of a Hermitian matrix
* `eig` returns the eigenvalues and eigenvectors of a matrix
* `eigh` returns the eigenvalues and eigenvectors of a Hermitian matrix.

```python
A = array([[13,-4],[-4,7]],'d')
eigvalsh(A)
```

```python
eigh(A)
```

## Example: Finite Differences
Now that we have these tools in our toolbox, we can start to do some cool stuff with it. Many of the equations we want to solve in Physics involve differential equations. We want to be able to compute the derivative of functions:

$$ y' = \frac{y(x+h)-y(x)}{h} $$

by *discretizing* the function $y(x)$ on an evenly spaced set of points $x_0, x_1, \dots, x_n$, yielding $y_0, y_1, \dots, y_n$. Using the discretization, we can approximate the derivative by

$$ y_i' \approx \frac{y_{i+1}-y_{i-1}}{x_{i+1}-x_{i-1}} $$

We can write a derivative function in Python via

```python
def nderiv(y,x):
    "Finite difference derivative of the function f"
    n = len(y)
    d = zeros(n,'d') # assume double
    # Use centered differences for the interior points, one-sided differences for the ends
    for i in range(1,n-1):
        d[i] = (y[i+1]-y[i-1])/(x[i+1]-x[i-1])
    d[0] = (y[1]-y[0])/(x[1]-x[0])
    d[n-1] = (y[n-1]-y[n-2])/(x[n-1]-x[n-2])
    return d
```

Let's see whether this works for our sin example from above:

```python
x = linspace(0,2*pi)
dsin = nderiv(sin(x),x)
plot(x,dsin,label='numerical')
plot(x,cos(x),label='analytical')
title("Comparison of numerical and analytical derivatives of sin(x)")
legend()
```

Pretty close!


## One-Dimensional Harmonic Oscillator using Finite Difference
Now that we've convinced ourselves that finite differences aren't a terrible approximation, let's see if we can use this to solve the one-dimensional harmonic oscillator.

We want to solve the time-independent Schrodinger equation

$$ -\frac{\hbar^2}{2m}\frac{\partial^2\psi(x)}{\partial x^2} + V(x)\psi(x) = E\psi(x)$$

for $\psi(x)$ when $V(x)=\frac{1}{2}m\omega^2x^2$ is the harmonic oscillator potential. We're going to use the standard trick to transform the differential equation into a matrix equation by multiplying both sides by $\psi^*(x)$ and integrating over $x$. This yields

$$ -\frac{\hbar}{2m}\int\psi(x)\frac{\partial^2}{\partial x^2}\psi(x)dx + \int\psi(x)V(x)\psi(x)dx = E$$

We will again use the finite difference approximation. The finite difference formula for the second derivative is

$$ y'' = \frac{y_{i+1}-2y_i+y_{i-1}}{x_{i+1}-x_{i-1}} $$

We can think of the first term in the Schrodinger equation as the overlap of the wave function $\psi(x)$ with the second derivative of the wave function $\frac{\partial^2}{\partial x^2}\psi(x)$. Given the above expression for the second derivative, we can see if we take the overlap of the states $y_1,\dots,y_n$ with the second derivative, we will only have three points where the overlap is nonzero, at $y_{i-1}$, $y_i$, and $y_{i+1}$. In matrix form, this leads to the tridiagonal Laplacian matrix, which has -2's along the diagonals, and 1's along the diagonals above and below the main diagonal.

The second term turns leads to a diagonal matrix with $V(x_i)$ on the diagonal elements. Putting all of these pieces together, we get:

```python
def Laplacian(x):
    h = x[1]-x[0] # assume uniformly spaced points
    n = len(x)
    M = -2*identity(n,'d')
    for i in range(1,n):
        M[i,i-1] = M[i-1,i] = 1
    return M/h**2
```

```python
x = linspace(-3,3)
m = 1.0
ohm = 1.0
T = (-0.5/m)*Laplacian(x)
V = 0.5*(ohm**2)*(x**2)
H =  T + diag(V)
E,U = eigh(H)
h = x[1]-x[0]
plot(x,V,color='k')
for i in range(4):
    # For each of the first few solutions, plot the energy level:
    axhline(y=E[i],color='k',ls=":")
    # as well as the eigenfunction, displaced by the energy level so they don't
    # all pile up on each other:
    plot(x,-U[:,i]/sqrt(h)+E[i])
title("Eigenfunctions of the Quantum Harmonic Oscillator")
xlabel("Displacement (bohr)")
ylabel("Energy (hartree)")
```

We've made a couple of hacks here to get the orbitals the way we want them. First, I inserted a -1 factor before the wave functions, to fix the phase of the lowest state. The phase (sign) of a quantum wave function doesn't hold any information, only the square of the wave function does, so this doesn't really change anything. 

But the eigenfunctions as we generate them aren't properly normalized. The reason is that finite difference isn't a real basis in the quantum mechanical sense. It's a basis of Dirac δ functions at each point; we interpret the space betwen the points as being "filled" by the wave function, but the finite difference basis only has the solution being at the points themselves. We can fix this by dividing the eigenfunctions of our finite difference Hamiltonian by the square root of the spacing, and this gives properly normalized functions.


## Special Functions
The solutions to the Harmonic Oscillator are supposed to be Hermite polynomials. The Wikipedia page has the HO states given by

$$\psi_n(x) = \frac{1}{\sqrt{2^n n!}}
\left(\frac{m\omega}{\pi\hbar}\right)^{1/4}
\exp\left(-\frac{m\omega x^2}{2\hbar}\right)
H_n\left(\sqrt{\frac{m\omega}{\hbar}}x\right)$$

Let's see whether they look like those. There are some special functions in the Numpy library, and some more in Scipy. Hermite Polynomials are in Numpy:

```python
from numpy.polynomial.hermite import Hermite
def ho_evec(x,n,m,ohm):
    vec = [0]*9
    vec[n] = 1
    Hn = Hermite(vec)
    return (1/sqrt(2**n*factorial(n)))*pow(m*ohm/pi,0.25)*exp(-0.5*m*ohm*x**2)*Hn(x*sqrt(m*ohm))
```

Let's compare the first function to our solution.

```python
plot(x,ho_evec(x,0,1,1),label="Analytic")
plot(x,-U[:,0]/sqrt(h),label="Numeric")
xlabel('x (bohr)')
ylabel(r'$\psi(x)$')
title("Comparison of numeric and analytic solutions to the Harmonic Oscillator")
legend()
```

The agreement is almost exact.


We can use the `subplot` command to put multiple comparisons in different panes on a single plot:

```python
phase_correction = [-1,1,1,-1,-1,1]
for i in range(6):
    subplot(2,3,i+1)
    plot(x,ho_evec(x,i,1,1),label="Analytic")
    plot(x,phase_correction[i]*U[:,i]/sqrt(h),label="Numeric")
```

Other than phase errors (which I've corrected with a little hack: can you find it?), the agreement is pretty good, although it gets worse the higher in energy we get, in part because we used only 50 points.

The Scipy module has many more special functions:

```python
from scipy.special import airy,jn,eval_chebyt,eval_legendre
subplot(2,2,1)
x = linspace(-1,1)
Ai,Aip,Bi,Bip = airy(x)
plot(x,Ai)
plot(x,Aip)
plot(x,Bi)
plot(x,Bip)
title("Airy functions")
subplot(2,2,2)
x = linspace(0,10)
for i in range(4):
    plot(x,jn(i,x))
title("Bessel functions")
subplot(2,2,3)
x = linspace(-1,1)
for i in range(6):
    plot(x,eval_chebyt(i,x))
title("Chebyshev polynomials of the first kind")
subplot(2,2,4)
x = linspace(-1,1)
for i in range(6):
    plot(x,eval_legendre(i,x))
title("Legendre polynomials")
```

As well as Jacobi, Laguerre, Hermite polynomials, Hypergeometric functions, and many others. There's a full listing at the [Scipy Special Functions Page](http://docs.scipy.org/doc/scipy/reference/special.html).


## Least squares fitting
Very often we deal with some data that we want to fit to some sort of expected behavior. Say we have the following:

```python
raw_data = """\
3.1905781584582433,0.028208609537968457
4.346895074946466,0.007160804747670053
5.374732334047101,0.0046962988461934805
8.201284796573875,0.0004614473299618756
10.899357601713055,0.00005038370219939726
16.295503211991434,4.377451812785309e-7
21.82012847965739,3.0799922117601088e-9
32.48394004282656,1.524776208284536e-13
43.53319057815846,5.5012073588707224e-18"""
```

There's a section below on parsing CSV data. We'll steal the parser from that. For an explanation, skip ahead to that section. Otherwise, just assume that this is a way to parse that text into a numpy array that we can plot and do other analyses with.

```python
data = []
for line in raw_data.splitlines():
    words = line.split(',')
    data.append(map(float,words))
data = array(data)
```

```python
title("Raw Data")
xlabel("Distance")
plot(data[:,0],data[:,1],'bo')
```

Since we expect the data to have an exponential decay, we can plot it using a semi-log plot.

```python
title("Raw Data")
xlabel("Distance")
semilogy(data[:,0],data[:,1],'bo')
```

For a pure exponential decay like this, we can fit the log of the data to a straight line. The above plot suggests this is a good approximation. Given a function
$$ y = Ae^{-ax} $$
$$ \log(y) = \log(A) - ax$$
Thus, if we fit the log of the data versus x, we should get a straight line with slope $a$, and an intercept that gives the constant $A$.

There's a numpy function called `polyfit` that will fit data to a polynomial form. We'll use this to fit to a straight line (a polynomial of order 1)

```python
params = polyfit(data[:,0],log(data[:,1]),1)
a = params[0]
A = exp(params[1])
```

Let's see whether this curve fits the data.

```python
x = linspace(1,45)
title("Raw Data")
xlabel("Distance")
semilogy(data[:,0],data[:,1],'bo')
semilogy(x,A*exp(a*x),'b-')
```

If we have more complicated functions, we may not be able to get away with fitting to a simple polynomial. Consider the following data:

```python
gauss_data = """\
-0.9902286902286903,1.4065274110372852e-19
-0.7566104566104566,2.2504438576596563e-18
-0.5117810117810118,1.9459459459459454
-0.31887271887271884,10.621621621621626
-0.250997150997151,15.891891891891893
-0.1463309463309464,23.756756756756754
-0.07267267267267263,28.135135135135133
-0.04426734426734419,29.02702702702703
-0.0015939015939017698,29.675675675675677
0.04689304689304685,29.10810810810811
0.0840994840994842,27.324324324324326
0.1700546700546699,22.216216216216214
0.370878570878571,7.540540540540545
0.5338338338338338,1.621621621621618
0.722014322014322,0.08108108108108068
0.9926849926849926,-0.08108108108108646"""
data = []
for line in gauss_data.splitlines():
    words = line.split(',')
    data.append(map(float,words))
data = array(data)
plot(data[:,0],data[:,1],'bo')
```

This data looks more Gaussian than exponential. If we wanted to, we could use `polyfit` for this as well, but let's use the `curve_fit` function from Scipy, which can fit to arbitrary functions. You can learn more using help(curve_fit).

First define a general Gaussian function to fit to.

```python
def gauss(x,A,a): return A*exp(a*x**2)
```

Now fit to it using `curve_fit`:

```python
from scipy.optimize import curve_fit
params,conv = curve_fit(gauss,data[:,0],data[:,1])
x = linspace(-1,1)
plot(data[:,0],data[:,1],'bo')
A,a = params
plot(x,gauss(x,A,a),'b-')
```

The `curve_fit` routine we just used is built on top of a very good general **minimization** capability in Scipy. You can learn more [at the scipy documentation pages](http://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.minimize.html).


## Monte Carlo, random numbers, and computing $\pi$
Many methods in scientific computing rely on Monte Carlo integration, where a sequence of (pseudo) random numbers are used to approximate the integral of a function. Python has good random number generators in the standard library. The `random` function gives pseudorandom numbers uniformly distributed between 0 and 1:

```python
from random import random
rands = []
for i in range(100):
    rands.append(random())
plot(rands)
```

`random` uses the [Mersenne Twister](http://www.math.sci.hiroshima-u.ac.jp/~m-mat/MT/emt.html) algorithm, which is a highly regarded pseudorandom number generator. There are also functions to generate random integers, to randomly shuffle a list, and functions to pick random numbers from a particular distribution, like the normal distribution:

```python
from random import gauss
grands = []
for i in range(100):
    grands.append(gauss(0,1))
plot(grands)
```

It is generally more efficient to generate a list of random numbers all at once, particularly if you're drawing from a non-uniform distribution. Numpy has functions to generate vectors and matrices of particular types of random distributions.

```python
plot(rand(100))
```

One of the first programs I ever wrote was a program to compute $\pi$ by taking random numbers as x and y coordinates, and counting how many of them were in the unit circle. For example:

```python
npts = 5000
xs = 2*rand(npts)-1
ys = 2*rand(npts)-1
r = xs**2+ys**2
ninside = (r<1).sum()
figsize(6,6) # make the figure square
title("Approximation to pi = %f" % (4*ninside/float(npts)))
plot(xs[r<1],ys[r<1],'b.')
plot(xs[r>1],ys[r>1],'r.')
figsize(8,6) # change the figsize back to 4x3 for the rest of the notebook
```

The idea behind the program is that the ratio of the area of the unit circle to the square that inscribes it is $\pi/4$, so by counting the fraction of the random points in the square that are inside the circle, we get increasingly good estimates to $\pi$. 

The above code uses some higher level Numpy tricks to compute the radius of each point in a single line, to count how many radii are below one in a single line, and to filter the x,y points based on their radii. To be honest, I rarely write code like this: I find some of these Numpy tricks a little too cute to remember them, and I'm more likely to use a list comprehension (see below) to filter the points I want, since I can remember that.

As methods of computing $\pi$ go, this is among the worst. A much better method is to use Leibniz's expansion of arctan(1):

$$\frac{\pi}{4} = \sum_k \frac{(-1)^k}{2*k+1}$$

```python
n = 100
total = 0
for k in range(n):
    total += pow(-1,k)/(2*k+1.0)
print 4*total
```

If you're interested a great method, check out [Ramanujan's method](http://en.wikipedia.org/wiki/Approximations_of_%CF%80). This converges so fast you really need arbitrary precision math to display enough decimal places. You can do this with the Python `decimal` module, if you're interested.


## Numerical Integration
Integration can be hard, and sometimes it's easier to work out a definite integral using an approximation. For example, suppose we wanted to figure out the integral:

$$\int_0^\infty\exp(-x)dx=1$$

```python
from numpy import sqrt
def f(x): return exp(-x)
x = linspace(0,10)
plot(x,exp(-x))
```

Scipy has a numerical integration routine `quad` (since sometimes numerical integration is called *quadrature*), that we can use for this:

```python
from scipy.integrate import quad
quad(f,0,inf)
```

There are also 2d and 3d numerical integrators in Scipy. [See the docs](http://docs.scipy.org/doc/scipy/reference/integrate.html) for more information.


## Fast Fourier Transform and Signal Processing

Very often we want to use FFT techniques to help obtain the signal from noisy data. Scipy has several different options for this.

```python
from scipy.fftpack import fft,fftfreq
npts = 4000
nplot = npts/10
t = linspace(0,120,npts)
def acc(t): return 10*sin(2*pi*2.0*t) + 5*sin(2*pi*8.0*t) + 2*rand(npts)
signal = acc(t)
FFT = abs(fft(signal))
freqs = fftfreq(npts, t[1]-t[0])
subplot(211)
plot(t[:nplot], signal[:nplot])
subplot(212)
plot(freqs,20*log10(FFT),',')
show()
```

There are additional signal processing routines in Scipy that you can [read about here](http://docs.scipy.org/doc/scipy/reference/tutorial/signal.html).


## Why CCFS Uses Only a Subset of Python


Despite the [Zen of Python's](https://peps.python.org/pep-0020/) assurances that there should be only one way to do things, any programming language offers many different methods of storing data and operating on those data structures. This book will strive to produce the *simplest readable code*, which in general will mean eschewing many of the advanced language facilities like classes and decorators. The benefit to this choice is that the resulting understandable code will often be trivial to express in other languages as well, and we will supply versions of the modules produced here in other languages, and encourage users to explore (and return to us) choices in still more languages.

There are several inspirations for this minimalist approach to programming. This first is Abelson and Sussman's [Structure and Interpretation of Computer Programs](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book-Z-H-4.html#%_toc_start) (SICP), possibly the best programming book ever written. SICP uses a subset of the Scheme programming language for the book, even though the book touches on very advanced topics in programming like creating interpreters with different variable binding rules. SICP's minimalism helps the reader focus on the details of the implementation rather than the details of the language that I would like to capture here.

Along similar lines is the work that Peter Norvig has done in a number of places, but the most notable is his Udacity course [Design of Computer Programs](https://www.udacity.com/course/design-of-computer-programs--cs212). Again, it is remarkable that Norvig demonstrates very advanced applications like a poker-playing program using language features rarely more advanced than a Python list. Norvig's [pytudes](https://github.com/norvig/pytudes) ("Python etudes") that solve a variety of programming problems in a similar very simple programming style are also highly recommended.

## Futher Reading
Here's a collection of the references mentioned and other sources of information on computer programming in general and Python in particular.

- [Python Tutorial](https://docs.python.org/3/tutorial/)
- [Jupyter Introduction](https://jupyter.org/try-jupyter/retro/notebooks/?path=notebooks/Intro.ipynb)
- [Matplotlib's Introduction to PyPlot](https://matplotlib.org/stable/tutorials/introductory/pyplot.html)
- [Google Colaboratory](https://colab.research.google.com)
- [Anaconda](https://docs.conda.io/en/latest/)
- [Zen of Python's](https://peps.python.org/pep-0020/)


- [Numpy](http://numpy.org)
- [Numpy for Matlab users](http://www.scipy.org/NumPy_for_Matlab_Users)
- [Scipy](http://scipy)
- [Scipy tutorial](http://docs.scipy.org/doc/scipy/reference/tutorial/signal.html)

- Abelson and Sussman's [Structure and Interpretation of Computer Programs](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book-Z-H-4.html#%_toc_start)
- Peter Norvig's [Design of Computer Programs](https://www.udacity.com/course/design-of-computer-programs--cs212) Udacity
Class.
