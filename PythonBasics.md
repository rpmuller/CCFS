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

The `range()` command is particularly useful with the `for` statement to execute loops of a specified length:

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

If we really want to get fancy, we can pass a third element into the slice, which specifies a step length (just like a third argument to the `range()` function specifies the step):

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
1 is 1.0
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

This is something of an advanced topic, but ordinary data types have boolean values associated with them, and, indeed, in early versions of Python there was not a separate boolean object. Essentially, anything that was a 0 value (the integer or floating point 0, an empty string "", or an empty list []) was False, and everything else was true. You can see the boolean value of any data object using the `bool()` function.

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

We can now call `fibonacci()` for different sequence_lengths:

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

```python
name,x,y = obj
```

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

The `len()` command works on both tuples and dictionaries:

```python
len(t)
```

```python
len(ages)
```

### Plotting with Matplotlib
One of the things Jupyter notebooks lets you do is have plots in-lined

We can generally understand trends in data by using a plotting program to chart it. Python has a wonderful plotting library called [Matplotlib](http://matplotlib.org). The IPython notebook interface we are using for these notes has that functionality built in.

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
figsize(8,6)
plot(facts,label="factorial")
plot(fibs,label="Fibonacci")
xlabel("n")
legend()
```

The factorial function grows much faster. In fact, you can't even see the Fibonacci sequence. It's not entirely surprising: a function where we multiply by n each iteration is bound to grow faster than one where we add (roughly) n each iteration.

Let's plot these on a semilog plot so we can see them both a little more clearly:

```python
semilogy(facts,label="factorial")
semilogy(fibs,label="Fibonacci")
xlabel("n")
legend()
```

There are many more things you can do with Matplotlib. We'll be looking at some of them in the sections to come. In the meantime, if you want an idea of the different things you can do, look at the Matplotlib [Gallery](http://matplotlib.org/gallery.html). Rob Johansson's IPython notebook [Introduction to Matplotlib](http://nbviewer.ipython.org/urls/raw.github.com/jrjohansson/scientific-python-lectures/master/Lecture-4-Matplotlib.ipynb) is also particularly good.



## Why CCFS Uses Only a Subset of Python

```python

```
