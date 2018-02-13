---
layout: post
title: STRING MANIPULATION, GUESS-and-CHECK, APPOXIMATEIONS, BISECTION
date: 2018-02-13
categories: blog
tags: [MIT, Python]
description: MIT Open Course of Python
---

## TODAY
------
* string manipulation 
* guess and check algorithms
* approximate solutions
* bisection method

## STRINGS
------
* think of as a **sequence** of case sensitive characters
* can compare strings with `==`, `>`, `<` etc.
* `len()` is a function used to retrieve the **length** of string in the parentheses

```python
s = "abc"
len(s) # -> evaluates to 3
```

------
* squere brackets used to perform **indexing** into a string to get the value at a certain index/position

```python
s = "abc"
# index :  0  1  2 <- index always starts at 0
# index : -3 -2 -1 <- last element always at index = -1
```

------
* can **slice** strings using `[start:stop:step]`
* if give two numbers, `[start:stop], step = 1` by default
* you can also omit numbers and leave just colons

```python
s = "abcdefgh"
s[3:6]		# -> evaluates to "def", same as s[3:6:1]
s[3:6:2] 	# -> evaluates to "df"
s[::]		# -> evaluates to "abcdefgh", same as s[0:len(s):1]
s[::-1]		# -> evaluates to "hgfedbca", same as s[-1:-(len(s)+1):-1]
s[4:1:-2]	# -> evaluates to "ec"
```

------
* stirngs are **immutable** - cannot be modified

```python
s = "hello"
s[0] = 'y'		# -> given an error
s = 'y' + s[1:len(s)]	# -> is allowed, s bound to new object
```

### for LOOPS RECAP
------
* `for` loops have a **loop variable** that iterates over a set of values

```python
for var in range(4):		# -> `var` iterates over values 0,1,2,3
    <expressions>		# expressions inside loop executed with each value for var

for var in range(4,6):		# -> `var` iterates over values 4, 5
    <expressions>
```

* `range` is a way to iterate over numbers, but a for loop variable can **iterate over any set of values**, not just numbers!

### STRINGS AND LOOPS
------
* these two code snippets do the same thing
* bottom one is more "pythonic"

```python
s = "abcdefgh"
for index in range(len(s)):
    if s[index] == 'i' or s[index] == 'u':
	print("There is an i or u")

for char in s:
    if char == 'i' or char == 'u':
	print("There is an i or u")
```

### CODE EXAMPLE:
------
#### ROBOT CHEERLEADERS
------

```python
an_letters = "aefhilmnorsxAEFHILMNORSX"

word = input("I will cheer for you! Enter a word: ")
times = int(input("Enthusiasm level (1-10): "))

#######################
# UNEFFICIENT EXAMPLE #
#######################
i = 0
while i < len(word):
    char = word[i]
    if char in an_letters:
	print("Give me an " + char + "! " + char)
    else:
	print("Give me a" + char + "! " +char)
    i = i + 1 						# No an efficient way

###################
# DS EXAMPLE #
###################
for char in word:
    if char in an_letters:
	print("Give me an" + char + "! " + char)
    else
	print("Give me a" + char + "! " + char)


print("What does that spell? ")
for i in range(times)
    print(word, "!!!")
```

### EXERCISE
------

```python
s1 = "mit u rock"
s2 = "i rule mit"
if len(s1) == len(s2):
    for char1 in s1:
	for char2 in s2:
	    if char1 == char2:
		print("comman letter")
		break
```

##　GUESS-AND-CHECK
------
* the process below also called **exhaustive enumeration**
* given a problem ...
  * you are able to **guess a value** for solution
  * you are able to **check if the solution is good**
  * keep guessing until find solution ror guessed all values

### GUESS-AND-CHECK - cube root
------

```python
cube = 8
for guess in range(cube+1):
    if guess**3 == cube:
	print("Cube root of", cube, "is", guess)
```

```python
cube = 8
for guess in range(abs(cube)+1):
    if guess**3 >= abs(cube):
	break
if guess**3 != abs(cube):
    print(cube, 'is not a prefect cube')
else:
    if cube < 0:
	guess = -guess
    print("Cube root of " + str(cube) + " is " + str(guess))
```

## APPROXIMATE SOLUTIONS
------
* **good enough** solution
* start with a guess and increment by some **small value**
* keep guessing if $|guess^3 - cube| >= epsilon$ for some **small epsilon**
* decreaing increment size 	-> slow program
* increasing epsion 		-> less accurate answer

### APPROXIMATE SOLUTION - cube root

```python
cube = 27
epsilon = 0.01
guess = 0.0
increment = 0.0001
num_guesses = 0
while abs(guess**3 - cube) >= epsilon and guess <= cube:
    guess += increment
    num_guesses += 1
print('num_guesses =', num_guesses)
if abs(guess**3 - cube) >= epsilon:
    print("Failed on cube root of", cube)
else:
    print(guess, 'is close to the cube root of', cube)
```

## BISECTION SEARCH
------
* half interval each iteration
* new guess is halfway in between

### BISECTION SEARCH - cube root
------

```python
cube = 27
epsilon = 0.01
num_guesses = 0
low = 0
high = cube
guess = (high + low)/2.0
while abs(guess**3 - cube) >= epsilon:
    if guess**3 < cube:
	low = guess
    else:
	high = guess
    guess = (high + low)/2.0
    num_guesses += 1
print "num_guesses =", num_guesses
print guess, "is close to the cube root of", cube
```

### BISECTION SEARCH CONVERGENCE
------
* search space
 - first guess: 	N/2
 - second guess:	N/4
 - kth guess:		N/2<sup>k</sup>
* guess converges on the order of log<sub>2</sub>N steps
* bisection search works when value of function varies monotonically with input
* code as shown only works for postitive cubes > 1 -- why?
* challenge 	-> modify to work with negative cubes!
		-> modify to work with x < 1!

### X < 1
------
* if x < 1, search space is 0 to x but cube root is greater than x and less than 1
* modify the code to choose the search space depending on value of x



